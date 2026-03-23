# 🏠 Ames Housing Price Prediction: Regression Analysis & Diagnostics

This project focuses on predicting residential house prices in Ames, Iowa, using the Ames Housing dataset. The primary goal was to demonstrate a full Machine Learning pipeline, from Exploratory Data Analysis (EDA) to rigorous model evaluation and diagnostic testing.

## 🏆 Key Results
I compared three different approaches to find the most balanced model:

| Model | Features | Train R² | Test R² | Test MSE |
| :--- | :--- | :--- | :--- | :--- |
| **Linear Regression** | **10 Selected** | **0.798** | **0.835** | **0.028** |
| LassoCV (Regularization) | Automated | 0.725 | 0.798 | 0.034 |
| Linear Regression | 2 Features | 0.719 | 0.775 | 0.038 |

**Key Finding:** The 10-feature Linear Regression model achieved the highest accuracy ($R^2 = 0.835$), demonstrating strong predictive power and excellent generalization to unseen data.

---

## 📊 Methodology & Workflow

### 1. Data Preprocessing & EDA
- **Handling Missing Values:** Imputed or removed missing data based on feature significance.
- **Log Transformation:** Applied log-transformation to `SalePrice` to handle skewness and normalize the distribution.
- **Feature Selection:** Identified top predictors including Overall Quality (`OverallQual`), Living Area (`GrLivArea`), and Garage capacity.

### 2. Modeling Strategy
- **Baseline:** Started with a simple 2-feature model to establish a performance floor.
- **Refinement:** Scaled features using `StandardScaler` and expanded to 10 high-correlation variables.
- **Regularization:** Implemented `LassoCV` with 5-fold cross-validation to perform automated feature selection and prevent overfitting.

### 3. Model Diagnostics (The "Internship-Ready" Part)
To ensure the model's reliability, I performed:
- **Residual Analysis:** Verified homoscedasticity (constant variance of errors).
- **Normal Q-Q Plot:** Confirmed that residuals follow a normal distribution, validating the assumptions of linear regression.

---

## 📈 Conclusion

* **Generalization:** The model demonstrated strong performance on the test set ($R^2=0.835$), slightly exceeding training metrics, which confirms the absence of overfitting.
* **Residual Analysis Insights:** The diagnostics show that errors are randomly distributed around zero. Minor deviations in the "tails" of the Q-Q plot suggest that unique, luxury properties remain the most challenging to predict with a linear approach.
* **Lasso Performance:** While LassoCV provided a robust baseline, the unregularized
