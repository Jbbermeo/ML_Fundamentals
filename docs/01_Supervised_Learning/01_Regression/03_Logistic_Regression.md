# 📘 Logistic Regression

## 📌 Introduction
Logistic Regression is a fundamental algorithm used for **classification tasks**. Unlike Linear Regression, which predicts continuous values, Logistic Regression predicts **probabilities** and assigns data points to discrete classes. It is widely used in **binary classification problems** where the target variable has two possible outcomes (e.g., spam vs. not spam, disease vs. no disease).

### 🔹 Why Use Logistic Regression?
- **Simple yet effective for classification** problems.
- **Interpretable**—coefficients provide insights into feature importance.
- **Computationally efficient**, making it ideal for large datasets.
- **Can extend to multi-class classification** using techniques like **one-vs-rest (OvR)** or **softmax regression**.

---

## 📊 Understanding the Data
Logistic Regression is used when the target variable $( y )$ is categorical, typically **binary (0 or 1)**. Each observation consists of:
- **Features $( X )$** (independent variables): Continuous or categorical values.
- **Target Variable $( y )$**: Labels such as {0,1} indicating different classes.

### Example Dataset:
| Feature 1 (Age) | Feature 2 (Income) | Target (Buy Insurance?) |
|--------------|--------------|------------------|
| 25          | 35,000        | 0                |
| 45          | 70,000        | 1                |
| 30          | 50,000        | 0                |
| 50          | 90,000        | 1                |

---

## 📐 Mathematical Foundation
### 🔹 How the Sigmoid Function Looks

The **sigmoid function** is an S-shaped curve that maps any real number to a probability between **0 and 1**:

 $\sigma(z) = \frac{1}{1 + e^{-z}}$

