# 📘 Regularization in Machine Learning

## 📌 Introduction
Regularization is a fundamental concept in machine learning used to **prevent overfitting** by discouraging complex models. It works by adding a **penalty term** to the loss function, which penalizes large weights or overly complex hypotheses.

The idea is to strike a balance between fitting the training data well and keeping the model simple enough to generalize to unseen data.

---

## ❗ Why is Regularization Needed?
When a model is too complex, it may learn the noise in the training data (overfitting), resulting in poor performance on new data. Regularization techniques help control the model's complexity.

---

## 🔧 Types of Regularization

### 1️⃣ L1 Regularization (Lasso)
Adds the **absolute value** of the weights to the loss function:

$L = \text{Loss} + \lambda \sum_{j=1}^{n} |w_j|$

- Encourages sparsity (many weights become exactly zero)
- Useful for **feature selection**

### 2️⃣ L2 Regularization (Ridge)
Adds the **squared value** of the weights:

$L = \text{Loss} + \lambda \sum_{j=1}^{n} w_j^2$

- Encourages small, evenly distributed weights
- Helps reduce model variance

### 3️⃣ Elastic Net
Combines both L1 and L2 regularization:

$L = \text{Loss} + \lambda_1 \sum |w_j| + \lambda_2 \sum w_j^2$

- Provides a trade-off between sparsity and smoothness
- Useful when there are multiple correlated features

---

## 🧠 Intuition
- **L1** acts like a constraint that pushes weights toward zero, but may keep a few large ones
- **L2** pulls all weights closer to zero uniformly
- Adding a regularization term forces the model to explain the data with simpler weights (less reliance on any single feature)

---

## 📊 Impact on Model Training
Regularization modifies the optimization objective. The model tries to minimize:

$\text{Total Cost} = \text{Empirical Loss (e.g., MSE)} + \text{Regularization Term}$

This leads to:
- Better generalization
- Lower risk of overfitting
- Improved performance on test data

---

## 🧪 When to Use Regularization
✅ When your model overfits the training data  
✅ When the number of features is large  
✅ When you suspect multicollinearity or noise in features  
✅ When interpretability or feature selection is important (L1)

---

## ⚙️ How to Apply Regularization
In most ML libraries, you can easily apply regularization:
- **scikit-learn**: `Ridge`, `Lasso`, `ElasticNet`, `LogisticRegression(C=1/λ)`
- **Keras**: Add `kernel_regularizer=regularizers.l1/l2()` in layers
- **PyTorch**: Add weight decay in optimizer: `optimizer = SGD(..., weight_decay=λ)`

Hyperparameters (like $( \lambda )$) can be tuned with cross-validation.

---

## 📌 Conclusion
Regularization is an essential technique to build more **robust**, **generalizable**, and **interpretable** machine learning models. It allows you to control the complexity of your models by penalizing extreme parameter values.

👉 Next steps: We'll explore how to apply L1 and L2 regularization in Python with different models and datasets.