# House Price Prediction — LaunchML Week 4 Capstone Report

**Student name:** Abenezer Abebe
**Project question:** How accurately can a Linear Regression model predict house sale prices from the available property features?

## 1. Problem definition

The target variable is `sale_price`, a continuous dollar value, which makes this a **regression** problem rather than a classification one — the goal is to predict a numeric quantity, not sort houses into categories. Property characteristics such as house area, lot area, number of bedrooms and bathrooms, year built, overall quality rating, garage capacity, basement area, distance to the city center, neighborhood, and renovation status were used as predictors, since these are the kinds of features that plausibly relate to what a house sells for.

## 2. Dataset description

The dataset (`data/launchml_house_prices.csv`) contains **1,100 rows and 12 columns** (11 predictors plus the `sale_price` target). Nine predictors are numerical (`house_area_sqft`, `lot_area_sqft`, `bedrooms`, `bathrooms`, `year_built`, `overall_quality`, `garage_capacity`, `basement_area_sqft`, `distance_to_city_center_km`) and two are categorical (`neighborhood`, `renovation_status`).

This is a **synthetic, educational dataset** and is not official real-estate market data. Results here should not be treated as real-world property valuations.

## 3. Data preparation decisions

Inspection showed several columns with missing values, and no missing values in the target:

| Column | Missing values |
|---|---|
| lot_area_sqft | 25 |
| bathrooms | 12 |
| garage_capacity | 43 |
| basement_area_sqft | 54 |
| distance_to_city_center_km | 23 |
| neighborhood | 20 |
| renovation_status | 26 |
| all other columns (incl. sale_price) | 0 |

No duplicate rows were found (`df.duplicated().sum()` returned 0), so no rows needed to be dropped for that reason.

Missing values were handled inside a scikit-learn `Pipeline`/`ColumnTransformer`, so the same fitted imputers used on the training data were applied to the test data — this avoids leaking test-set information into training:

- **Numerical columns** — missing values filled with the **median** of each column. Median was chosen over mean because it is less sensitive to outliers (e.g. a few very large or very small houses skewing the average).
- **Categorical columns** (`neighborhood`, `renovation_status`) — missing values filled with the **most frequent category** in that column, then one-hot encoded so Linear Regression could use them numerically.

## 4. Exploratory findings

The first visualization (house area vs. sale price) shows a clear, strong **positive linear relationship**: larger houses consistently sell for more, and the fitted trend line tracks the bulk of the data closely, with some natural scatter around it and a handful of higher-priced outliers above ~3,500 sqft. This suggests house area is one of the more influential predictors of price, though it does not by itself prove that area *causes* the price — other correlated factors (like quality or neighborhood) may also be at play.

## 5. Modeling method