![Sigmoid Function](https://miro.medium.com/max/970/1*Xu7B5y9gp0iL5ooBj7LtWw.png)  


📌 **Key Properties:**
- When **$( z \to -\infty )$**, $( \sigma(z) \to 0 )$.
- When **$( z \to \infty )$**, $( \sigma(z) \to 1 )$.
- At **$( z = 0 )$**, $( \sigma(0) = 0.5 )$.
- The function is **differentiable and has a smooth gradient**, making it ideal for optimization.

### 🔹 How the Sigmoid Function Relates to the Data
In Logistic Regression, we model the probability of an instance belonging to class **1**:

 $P(y=1 | X) = \sigma(z) = \frac{1}{1 + e^{-z}}$

where:
- **$( X )$** represents the feature inputs.
- **$( z )$** is a **linear combination** of input features: 

  $z = \beta_0 + \beta_1 x_1 + \beta_2 x_2 + \dots + \beta_n x_n$

- **$( \sigma(z) )$** maps this linear combination to a probability between **0 and 1**.

This means:
- If **$( z )$ is large and positive**, $( \sigma(z) \approx 1 )$ → The instance is likely class **1**.
- If **$( z )$ is large and negative**, $( \sigma(z) \approx 0 )$ → The instance is likely class **0**.
- If **$( z = 0 )$**, then $( \sigma(z) = 0.5 )$, meaning we are **completely uncertain** about the class.

Thus, **Logistic Regression transforms raw data through a linear function and maps it into probability space using the sigmoid function**.

### 🔹 Decision Rule
To classify an instance, we apply a threshold $( \theta )$ (commonly set at **0.5**):

$ \hat{y} = \begin{cases} 1, & \sigma(z) \geq 0.5 \\ 0, & \sigma(z) < 0.5 \end{cases}$

This means if the probability is greater than 50%, we assign class **1**, otherwise class **0**.

![Decision Rule](https://ml-cheatsheet.readthedocs.io/en/latest/_images/logistic_regression_sigmoid_w_threshold.png)  



---

## 📊 Why Does the Cost Function Change?

### 🔹 What is the Goal?
In regression models, we need a function that measures how well the predicted values match the actual labels. In Logistic Regression, the model outputs **probabilities**, not continuous values. We need a function that:
- **Penalizes incorrect classifications heavily**.
- **Encourages well-calibrated probabilities**.
- **Is convex**, allowing efficient optimization.

### 🔹 Why Not Use Mean Squared Error (MSE)?
In Linear Regression, we minimize the **Mean Squared Error (MSE)**:

 $J(\beta) = \frac{1}{m} \sum_{i=1}^{m} (y_i - \hat{y}_i)^2$

However, in Logistic Regression:
- **MSE leads to a non-convex optimization problem**, meaning gradient descent may not find the global minimum.
- **MSE does not properly penalize incorrect probability estimates**, resulting in poor probability calibration.

### 🔹 Derivation of the Log Loss (Binary Cross-Entropy)
We use **Maximum Likelihood Estimation (MLE)** to derive a cost function for Logistic Regression.
1. The probability of a correct classification for one instance is:

   $P(y | X) = \sigma(z)^y (1 - \sigma(z))^{(1 - y)}$

   - If $( y = 1 )$, we want $( \sigma(z) )$ to be close to **1**.
   - If $( y = 0 )$, we want $( 1 - \sigma(z) )$ to be close to **1**.
2. The likelihood function over all data points is:

   $L(\beta) = \prod_{i=1}^{m} \sigma(z_i)^{y_i} (1 - \sigma(z_i))^{(1 - y_i)}$

3. Taking the **log** of the likelihood function (to simplify calculations), we get the **log-likelihood**:

   $\log L(\beta) = \sum_{i=1}^{m} \left[ y_i \log(\sigma(z_i)) + (1 - y_i) \log(1 - \sigma(z_i)) \right]$

4. Since we minimize cost functions, we take the **negative** log-likelihood, giving us the **Binary Cross-Entropy (Log Loss)**:

   $J(\beta) = -\frac{1}{m} \sum_{i=1}^{m} \left[ y_i \log(\hat{y}_i) + (1 - y_i) \log(1 - \hat{y}_i) \right]$


### 🔹 What Does the Cost Function Expect?
- If $( y = 1 )$:
  - **If $( \hat{y} )$ is close to 1**, $( \log(\hat{y}) )$ is close to **0** → **Small loss** ✅.
  - **If $( \hat{y} )$ is close to 0**, $( \log(\hat{y}) )$ is very negative → **Large loss** ❌.
- If $( y = 0 )$:
  - **If $( \hat{y} )$ is close to 0**, $( \log(1 - \hat{y}) )$ is close to **0** → **Small loss** ✅.
  - **If $( \hat{y} )$ is close to 1**, $( \log(1 - \hat{y}) )$ is very negative → **Large loss** ❌.

Thus, **Log Loss assigns a large penalty when the predicted probability is far from the true label**.

---

## 📊 Are There Other Cost Functions?
While **Binary Cross-Entropy** is the standard, there are alternatives:
- **Hinge Loss (for SVMs):** Maximizes the margin between classes.
- **Exponential Loss:** Used in boosting models like AdaBoost.
- **Squared Log Loss:** Penalizes incorrect probabilities less aggressively.

### 🔹 Is Sigmoid Always Used?
- For **binary classification**, sigmoid is the standard.
- For **multi-class classification**, we use the **Softmax function**.
- In **deep learning**, other activation functions like **ReLU** are often preferred.

---

## 🏗️ When to Use Logistic Regression
✅ The target variable is **categorical** (binary or multi-class).  
✅ The relationship between features and output is **linear in the log-odds space**.  
✅ You need a **fast and interpretable** model.  

⚠️ **Cautions:**
- Logistic Regression assumes **independent features**—correlated variables can affect performance.
- It struggles with **non-linear relationships** (consider Decision Trees or Neural Networks in such cases).
- Imbalanced datasets may require techniques like **resampling, SMOTE, or class weighting**.

---

## 📊 Metrics for Evaluation
Since Logistic Regression is a classification model, standard regression metrics (like RMSE) are not appropriate. Instead, we use:

| Metric         | Description |
|---------------|-------------|
| **Accuracy**  | Overall correctness of predictions |
| **Precision** | Fraction of true positive predictions out of all predicted positives |
| **Recall**    | Fraction of true positive predictions out of actual positives |
| **F1 Score**  | Harmonic mean of precision and recall |
| **ROC-AUC**   | Measures model performance across different thresholds |

📌 **Which metric to use?**
- **For balanced datasets**, accuracy is often sufficient.
- **For imbalanced datasets**, precision, recall, and F1-score are more informative.
- **For ranking models**, ROC-AUC is useful.

---

## 📌 Conclusion
Logistic Regression is a powerful yet simple classification algorithm that works well when assumptions hold. It is widely used in applications like **spam detection, medical diagnosis, and fraud detection**.
### **Key Takeaways:**
✅ The sigmoid function **maps a linear model’s output to probabilities**.
✅ The Log Loss function **penalizes incorrect predictions exponentially**.
✅ The cost function is derived using **Maximum Likelihood Estimation**.
✅ Other loss functions exist but Binary Cross-Entropy is standard for binary classification.

👉 **Next Steps:** Implement Logistic Regression in [Python](/notebooks/01_Supervised_Learning/01_Regression/03_Logistic_regression.ipynb)!

