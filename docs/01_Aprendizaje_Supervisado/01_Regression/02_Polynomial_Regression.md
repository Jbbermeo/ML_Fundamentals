# 📘 Polynomial Regression

## 📌 Introduction
Polynomial Regression is an extension of Linear Regression that models the relationship between the dependent and independent variables as an **n-degree polynomial**. It allows us to capture non-linear relationships while still maintaining a linear approach in terms of coefficients.

### 🔹 Why Use Polynomial Regression?
- **Linear Regression is too simple** when data shows curvature.
- **Polynomial Regression adds flexibility** by introducing higher-degree terms.
- **Can model complex patterns** without requiring a non-linear model.

---

## 📐 Mathematical Foundation
### 🔹 Polynomial Regression Equation
For a simple **second-degree** polynomial, the equation is:

$y = \beta_0 + \beta_1 x + \beta_2 x^2 + \epsilon$

For a general **n-degree polynomial**, it is:

$y = \beta_0 + \beta_1 x + \beta_2 x^2 + \dots + \beta_n x^n + \epsilon$

where:
- $( y )$ is the dependent variable (target output)
- $( x )$ is the independent variable (feature input)
- $( \beta_0, \beta_1, ..., \beta_n )$ are the model coefficients
- $( \epsilon )$ is the error term

### 🔹 Matrix Representation
Using matrix notation, we define:

 $\mathbf{y} = \mathbf{X} \boldsymbol{\beta} + \boldsymbol{\epsilon}$

where:
- $( \mathbf{X} )$ is the design matrix containing polynomial terms:

$$
\mathbf{X} =
\begin{bmatrix} 
1 & x_1 & x_1^2 & \dots & x_1^n \\
1 & x_2 & x_2^2 & \dots & x_2^n \\
\vdots & \vdots & \vdots & \dots & \vdots \\
1 & x_m & x_m^2 & \dots & x_m^n
\end{bmatrix}
$$




The model is solved using the **Normal Equation**:

 $\boldsymbol{\beta} = (\mathbf{X}^T \mathbf{X})^{-1} \mathbf{X}^T \mathbf{y}$


---

## 📊 Metrics for Evaluation
### 🔹 Common Metrics Used
To evaluate the performance of Polynomial Regression, we use:
- **Mean Squared Error (MSE):** Measures the average squared difference between actual and predicted values.
- **Root Mean Squared Error (RMSE):** The square root of MSE, making it more interpretable.
- **R² Score (Coefficient of Determination):** Measures how well the model explains variability in the data.

### 🔹 When to Use Linear vs. Polynomial Regression
| Scenario | Linear Regression | Polynomial Regression |
|----------|-----------------|---------------------|
| Data is approximately linear | ✅ Yes | ❌ No |
| Data has a non-linear trend | ❌ No | ✅ Yes |
| Model needs high interpretability | ✅ Yes | ❌ No (Higher-degree polynomials are less interpretable) |
| Overfitting risk | ❌ Low | ✅ High (if degree is too high) |

- Use **Linear Regression** when the data follows a straight-line trend.
- Use **Polynomial Regression** when the relationship is curved but still follows a structured pattern.

---

## 🏗️ When to Use Polynomial Regression
✅ The data follows a **non-linear** trend but can still be approximated by a polynomial function.  
✅ You need a **simple interpretable model** without using advanced non-linear techniques.  
✅ Avoid **overfitting** by choosing an appropriate polynomial degree.  

⚠️ **Cautions:**
- **High-degree polynomials can overfit**, making predictions unstable.
- **Feature scaling is important** to prevent numerical instability.
- Consider using **regularization (Ridge/Lasso Regression)** to mitigate overfitting.


---

## 📌 Conclusion
Polynomial Regression extends Linear Regression to handle non-linear relationships by introducing polynomial terms. It is a powerful tool when applied correctly but requires careful selection of the polynomial degree to balance bias and variance.

👉 **Next Steps:** Implement Polynomial Regression in [Python](/notebooks/01_Aprendizaje_Supervisado/01_Regression/02_Polynomial_regression.ipynb)!








