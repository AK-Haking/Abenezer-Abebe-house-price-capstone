# House Price Prediction — LaunchML Week 4 Capstone

**Student:** Abenezer Abebe
**Repository:** https://github.com/AK-Haking/Abenezer-Abebe-house-price-capstone

## About this project

This project predicts house sale prices from property features using a **Linear Regression** model, built as an individual capstone for the LaunchML program. The goal was to work through one complete machine-learning workflow — from imperfect, real-world-style data to an explained, evaluated result — rather than to build the single "best" possible model.

**Project question:** How accurately can a Linear Regression model predict house sale prices from the available property features?

## Dataset

`data/launchml_house_prices.csv` — the LaunchML house-price dataset, a realistic **synthetic educational dataset** (1,100 rows, 11 predictors, one target column: `sale_price`). It contains a mix of numerical and categorical features and intentional missing values for cleaning practice.

> This is synthetic data created for learning purposes. It is not official real-estate market data and should not be treated as evidence about actual house prices.

## Model

**Linear Regression only** (scikit-learn's `LinearRegression`), as required by the project scope. No other model type (e.g. decision trees, Random Forest, Gradient Boosting) was used or compared.

## How missing values were handled

The dataset had missing values in 7 columns: `lot_area_sqft` (25), `bathrooms` (12), `garage_capacity` (43), `basement_area_sqft` (54), `distance_to_city_center_km` (23), `neighborhood` (20), and `renovation_status` (26). No missing values were found in the target column, `sale_price`, and no duplicate rows were found.

- Missing **numerical** predictor values were filled with the **median** of each column, using a scikit-learn `SimpleImputer` inside a `Pipeline`, to avoid extreme values skewing the fill.
- Missing **categorical** predictor values (`neighborhood`, `renovation_status`) were filled with the **most frequent category** in that column, then one-hot encoded.
- All imputation was fitted only on the training split, then applied to the test split, to avoid data leakage.

## Evaluation metrics calculated

- Mean Absolute Error (MAE)
- Mean Squared Error (MSE)
- Root Mean Squared Error (RMSE)
- R-squared (R²)

| Metric | Value |
|---|---|
| MAE | $83,051 |
| MSE | 1.19 × 10¹⁰ |
| RMSE | $109,140 |
| R²  | 0.881 |

## Main findings

The model explains about 88.1% of the variance in sale price on the held-out test set (R² = 0.881), with a typical prediction error of roughly $83,000 (MAE). `house_area_sqft` showed the clearest positive relationship with price during exploration. Predictions were closest to actual prices for mid-range homes, and residuals were centered near zero overall, but the model's errors grew larger and more variable for higher-priced properties — suggesting the linear model underfits somewhat at the top end of the market. See `reports/completed_report.md` for the full write-up.

## Repository structure

```
Abenezer-Abebe-house-price-capstone/
├── README.md
├── requirements.txt
├── data/
│   ├── launchml_house_prices.csv
│   └── data_dictionary.md
├── notebooks/
│   └── completed_student_project.ipynb
├── reports/
│   └── completed_report.md
└── images/
    ├── visualization_1_house_area_vs_price.png
    ├── visualization_2_actual_vs_predicted.png
    └── visualization_3_residuals.png
```

## How to run this project

1. Clone this repository:
   ```
   git clone https://github.com/AK-Haking/Abenezer-Abebe-house-price-capstone.git
   cd Abenezer-Abebe-house-price-capstone
   ```
2. Install the required libraries:
   ```
   pip install -r requirements.txt
   ```
3. Open the notebook:
   ```
   jupyter notebook notebooks/completed_student_project.ipynb
   ```
   (Or upload it to Google Colab, along with `data/launchml_house_prices.csv`.)
4. Run all cells from top to bottom.

## Limitations

1. The dataset is synthetic and educational — it does not reflect real market dynamics and results should not be treated as real-world property valuations.
2. Linear Regression assumes straight-line relationships between features and price, so it cannot capture non-linear pricing patterns, which likely contributes to larger errors on higher-priced homes.
3. Missing values were filled with medians/most-frequent categories, a simple approach that may slightly understate the true variability in those columns.
4. A feature relating to price (like house area) does not prove it causes the price — other unmeasured factors could be responsible.
5. With 1,100 rows (880 for training) and 11 predictors, the sample size is modest, which limits how confidently the model's patterns generalize.
