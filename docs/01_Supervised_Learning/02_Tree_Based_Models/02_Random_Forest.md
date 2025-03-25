# 📘 Random Forest

## 📌 Introduction
Random Forest is an **ensemble learning method** that builds multiple decision trees and combines their predictions to improve accuracy and reduce overfitting. It is used for both **classification and regression** tasks.

### 🔹 Why Use Random Forest?
- **More accurate than a single Decision Tree**: Reduces variance by averaging multiple trees.
- **Robust to overfitting**: By using multiple trees, it generalizes better to unseen data.
- **Handles missing data well**: Can handle missing values without the need for imputation.
- **Can handle high-dimensional data**: Works well with many features.

---

## 📐 How Random Forest Works
### 🔹 Ensemble Learning: Bagging vs. Boosting
Random Forest belongs to a family of **ensemble methods**, where multiple models are combined to improve predictions. There are two main types of ensemble learning:

1. **Bagging (Bootstrap Aggregating)** → Used in **Random Forest**
   - Each tree is trained on a **random sample (with replacement)** of the dataset (Bootstrapping).
   - The models are trained **independently in parallel**.
   - Predictions are aggregated using **majority voting (classification)** or **averaging (regression)**.

2. **Boosting** (Used in models like Gradient Boosting, AdaBoost, XGBoost)
   - Trees are trained **sequentially**, where each new tree corrects mistakes from the previous tree.
   - Weak models are combined into a stronger model by adjusting their weights.
   - More computationally expensive but often achieves better accuracy.

### 🔹 Step 1: Bootstrapping (Bagging)
Random Forest creates **multiple Decision Trees** using different subsets of the dataset:
- Selects a **random sample (with replacement)** of the training data for each tree.
- Each tree is trained independently on its own subset.

### 🔹 Step 2: Feature Randomness (Random Subspace Method)
- Each tree considers only a **random subset of features** when making splits.
- This ensures that trees are **decorrelated**, improving robustness.

### 🔹 Step 3: Aggregation of Predictions
- **For classification**: Uses **majority voting** (the most common class among trees is chosen).
- **For regression**: Uses **averaging** (the mean of all tree predictions is taken).

### 🔹 How Does Random Forest Look?
Visually, Random Forest consists of multiple trees that operate independently:
```
            [Root Node]                [Root Node]                 [Root Node]
           /         \                 /         \                 /         \
      [Split1]     [Split2]       [Split3]     [Split4]       [Split5]     [Split6]
        /   \         /   \           /   \         /   \          /   \         /   \
    [Leaf] [Leaf]  [Leaf] [Leaf]   [Leaf] [Leaf]  [Leaf] [Leaf]  [Leaf] [Leaf]  [Leaf] [Leaf]
```
- Each tree makes a prediction independently.
- The final decision is **based on aggregation of all tree predictions**.

---

## 🏗️ Advantages and Disadvantages
✅ **Advantages**
- **Higher accuracy** than a single Decision Tree.
- **Reduces overfitting** due to averaging multiple trees.
- **Handles both classification and regression** tasks well.
- **Works well with large datasets and high-dimensional spaces.**

⚠️ **Disadvantages**
- **Slower than a single Decision Tree**: Training multiple trees increases computation time.
- **Less interpretable**: Harder to understand compared to a single tree.
- **Memory-intensive**: Requires storing multiple models in memory.

---

## 📊 Random Forest Hyperparameters
Key hyperparameters include:
- **n_estimators**: Number of trees in the forest (higher = better stability but slower training).
- **max_features**: Number of features each tree considers (lower = more randomness, higher = more similarity to a single tree).
- **max_depth**: Limits the depth of each tree to prevent overfitting.
- **min_samples_split**: Minimum samples required to split an internal node.
- **bootstrap**: Whether to use bootstrapping when building trees.

---

## 📌 Conclusion
Random Forest is a powerful ensemble method that improves upon Decision Trees by reducing overfitting and increasing accuracy. It works by combining multiple weak learners (Decision Trees) through **bagging and feature randomness**, making it more robust and generalizable.

👉 **Next Steps:** Implement Random Forest in [Python](/notebooks/01_Supervised_Learning/02_Tree_Based_Models/02_Random_Forest.ipynb)!

