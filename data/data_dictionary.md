# LaunchML House Price Dataset Data Dictionary

## Dataset purpose

This dataset is a **synthetic educational dataset** for the LaunchML Week 4 individual capstone. It is designed to support practice with data inspection, missing-value handling, categorical encoding, exploratory analysis, and Linear Regression.

The dataset contains 1,100 rows, 11 predictor columns, and one target column. It is not official market data and must not be used as evidence about actual property prices.

## Columns

| Column | Type | Role | Description | Missing values expected? |
|---|---|---|---|---|
| `house_area_sqft` | Numeric | Predictor | Indoor house area in square feet. | No |
| `lot_area_sqft` | Numeric | Predictor | Land or lot area in square feet. | Yes |
| `bedrooms` | Numeric | Predictor | Number of bedrooms. | No |
| `bathrooms` | Numeric | Predictor | Number of bathrooms, including half-bath values where present. | Yes |
| `year_built` | Numeric | Predictor | Year in which the house was built. | No |
| `overall_quality` | Numeric | Predictor | An educational quality score from 1 to 10. | No |
| `garage_capacity` | Numeric | Predictor | Approximate number of vehicles the garage can hold. | Yes |
| `basement_area_sqft` | Numeric | Predictor | Basement area in square feet. A value of zero indicates no basement area. | Yes |
| `distance_to_city_center_km` | Numeric | Predictor | Approximate distance from the city center in kilometers. | Yes |
| `neighborhood` | Categorical | Predictor | Neighborhood category. | Yes |
| `renovation_status` | Categorical | Predictor | Renovation category: not renovated, partially renovated, or fully renovated. | Yes |
| `sale_price` | Numeric | Target | Synthetic sale price to be predicted. | No |

## Expected missing-value counts

The exact counts below describe the supplied dataset generated with seed 42. Students should still calculate missing values themselves rather than copying this table as a substitute for inspection.

| Column | Expected missing values |
|---|---:|
| `lot_area_sqft` | 25 |
| `bathrooms` | 12 |
| `garage_capacity` | 43 |
| `basement_area_sqft` | 54 |
| `distance_to_city_center_km` | 23 |
| `neighborhood` | 20 |
| `renovation_status` | 26 |
| All other columns | 0 |

## Target and predictors

The target is `sale_price`. It must be separated from the predictors before modeling. The remaining 11 columns are possible predictors. The categorical columns must be converted to numerical columns before they are passed to Linear Regression.

## Recommended educational cleaning approach

For missing numerical predictors, students may use the median. For missing categorical predictors, students may use the mode or a clearly labeled category such as `Unknown`. Students must explain their choice and confirm that missing predictor values no longer remain before training.

## Important disclaimer

The data are synthetic. Relationships in the dataset were created for learning purposes and do not represent verified property-market relationships. Model predictions are educational estimates, not professional appraisals.

## Reproducibility

The source dataset was generated with random seed 42. Students do not need to regenerate it. They should use the supplied CSV file and keep their train-test split reproducible by using `random_state=42`.

## References

[1]: https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html "Scikit-learn LinearRegression documentation"
[2]: https://pandas.pydata.org/docs/user_guide/missing_data.html "Pandas missing data documentation"
