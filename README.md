# DNSC 6330 Responsible Machine Learning

This repository contains my coursework for DNSC 6330 Responsible Machine Learning.

## Repository Contents

- [`Individual_Assignment_1.ipynb`](./Individual_Assignment_1.ipynb)
- [`Individual_Assignment_2.ipynb`](./Individual_Assignment_2.ipynb)
- `README.md`

## Individual Homework 1

**File:** [`Individual_Assignment_1.ipynb`](./Individual_Assignment_1.ipynb)

### Purpose
The purpose of this assignment is to translate the complete COMPAS recidivism workflow from the Lecture 01 R notebook into Python while preserving the same analytical logic, preprocessing steps, model specification, and evaluation procedure.

### Python Libraries Used
- `pandas`
- `numpy`
- `matplotlib`
- `statsmodels`
- `scikit-learn`

### Dataset
The analysis uses the ProPublica COMPAS dataset:  
[https://raw.githubusercontent.com/propublica/compas-analysis/master/compas-scores-two-years.csv](https://raw.githubusercontent.com/propublica/compas-analysis/master/compas-scores-two-years.csv)

The original dataset contains 7,214 observations. After applying the same filtering criteria used in the R notebook, the final analytical sample contains 6,172 observations.

### Description
This notebook reproduces the COMPAS analysis from Lecture 01 in Python. The notebook includes:
- Loading the COMPAS dataset
- Reproducing the same filtering and preprocessing steps used in the R workflow
- Converting variables to categorical and datetime types
- Exploratory data analysis of race, age, sex, prior arrests, and recidivism
- Calculation of jail stay length and its relationship with COMPAS score
- Comparison of COMPAS decile score distributions across racial groups
- Construction of a logistic regression model predicting medium/high COMPAS risk scores
- Interpretation of regression coefficients and odds ratios
- Evaluation using confusion matrices, accuracy, precision, recall, false-positive rate, and false-negative rate
- Fairness analysis by race

### Main Findings
The Assignment 1 notebook shows that:
- African-American defendants are more likely than Caucasian defendants to receive higher COMPAS scores, even after controlling for age, prior arrests, charge severity, and recidivism
- Younger defendants, especially those under age 25, receive substantially higher predicted risk scores
- Prior arrests strongly increase the probability of receiving a higher COMPAS score
- African-American defendants experience higher false-positive rates, while Caucasian defendants experience higher false-negative rates

## Individual Homework 2

**File:** [`Individual_Assignment_2.ipynb`](./Individual_Assignment_2.ipynb)

### Purpose
The purpose of this assignment is to explain and audit the COMPAS replacement model developed in Assignment 1 using model explanation methods introduced in Lecture 02.

### Python Libraries Used
- `pandas`
- `numpy`
- `matplotlib`
- `scikit-learn`
- `shap`
- `lime`
- `dice-ml`

### Description
This notebook extends the COMPAS model from Homework 1 using explainability methods from Lecture 02. It includes:
- Building a logistic regression model and a gradient boosted tree model
- Comparison of prediction performance across racial groups
- SHAP beeswarm summary plots
- SHAP waterfall plots for the highest risk and lowest risk African-American and Caucasian defendants
- LIME explanations for the same individuals
- Comparison of SHAP and LIME feature attributions
- DiCE counterfactual explanations
- Identification of whether counterfactuals require changes to immutable features such as race or sex
- A governance memo discussing model behavior, explanation limitations, and recommendations for future monitoring

### Key Results: GBT Performance by Race

| race             | accuracy | **FPR**  | FNR   |
|:-----------------|---------:|---------:|------:|
| African-American |   0.694 | **0.342**| 0.273 |
| **Caucasian**    |   0.674 | **0.139**| 0.634 |
| Hispanic         |   0.617 |   0.163 | 0.622 |
| Other            |   0.723 |   0.128 | 0.667 |
| Asian            |   0.714 |   0.167 | 1.000 |
| Native American  |   1.000 |   0.000 | 0.000 |

**Key Finding:** Substantial FPR disparity persists: **African-American 0.342 vs Caucasian 0.139**.

### Main Findings

- **SHAP:** Prior arrests and age strongest drivers. Younger defendants + more priors = substantially higher risk.
- **SHAP vs LIME:** Both agree age/priors dominate. **SHAP consistent on race**, LIME variable.
- **DiCE:** Counterfactuals flip predictions **without race/sex changes**.
- **Governance:** Use **multiple explanation methods** + **regular subgroup error audits**.

## Reproducing the Analysis
**1.** Clone this repository  
**2.** Open notebooks in Jupyter/Colab  
**3.** Run cells sequentially (no manual intervention needed)

**Install packages:**
```bash
pip install pandas numpy matplotlib statsmodels scikit-learn shap lime dice-ml
```
