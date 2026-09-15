# LaunchML Week 4 Mini Capstone

## House Price Prediction with Linear Regression

Welcome to the LaunchML individual capstone project. In this project, you will use Python and machine learning to predict house sale prices from property information. You will work with a realistic synthetic dataset, prepare imperfect data, train a Linear Regression model, evaluate its predictions, explain your findings, and publish your work in a GitHub repository.

This is an individual project. You are expected to make your own decisions, write your own explanations, and understand every line of code you submit.

> **Important:** The dataset is synthetic and created for education. It is not official property-market data. Your results should not be presented as real market valuations.

## 1. Project question

Your project must answer this question:

> **How accurately can a Linear Regression model predict house sale prices from the available property features?**

Your report must also explain which features appear related to price, how you handled missing values, how well the model performed, and what limitations affect your conclusions.

## 2. Required tools

Use Python in Google Colab or Jupyter Notebook. You may use only the following main libraries:

| Library | Purpose |
|---|---|
| NumPy | Numerical operations when needed |
| Pandas | Loading, cleaning, and analyzing data |
| Matplotlib | Required visualizations |
| Scikit-learn | Train-test split, preprocessing, Linear Regression, and metrics |

You must use **Linear Regression only** as your predictive model. Do not replace it with decision trees, Random Forest, Gradient Boosting, K-Nearest Neighbors, neural networks, or another model.

## 3. Required project workflow

Complete the project in the following order.

### Step 1: Define the problem

Write a short problem definition in your notebook. Identify:

- The target you want to predict: `sale_price`.
- The available predictors.
- Whether the task is regression or classification.
- Why predicting a continuous price is a regression problem.

### Step 2: Load and inspect the data

Load the CSV file into a Pandas DataFrame. Then inspect:

- The first five rows.
- The number of rows and columns.
- Column names.
- Data types.
- Numerical summary statistics.
- Missing-value counts.
- Duplicate rows.

Do not assume that the data is clean. Show evidence from the DataFrame before making cleaning decisions.

### Step 3: Clean the data

You must handle missing values before training the model. Explain your choices in Markdown cells.

A beginner-friendly approach is:

- Fill missing numerical predictor values with the median of that column.
- Fill missing categorical predictor values with the most frequent category, or with a clearly named category such as `Unknown`.
- Confirm that no missing predictor values remain.
- Check for duplicate rows and explain whether you removed any.

Do not fill missing target values because the dataset should contain no missing `sale_price` values. If you find any, investigate and explain what you did.

### Step 4: Prepare features

Separate the data into:

- `X`: predictor columns.
- `y`: target column, `sale_price`.

The columns `neighborhood` and `renovation_status` are categorical. Linear Regression requires numerical inputs, so convert these columns into numerical indicator columns using one-hot encoding.

Avoid data leakage. The target column must not be included in `X`.

### Step 5: Explore the data

Use tables and Matplotlib charts to investigate relationships in the dataset. Look for patterns rather than trying to prove that one feature causes price changes.

Your project must include at least these three Matplotlib visualizations:

1. **House area versus sale price:** a scatter plot of `house_area_sqft` and `sale_price`. Add a clear title, axis labels, and a fitted line or another clearly explained visual indication of the relationship.
2. **Actual versus predicted prices:** after training the model, plot actual test-set prices against predicted test-set prices. Add a reference line showing where perfect predictions would fall.
3. **Prediction errors:** create a residual or error plot. Clearly label the axes and explain what the pattern suggests about model performance.

Save the three images as PNG files in an `images/` folder in your submission repository. Also display them in the notebook.

### Step 6: Split the data

Use `train_test_split` to divide the prepared data into training and testing sets. Use a test size of approximately 20% and set `random_state=42` so that your result can be reproduced.

Explain why a model should be evaluated on data that was not used for training.

### Step 7: Train the Linear Regression model

Create and fit a scikit-learn `LinearRegression` model using the training data. Record the model's learned coefficients and intercept if you can explain what they represent.

Do not train alternative models for comparison. The purpose of this capstone is to understand one complete machine-learning workflow using Linear Regression.

### Step 8: Evaluate the model

Evaluate the model on the test set. Include at least:

- Mean Absolute Error (MAE).
- Mean Squared Error (MSE).
- Root Mean Squared Error (RMSE).
- R-squared (R²).

Explain each metric in plain language. Report the units of price-based metrics in the same units as `sale_price`.

