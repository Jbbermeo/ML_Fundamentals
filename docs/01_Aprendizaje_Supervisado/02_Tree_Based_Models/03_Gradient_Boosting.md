# 📘 Gradient Boosting

## 📌 Introduction
Gradient Boosting is a **powerful ensemble learning method** that builds multiple weak learners (typically Decision Trees) in a **sequential manner**, where each tree corrects the errors of the previous one. Unlike Random Forest, which trains trees **independently in parallel**, Gradient Boosting focuses on **learning from mistakes** to improve performance.

### 🔹 Why Use Gradient Boosting?
- **Higher accuracy than bagging methods (Random Forest)**.
- **Great for imbalanced data** by focusing on difficult-to-classify samples.
- **Works well with structured/tabular data** in regression and classification tasks.
- **Used in top-performing models** like XGBoost, LightGBM, and CatBoost.

---

## 📐 How Gradient Boosting Works

### 🔹 Step 1: Understanding the Gradient Component
The term **"Gradient"** in Gradient Boosting comes from the fact that it minimizes a **loss function** using **gradient descent**. Instead of averaging multiple models (as in Random Forest), Gradient Boosting **adjusts predictions in the direction of the negative gradient of the loss function** to minimize errors step by step.

### 🔹 Step 2: Initialize with a Weak Model
1. We start with a simple model (often a Decision Tree with low depth).
2. The model makes initial predictions $( \hat{y} )$ and computes the residuals (errors):

   $r_i = y_i - \hat{y}_i$

   where $( r_i )$ are the residuals (differences between actual and predicted values).

### 🔹 Step 3: Fit a New Model to the Residuals
1. A new Decision Tree is trained to predict the residuals from Step 2.
2. The model updates its predictions:

   $\hat{y}_i^{new} = \hat{y}_i^{old} + \lambda f(x_i)$

   where $( \lambda )$ is the learning rate, and $( f(x_i) )$ is the new tree’s prediction.
3. This step ensures that each new tree **corrects the errors** of the previous model.

### 🔹 Step 4: Repeat Sequentially
- The process continues, adding new trees that iteratively correct previous errors.
- The final model is an **ensemble of all trees**, each making small adjustments to the prediction.

### 🔹 Step 5: Visualizing Gradient Boosting
Gradient Boosting creates a sequential chain of models:
```
   [Initial Model] → [Tree 1] → [Tree 2] → [Tree 3] → ... → [Final Prediction]
```
Each tree improves on the previous one, moving predictions closer to the correct values.

---

## 📊 Why is the Gradient Used?
Gradient Boosting uses the **gradient of the loss function** to determine how much each new tree should correct the errors. For example:

- **For Regression:** The squared error loss function is used:

    $L = \sum (y_i - \hat{y}_i)^2$

  The gradient (derivative) gives us the direction to minimize this loss.

- **For Classification:** The log loss function is used:

    $L = - \sum [ y_i \log(\hat{y}_i) + (1 - y_i) \log(1 - \hat{y}_i)]$

  The gradient helps adjust predictions in a way that maximizes class separation.

---

### 🔹 Step 6: Example of Gradient Boosting in Action
Consider a **simple regression problem** where we predict house prices based on square footage.

---

## 📐 Step 1: Initial Model and Residual Calculation
Let's assume we want to **predict house prices** based on square footage. We start with a weak model (a single Decision Tree with low depth).

| House | Square Feet | Actual Price (\$1000s) | Initial Prediction (\$1000s) | Residual (Error) |
|-------|------------|-----------------|------------------|----------------|
| A     | 1500       | 300             | 250              | 50             |
| B     | 2000       | 400             | 350              | 50             |
| C     | 2500       | 500             | 400              | 100            |

- The **residual** is the difference between actual and predicted values:

  $r_i = y_i - \hat{y}_i$

  where $( r_i )$ is the error.

---

## 📐 Step 2: Fitting a New Model to the Residuals
- We **train a new tree** (Tree 2) to predict the residuals.
- Instead of predicting house prices, this tree learns the errors **left by the first model**.

| House | Square Feet | Residual (Error) | Tree 2 Prediction |
|-------|------------|----------------|------------------|
| A     | 1500       | 50             | 30               |
| B     | 2000       | 50             | 40               |
| C     | 2500       | 100            | 80               |

---

## 📐 Step 3: Updating Predictions
- The updated prediction is:

  $\hat{y}_i^{new} = \hat{y}_i^{old} + \lambda f(x_i)$

  where $( \lambda )$ is the **learning rate** (e.g., 0.1).
- Using a learning rate, we **scale the update to prevent overfitting**.

| House | Previous Prediction (\$1000s) | Scaled Update (λ = 0.1) | New Prediction (\$1000s) |
|-------|------------------|--------------------|------------------|
| A     | 250              | 0.1 × 30 = 3       | 253              |
| B     | 350              | 0.1 × 40 = 4       | 354              |
| C     | 400              | 0.1 × 80 = 8       | 408              |

---

## 📐 Step 4: Iterating Until Convergence
- We **repeat Steps 2 and 3**, training new trees to correct the remaining errors.
- Each step gets **closer to the true values**.

| Iteration | House A Prediction | House B Prediction | House C Prediction |
|-----------|--------------------|--------------------|--------------------|
| Initial   | 250                | 350                | 400                |
| Tree 2    | 253                | 354                | 408                |
| Tree 3    | 257                | 360                | 418                |
| Tree 4    | 265                | 370                | 435                |

- The model gradually **refines predictions** until errors are minimized.

---

## 📊 Why Does Gradient Boosting Work?
Gradient Boosting reduces errors efficiently by:
1. **Using the gradient of the loss function** to guide learning.
2. **Adding corrections iteratively** using small learning steps.
3. **Combining multiple weak models** into a strong final model.

---

## 🏗️ Advantages and Disadvantages
✅ **Advantages**
- Highly accurate and widely used in machine learning competitions.
- Handles non-linearity and complex interactions between features.
- Works well with both classification and regression problems.

⚠️ **Disadvantages**
- Computationally expensive compared to simpler models.
- Sensitive to hyperparameter tuning (learning rate, depth, number of trees).
- Prone to overfitting if not regularized properly.

---

## 📊 Popular Gradient Boosting Implementations
- **XGBoost**: Optimized for speed and scalability.
- **LightGBM**: Faster and more efficient with large datasets.
- **CatBoost**: Handles categorical variables efficiently.

---

## 📌 Conclusion
Gradient Boosting is a highly effective method for structured data problems, offering strong predictive power. However, it requires careful tuning to balance accuracy and overfitting.

👉 **Next Steps:** Implement Gradient Boosting in [Python](/notebooks/01_Aprendizaje_Supervisado/02_Tree_Based_Models/03_Gradient_Boosting.ipynb)!

