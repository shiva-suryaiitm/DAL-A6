# DA5401 A6: Imputation via Regression for Missing Data
# PH21B009 - Shivasurya C M

## Overview

This project explores and evaluates various strategies for handling missing data in a credit card default prediction task. The notebook systematically introduces missing values into the UCI Credit Card dataset and then applies four different handling techniques:
1.  **Median Imputation**
2.  **Linear Regression Imputation**
3.  **Non-Linear Regression (Random Forest) Imputation**
4.  **Listwise Deletion**

A Logistic Regression model is trained on each of the resulting datasets. The performance of each model is then evaluated and compared to determine the most effective strategy for this specific problem.

## Dataset

The project uses the **UCI Credit Card Default** dataset, which contains information on default payments, demographic factors, credit data, history of payment, and bill statements for credit card clients in Taiwan from April 2005 to September 2005.

## Methodology

### 1. Missing Data Simulation

To simulate a real-world scenario with missing data, `NaN` (Not a Number) values are intentionally introduced into 10% of the rows for three randomly selected numerical columns: `LIMIT_BAL`, `PAY_AMT3`, and `PAY_AMT5` [1].

### 2. Missing Data Handling Strategies

Four separate datasets are created based on different handling approaches:

*   **Dataset A (Median Imputation):** Missing values are filled with the median of their respective columns. This method is robust to outliers [1].
*   **Dataset B (Linear Regression Imputation):** Missing values in one column are predicted using a Linear Regression model trained on other available features, assuming a linear relationship exists [1].
*   **Dataset C (Non-Linear Regression Imputation):** A `RandomForestRegressor` is used to predict and impute missing values, capturing more complex, non-linear relationships between features [1].
*   **Dataset D (Listwise Deletion):** All rows containing at least one missing value are removed from the dataset. This is the simplest method but can lead to significant data loss [1].

### 3. Model Training and Evaluation

For each of the four datasets (A, B, C, D):
1.  The data is split into training (80%) and testing (20%) sets.
2.  The features are standardized using `StandardScaler`.
3.  A `LogisticRegression` model is trained on the standardized training data.
4.  The model's performance is evaluated on the test set using a classification report, which includes precision, recall, and F1-score [1].

## Results

The performance of the four models was compared to assess the effectiveness of each imputation strategy.

| Model | Imputation Method | Accuracy | F1-Score (Class 1) | Macro Avg F1-Score | Weighted Avg F1-Score |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Model A** | Median Imputation | 0.8095 | 0.3457 | 0.6171 | 0.7697 |
| **Model B** | Linear Regression | 0.8102 | 0.3503 | 0.6196 | 0.7710 |
| **Model C** | Non-Linear Regression | 0.8102 | 0.3510 | 0.6199 | 0.7711 |
| **Model D** | Listwise Deletion | 0.8093 | 0.3571 | 0.6225 | 0.7702 |

### Key Insights

*   **Accuracy:** All models achieved similar accuracy, around 81%. Models B and C had the highest accuracy (81.02%) [1].
*   **F1-Score (Class 1):** Model D (Listwise Deletion) surprisingly achieved the best F1-score for the minority class (default payment), indicating better performance on the primary prediction target despite data loss [1].
*   **Overall Performance:** The more complex imputation methods (Linear and Non-Linear Regression) showed a slight improvement over the simple Median Imputation.

## Conclusion

Based on the analysis, **Model C (Non-Linear Regression Imputation)** is recommended as the best overall strategy. Although Model D had a slightly better F1-score for the minority class, it came at the cost of reducing the dataset size. Model C provides the best balance by:
- Maintaining the complete dataset without information loss.
- Achieving the highest accuracy (tied with Model B).
- Capturing complex feature relationships, leading to strong and reliable performance metrics across the board [1].