Do not claim that a metric is good or bad without explaining the context and limitations of this synthetic dataset.

### Step 9: Make predictions

Use the trained model to produce predictions for the test set. Display a small table containing:

- Actual sale price.
- Predicted sale price.
- Difference or error.

You may also create a prediction for a clearly described hypothetical property, but this is optional. If you do so, explain that it is a model estimate and not a professional valuation.

### Step 10: Interpret the results

Answer these questions in your notebook and report:

- Which numerical features appear most related to `sale_price` during exploration?
- What did you do with missing values, and why?
- How well did the model perform according to MAE, RMSE, and R²?
- What does the actual-versus-predicted chart show?
- What does the residual chart show?
- Where does the model appear to make larger errors?
- What are at least three limitations of this project?

Remember that correlation and model coefficients do not automatically prove causation.

### Step 11: Make the work reproducible

Another learner should be able to run your project by following your instructions. Therefore:

- Keep the dataset filename clear.
- Use a consistent random state.
- Run all notebook cells from top to bottom before submitting.
- Do not depend on files stored only on your personal computer.
- Include `requirements.txt` or clearly identify the required libraries.
- Use Markdown explanations beside important code sections.

## 4. Notebook requirements

Your submitted notebook must contain the following sections:

1. Title and student information.
2. Problem definition.
3. Imports and setup.
4. Load the dataset.
5. Inspect the dataset.
6. Handle missing values and duplicates.
7. Explore the data.
8. Prepare categorical features.
9. Split the data.
10. Train Linear Regression.
11. Evaluate the model.
12. Create the three required visualizations.
13. Review predictions.
14. Interpret findings.
15. Limitations and conclusion.

Every important code block must have a short explanation. A notebook containing code without interpretation is incomplete.

## 5. Report requirements

Submit a written report using the report template. The report should include:

- Project title and student name.
- Problem definition.
- Dataset description.
- Data preparation decisions.
- Exploratory findings.
- Modeling method.
- Evaluation metrics.
- Three visualizations with captions.
- Interpretation of results.
- Limitations.
- Conclusion.
- Reproducibility information.

Use your own words. Do not copy explanations from another student or from an online project.

## 6. GitHub submission requirements

Create your own GitHub repository using the provided structure. Your repository must contain:

```text
README.md
requirements.txt
data/
    launchml_house_prices.csv
a notebook file in notebooks/ or the repository root
reports/
    your written report
images/
    visualization_1.png
    visualization_2.png
    visualization_3.png
```

Your repository README must explain what the project does, how to run it, which libraries are required, and what the main results were.

## 7. Final presentation

Prepare a short individual presentation. It should explain:

1. The problem.
2. The dataset.
3. The most important cleaning decision.
4. One or two important visual findings.
5. The Linear Regression evaluation results.
6. One limitation.
7. What you learned.

Do not read every line of code during the presentation. Focus on the reasoning behind your decisions and the meaning of your results.

## 8. Common mistakes to avoid

- Using a model other than Linear Regression.
- Including `sale_price` inside the predictor matrix.
- Training before handling missing values.
- Encoding categories inconsistently between training and testing data.
- Reporting metrics without explaining them.
- Creating charts without titles or axis labels.
- Claiming that a relationship proves causation.
- Submitting a notebook that has not been run from beginning to end.
- Uploading only screenshots instead of the actual notebook and report.
- Presenting synthetic results as official real-estate statistics.

## 9. Final checklist

Before submitting, confirm that:

- [ ] I worked individually.
- [ ] I used the LaunchML dataset.
- [ ] I used Linear Regression only.
- [ ] I explained the problem as a regression task.
- [ ] I inspected missing values and duplicates.
- [ ] I handled missing values and explained my method.
- [ ] I encoded categorical features.
- [ ] I used a train-test split.
- [ ] I calculated MAE, MSE, RMSE, and R².
- [ ] I created three Matplotlib visualizations.
- [ ] My charts have titles, labels, and readable output.
- [ ] I interpreted my results in plain language.
- [ ] I discussed limitations.
- [ ] I ran the entire notebook successfully.
- [ ] I wrote the report.
- [ ] I uploaded the notebook, report, dataset, and images to GitHub.
- [ ] I prepared my final presentation.

## 10. Definition of completion

The capstone is complete only when your notebook, report, visualizations, GitHub repository, and presentation tell the same coherent story: you started with imperfect data, prepared it responsibly, trained a Linear Regression model, evaluated its predictions, and explained what the results do and do not mean.