A **Linear Regression** model (scikit-learn's `LinearRegression`) was trained inside a pipeline that first imputes missing values and one-hot encodes the categorical features, then fits the regression. Per the project's scope rule, no other model type was used or compared.

The data was split with `train_test_split(test_size=0.20, random_state=42)`, giving **880 training rows and 220 testing rows**. Evaluating on a held-out test set — data the model never saw during training — is necessary because a model can effectively "memorize" its training data; testing on unseen rows is what shows whether it generalizes.

## 6. Evaluation metrics

| Metric | Value | Meaning |
|---|---|---|
| MAE | $83,051 | On average, predictions are off by about $83,051 in either direction. |
| MSE | 1.19 × 10¹⁰ | Squared-error version of the above; large errors are penalized more heavily, but the units (squared dollars) aren't directly interpretable. |
| RMSE | $109,140 | The square root of MSE, brought back into dollar units — a bit higher than MAE because it's more sensitive to a handful of larger errors. |
| R² | 0.881 | The model explains about **88.1%** of the variation in sale price on the test set, leaving roughly 12% unexplained by these features and this linear model. |

For context, the dataset's `sale_price` ranges from about $240,622 to $2,430,174 with a mean around $880,829 — so a typical error of roughly $83,000–$109,000 represents a meaningful but not huge share of a typical house's price.

## 7. Visualizations

**Visualization 1 — House Area vs. Sale Price** (`images/visualization_1_house_area_vs_price.png`)
Shows a strong positive relationship between house area and price, with the fitted line closely tracking the trend across most of the range, and slightly wider scatter at the high end.

**Visualization 2 — Actual vs. Predicted Sale Prices** (`images/visualization_2_actual_vs_predicted.png`)
Most points sit close to the "perfect prediction" reference line, especially in the $250,000–$1,250,000 range, indicating good agreement between actual and predicted prices there. A smaller number of points — mostly higher-priced houses — fall noticeably off the line, meaning the model's predictions get less precise at the top end of the price range.

**Visualization 3 — Residuals vs. Predicted Sale Prices** (`images/visualization_3_residuals.png`)
Residuals are centered around zero across most of the predicted-price range, which is a good sign — it means the model isn't systematically over- or under-predicting overall. However, the spread of residuals widens somewhat at higher predicted prices, and the largest individual errors (several in the $200,000–$480,000 range) tend to occur among the more expensive homes in the test set.

## 8. Interpretation of results

- **Features most related to price:** `house_area_sqft` shows the clearest visible relationship with `sale_price` in exploration. Other features (overall quality, bathrooms, neighborhood, etc.) were included in the model but weren't individually visualized here — a natural follow-up would be to inspect the model's fitted coefficients to rank each feature's contribution.
- **Missing values:** handled via median imputation for numeric columns and most-frequent-category imputation for categorical columns, fitted only on training data to prevent leakage (see Section 3).
- **Model performance:** an R² of 0.881 and an average error (MAE) of about $83,000 indicate the model captures the large majority of the price pattern in this dataset, though it is not highly precise for every individual house.
- **Where errors are largest:** the biggest absolute errors in the test set cluster among higher-priced homes (several actual prices above $1,400,000 had errors of $200,000+), suggesting the linear model underfits some of the pricing dynamics at the top of the market — possibly because price growth isn't perfectly linear at the high end, or because fewer expensive homes exist in the training data for the model to learn from.

## 9. Limitations

1. **Synthetic data** — this dataset was generated for educational purposes and does not reflect real market dynamics, so these results cannot be generalized to actual real-estate prices.
2. **Linear-only relationships** — Linear Regression assumes each feature relates to price in a straight-line way; if the true relationship is curved (e.g. diminishing returns on very large houses), the model can't capture that, which may explain some of the larger errors at higher price points.
3. **Imputed missing values** — filling missing values with medians/most-frequent categories is a simple, practical approach, but it can slightly understate the true variability in those columns and may not reflect the real (unknown) values.
4. **Correlation vs. causation** — a feature relating to price in this dataset (like house area) does not prove it causes the price to be what it is; other unmeasured factors could be responsible.
5. **Sample size** — 1,100 rows (880 for training) is a modest amount of data for a regression task with 11 predictors, which limits how confidently the model's patterns generalize.

## 10. Conclusion

Overall, a Linear Regression model was able to predict house sale prices in this dataset reasonably well, explaining about 88% of the variance in price on unseen test data with an average error of roughly $83,000. House area emerged as a clearly visible driver of price during exploration. The model performed best on mid-range-priced homes and was noticeably less precise for higher-priced properties, which is a reasonable limitation given the model's linear assumption and the synthetic nature of the data. This project reinforced the importance of properly separating training and test data, handling missing values thoughtfully before modeling, and interpreting evaluation metrics and residual patterns rather than treating a single metric as the whole story.

## 11. Reproducibility

1. Clone the repository: `git clone https://github.com/AK-Haking/Abenezer-Abebe-house-price-capstone.git`
2. Install dependencies: `pip install -r requirements.txt`
3. Open `notebooks/completed_student_project.ipynb` in Jupyter or Google Colab.
4. Ensure `data/launchml_house_prices.csv` is available at the path referenced in the notebook (`DATA_PATH`).
5. Run all cells from top to bottom — the split uses `random_state=42`, so results should reproduce exactly.
