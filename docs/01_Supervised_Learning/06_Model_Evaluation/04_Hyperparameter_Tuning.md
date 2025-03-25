# 📘 Hyperparameter Tuning in Machine Learning

## 📌 Introduction
Hyperparameter tuning is the process of **optimizing the configuration settings** that control the behavior of a machine learning algorithm. Unlike model parameters (learned from data), **hyperparameters** are set manually **before training begins** and can have a significant impact on model performance.

Tuning helps find the best combination of hyperparameters to improve generalization, reduce overfitting, and maximize accuracy or other performance metrics.

---

## 🔧 What are Hyperparameters?
Examples include:
- Learning rate
- Number of trees (in Random Forest)
- Maximum depth of a decision tree
- Regularization strength (lambda)
- Number of hidden units or layers in a neural network
- Kernel type in SVM

---

## 🧪 Why Tune Hyperparameters?
- Improve model performance
- Reduce underfitting or overfitting
- Select the best version of a model before deployment

Without tuning, default values may not yield optimal performance.

---

## 🔄 Common Tuning Strategies

### 1️⃣ Grid Search
- Exhaustively tries all combinations of specified hyperparameter values
- Simple, but computationally expensive

📌 Example:
```python
from sklearn.model_selection import GridSearchCV
params = {'C': [0.1, 1, 10], 'kernel': ['linear', 'rbf']}
model = GridSearchCV(SVC(), param_grid=params, cv=5)
```

### 2️⃣ Random Search
- Randomly samples combinations from the hyperparameter space
- More efficient when some parameters are more important than others

📌 Example:
```python
from sklearn.model_selection import RandomizedSearchCV
params = {'C': [0.1, 1, 10], 'gamma': [0.001, 0.01, 0.1]}
model = RandomizedSearchCV(SVC(), param_distributions=params, n_iter=10, cv=5)
```

### 3️⃣ Bayesian Optimization
- Builds a probabilistic model of the objective function
- Chooses hyperparameters that are likely to improve performance
- Examples: `Optuna`, `Hyperopt`, `BayesSearchCV`

### 4️⃣ Evolutionary / Genetic Algorithms
- Uses biologically inspired techniques to evolve the best set of hyperparameters
- Examples: `TPOT`, `DEAP`

---

## ⚙️ Best Practices
- Always combine tuning with **cross-validation**
- Monitor **validation performance**, not just training accuracy
- Use **early stopping** to avoid wasting time on poor settings
- Start with **random search** or **coarse grid**, then refine
- Scale/normalize your data before tuning where applicable

---

## 📊 Evaluation During Tuning
Use metrics aligned with your goal:
- Accuracy, F1 score (for classification)
- RMSE, R² (for regression)
- ROC AUC (for imbalanced classification)

Consider using `scoring` parameter in scikit-learn tuning functions.

---

## 📌 Conclusion
Hyperparameter tuning is critical to building well-performing machine learning models. By systematically exploring different configurations, you can greatly improve the quality, robustness, and generalization ability of your models.

👉 In the next section, we'll implement Grid Search and Random Search with real datasets and visualize their effects.

