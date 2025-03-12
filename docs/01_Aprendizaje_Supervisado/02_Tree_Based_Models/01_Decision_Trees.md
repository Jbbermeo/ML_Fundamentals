# 📘 Decision Trees

## 📌 Introduction
Decision Trees are a fundamental machine learning algorithm used for **classification and regression** tasks. They work by recursively splitting data based on feature values to create a tree-like model that makes predictions in an interpretable way.

### 🔹 Why Use Decision Trees?
- **Simple and interpretable**: Easy to visualize and explain.
- **Handles numerical and categorical data**: Unlike some models that require feature engineering.
- **No need for feature scaling**: Works well without standardization or normalization.
- **Can model non-linear relationships**: Captures complex patterns through hierarchical splits.

---

## 📐 How Decision Trees Work

### 📌 Introduction
Decision Trees make predictions by recursively splitting the dataset into smaller subsets based on feature values. The goal is to find the best splits that maximize the separation between different target classes (for classification) or minimize variance (for regression).

---

### 📐 Example: Building a Decision Tree Step by Step

#### 🔹 Given Dataset:
| ID | Feature: Age | Feature: Salary (in K$) | Class: Loan Approval |
|----|-------------|----------------------|------------------|
| 1  | 25          | 30                   | No               |
| 2  | 45          | 60                   | Yes              |
| 3  | 35          | 40                   | No               |
| 4  | 50          | 80                   | Yes              |
| 5  | 23          | 25                   | No               |
| 6  | 40          | 70                   | Yes              |

### 🔹 Step 1: Selecting the Best Feature to Split
At each step, the algorithm evaluates possible splits and chooses the one that results in the best separation.

##### **Criteria for Splitting the Data:**
1. **Gini Impurity** (Classification)
   
   The Gini impurity measures how "impure" a node is. It is calculated as:
   
   $Gini = 1 - \sum_{i=1}^{c} p_i^2$

   where $( p_i )$ is the proportion of instances in class $( i )$.
   
   A pure node (only one class present) has **Gini = 0**, and a completely mixed node has **Gini close to 0.5 or higher**.

2. **Entropy & Information Gain** (Classification)
   
   Entropy measures disorder in the data:
   
   $Entropy = - \sum_{i=1}^{c} p_i \log_2(p_i)$
   
   A split is selected to maximize **Information Gain**:
   
   $IG = Entropy_{parent} - \sum_{j} \frac{|S_j|}{|S|} Entropy_j$
   
   where **S** is the dataset, and **S_j** are the subsets after splitting.
   
3. **Mean Squared Error (MSE) for Regression**
   
   For regression, we minimize the variance within splits by computing:
   
    $MSE = \frac{1}{n} \sum_{i=1}^{n} (y_i - \bar{y})^2$

   The best split is the one that reduces MSE the most.

### 🔹 Step 2: Calculating Gini and Entropy for a Split
##### **Parent Node Calculation:**
We start with all samples in the root node:

- **Class Distribution:**
  - "No" = 3 samples
  - "Yes" = 3 samples

- **Gini Impurity:**

  $Gini_{parent} = 1 - \left( \frac{3}{6} \right)^2 - \left( \frac{3}{6} \right)^2 = 0.5$


- **Entropy:**

  $Entropy_{parent} = - \left( \frac{3}{6} \log_2 \frac{3}{6} \right) - \left( \frac{3}{6} \log_2 \frac{3}{6} \right) = 1.0$

##### **After Splitting on Salary < 50K:**
| Salary Range | "No" Count | "Yes" Count |
|-------------|-----------|-----------|
| <50K       | 3         | 0         |
| >=50K      | 0         | 3         |

- **Gini After Split:**
  - Left Node: $( Gini = 1 - (3/3)^2 - (0/3)^2 = 0.0 )$
  - Right Node: $( Gini = 1 - (0/3)^2 - (3/3)^2 = 0.0 )$
  - Weighted Gini: $( Gini_{split} = \frac{3}{6} (0) + \frac{3}{6} (0) = 0.0 )$

- **Entropy After Split:**
  - Left Node: $( Entropy = - (3/3) \log_2(3/3) - (0/3) \log_2(0/3) = 0.0 )$
  - Right Node: $( Entropy = - (0/3) \log_2(0/3) - (3/3) \log_2(3/3) = 0.0 )$
  - Weighted Entropy: $( Entropy_{split} = \frac{3}{6} (0) + \frac{3}{6} (0) = 0.0 )$

Since both resulting nodes are pure, **Gini and Entropy are 0**, meaning the split is optimal.

### 🔹 Step 3: Performing the Split
Let's assume the best split is at **Salary = 50K**:

```
          [Root Node: Salary]
         /                    \
  Salary < 50K           Salary >= 50K
    [No]                 [Yes]
```
- Left branch: Instances where Salary < 50K (mostly "No" for loan approval).
- Right branch: Instances where Salary >= 50K (mostly "Yes" for loan approval).

#### 🔹 Step 3: Recursive Splitting
For the **Salary < 50K** branch, we further split on **Age** if it improves classification:

```
          [Salary]
         /       \
     <50K        >=50K
    /      \       [Yes]
 [Age < 30]  [Age >= 30]
  [No]       [No]
```
Since both leaf nodes contain only one class, the tree stops growing here.

---

### 📊 Summary of How Decision Trees Work
✅ **Splits the dataset recursively** by selecting the best feature at each step.
✅ **Uses Gini, Entropy, or MSE** to find the best split.
✅ **Stops when nodes are pure or meet a stopping condition.**
✅ **Can overfit**, so pruning methods like pre-pruning and post-pruning are needed.

---

## 🏗️ Advantages and Disadvantages
✅ **Advantages**
- Intuitive and easy to understand.
- Requires little data preprocessing.
- Can handle both classification and regression tasks.
- Can model interactions between features.

⚠️ **Disadvantages**
- **Overfitting**: Can create complex trees that generalize poorly.
- **Instability**: Small changes in data can result in a completely different tree.
- **Greedy algorithm**: May not always find the best global split.

---

## 📌 Conclusion
Decision Trees are a powerful yet simple model for classification and regression tasks. They are widely used in **finance, healthcare, and business analytics** due to their interpretability. However, they require pruning or ensemble methods (like Random Forest) to prevent overfitting.

👉 **Next Steps:** Implement Decision Trees in Python and compare them with ensemble methods like Random Forest!






