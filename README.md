# LaunchML Week 4 House Price Prediction Capstone

This repository contains the student materials for the LaunchML Week 4 individual mini capstone. Each student will prepare a synthetic house-price dataset, train a **Linear Regression** model, evaluate its predictions, explain the findings, and submit the completed work through an individual GitHub repository.

## Project question

> **How accurately can a Linear Regression model predict house sale prices from the available property features?**

## Important scope rule

Students must use **Linear Regression only**. Do not replace it with Gradient Boosting, Random Forest, Decision Tree, K-Nearest Neighbors, neural networks, or another predictive model. The goal is to understand one complete machine-learning workflow from imperfect data to an explained result.

## Dataset disclaimer

`data/launchml_house_prices.csv` is a realistic synthetic educational dataset. It is not official property-market data and must not be presented as evidence about actual house prices. The dataset contains 1,100 rows, 11 predictors, one target column, numerical and categorical features, and intentional missing values for cleaning practice.

## Repository contents

| Path | Purpose |
|---|---|
| `student_project_guide.md` | Complete project instructions |
| `data/launchml_house_prices.csv` | Supplied dataset |
| `data/data_dictionary.md` | Column descriptions and missing-value expectations |
| `notebooks/student_project_template.ipynb` | Guided notebook workflow |
| `reports/report_requirements.md` | Written-report rules |
| `reports/report_template.md` | Report structure students can complete |
| `requirements.txt` | Required Python packages |
| `submissions/` | Optional local organization folder |

## Required workflow

Students should follow this sequence:

```text
Problem definition
    ↓
Load and inspect data
    ↓
Handle missing values and duplicates
    ↓
Explore relationships with Matplotlib
    ↓
Encode categorical features
    ↓
Split training and testing data
    ↓
Train Linear Regression
    ↓
Evaluate with MAE, MSE, RMSE, and R²
    ↓
Create three required visualizations
    ↓
Interpret results and limitations
    ↓
Write report and prepare presentation
    ↓
Publish the final work on GitHub
```

## Required student submission

Each student must submit an individual GitHub repository containing:

```text
README.md
requirements.txt
data/
    launchml_house_prices.csv
    data_dictionary.md
notebooks/
    completed_student_project.ipynb
reports/
    completed_report.md or completed_report.pdf
images/
    visualization_1_house_area_vs_price.png
    visualization_2_actual_vs_predicted.png
    visualization_3_residuals.png
```

The completed notebook must run from top to bottom without errors. It must contain explanations as well as code.

## Required visualizations

The completed project must include three Matplotlib images:

1. House area versus sale price, including a fitted line or clearly explained relationship.
2. Actual versus predicted sale prices, including a perfect-prediction reference line.
3. Prediction errors or residuals, with an explanation of visible patterns.

Every figure must have a title, labeled axes, and an interpretation in the notebook or report.

## Running the project locally

Install the dependencies:

```bash
pip install -r requirements.txt
```

Open the notebook:

```bash
jupyter notebook notebooks/student_project_template.ipynb
```

In Google Colab, upload the notebook and the CSV file, then update the `DATA_PATH` variable if necessary. Students should run all cells from top to bottom before submission.

## Written report and presentation

The report must describe the problem, dataset, cleaning decisions, exploratory findings, Linear Regression method, evaluation metrics, visualizations, interpretation, limitations, conclusion, and reproducibility instructions.

The final presentation should be short and should focus on the reasoning behind the project, the most important findings, the model metrics, one limitation, and what the student learned.

## Academic integrity

Students may use documentation and tutorials for learning, but submitted code and explanations must be understood and written by the student. Copying another student's analysis or presenting synthetic data as official market data is not acceptable.
# Abenezer-Abebe-house-price-capstone
