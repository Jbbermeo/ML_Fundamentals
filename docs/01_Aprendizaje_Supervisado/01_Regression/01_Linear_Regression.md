# 📘 Linear Regression: Mathematical Foundations

## 📌 Introduction
Linear Regression is one of the most fundamental techniques in Machine Learning. It models the relationship between a dependent variable $(y)$ and one or more independent variables $(X)$ by fitting a linear equation to the observed data. The goal is to minimize the error between the predicted and actual values using mathematical optimization techniques.

## 📐 Mathematical Foundation

### 🔹 The Linear Model
For a simple linear regression with a single predictor variable:

$y = \beta_0 + \beta_1 x + \epsilon$

where:
- $(y)$ is the dependent variable (target output)
- $(x)$ is the independent variable (feature input)
- $(\beta_0)$ is the intercept (bias term)
- $(\beta_1)$ is the slope (coefficient of the feature)
- $(\epsilon)$ is the error term

For multiple regression with $(n)$ features:

$y = \beta_0 + \beta_1 x_1 + \beta_2 x_2 + \dots + \beta_n x_n + \epsilon$

This equation can be rewritten using matrix notation:

$\mathbf{y} = \mathbf{X} \boldsymbol{\beta} + \boldsymbol{\epsilon}$
where:
- $(\mathbf{y})$ is an $(m \times 1)$ vector of target values
- $(\mathbf{X})$ is an $( m \times (n+1))$ matrix of input features (including a column of ones for $( \beta_0)$)
- $(\boldsymbol{\beta})$ is an $((n+1) \times 1)$ vector of coefficients
- $(\boldsymbol{\epsilon})$ is an $(m \times 1)$ error term vector

### 🔹 Cost Function: Mean Squared Error (MSE)
The most common cost function for linear regression is the **Mean Squared Error (MSE)**:

$J(\boldsymbol{\beta}) = \frac{1}{m} \sum_{i=1}^{m} (y_i - \hat{y}_i)^2$

where $( \hat{y}_i )$ is the predicted value for $( x_i )$.

In matrix form:

 $J(\boldsymbol{\beta}) = \frac{1}{m} (\mathbf{y} - \mathbf{X} \boldsymbol{\beta})^T (\mathbf{y} - \mathbf{X} \boldsymbol{\beta})$


#### Why use MSE?
- **Smooth and differentiable**: Unlike absolute error, the squared term ensures that the function is continuously differentiable, making optimization easier.
- **Penalizes larger errors**: Squaring the errors gives more weight to large deviations, making the model focus on minimizing significant mistakes.
- **Alternative Loss Functions**:
  - **Mean Absolute Error (MAE)**: Useful when outliers are present but lacks differentiability at zero.
  - **Huber Loss**: A combination of MSE and MAE, robust to outliers.
  - **Log-Cosh Loss**: Similar to Huber but differentiable everywhere.

### 🔹 Derivation of the Normal Equation
To find the optimal parameters $( \boldsymbol{\beta})$, we minimize $( J(\boldsymbol{\beta}))$ by taking its derivative with respect to $( \boldsymbol{\beta})$ and setting it to zero:

$ \frac{d}{d \boldsymbol{\beta}} J(\boldsymbol{\beta}) = \frac{d}{d \boldsymbol{\beta}} \frac{1}{m} (\mathbf{y} - \mathbf{X} \boldsymbol{\beta})^T (\mathbf{y} - \mathbf{X} \boldsymbol{\beta}) = 0$

Expanding the derivative:

 $-\frac{2}{m} \mathbf{X}^T (\mathbf{y} - \mathbf{X} \boldsymbol{\beta}) = 0$

Solving for $( \boldsymbol{\beta})$:

 $\mathbf{X}^T \mathbf{X} \boldsymbol{\beta} = \mathbf{X}^T \mathbf{y}$

 $\boldsymbol{\beta} = (\mathbf{X}^T \mathbf{X})^{-1} \mathbf{X}^T \mathbf{y}$


### 🔹 Interpretation of the Normal Equation
- $(\mathbf{X}^T \mathbf{X})^{-1}$ represents the inverse of the covariance matrix of $( X )$, ensuring that features are not collinear.
- The term $( \mathbf{X}^T \mathbf{y} )$ represents the correlation between input variables and the output.
- This method is computationally efficient for small datasets but **not scalable for large datasets** due to the matrix inversion operation $O(n^3) $.

## 📌 Conclusion
Linear Regression is a fundamental model that relies on algebraic principles to establish relationships between variables. The cost function plays a critical role in optimizing predictions, and the Normal Equation provides an analytical solution to parameter estimation. While useful for small-scale problems, alternative optimization methods like **Gradient Descent** are necessary for handling large datasets efficiently.

---

**Next Steps:** Explore a Linear regression exercise [here](/notebooks/01_Aprendizaje_Supervisado/01_Regression/01_Linear_regression.ipynb)!

