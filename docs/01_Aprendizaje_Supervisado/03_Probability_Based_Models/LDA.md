# 📘 Linear Discriminant Analysis (LDA)

## 📌 Introduction
Linear Discriminant Analysis (LDA) is a **supervised learning algorithm** used for **classification** and **dimensionality reduction**. It finds a linear combination of features that best separates two or more classes.

### 🔹 Why Use LDA?
- **Maximizes class separation** by finding the best projection for classification.
- **Reduces dimensionality** while preserving the most important class-discriminative information.
- **Works well with normally distributed data** and when classes have similar covariance structures.

---

## 📐 How LDA Works
LDA transforms the dataset into a **lower-dimensional space** while keeping class separability high. It does so by:

1️⃣ **Computing the Mean Vectors** for each class.

2️⃣ **Computing the Scatter Matrices**:
   - **Within-class scatter matrix** (how samples in the same class vary).
   - **Between-class scatter matrix** (how different the classes are from each other).

3️⃣ **Computing the Linear Discriminants** by solving the eigenvalue problem.
4️⃣ **Projecting the Data** onto the new feature space.

---

## 🔢 LDA Mathematical Formulation
### 1️⃣ **Compute the Class Mean Vectors**
For each class $( C_k )$, compute the mean vector:

 $\mu_k = \frac{1}{N_k} \sum_{i=1}^{N_k} x_i$

where:
- $( \mu_k )$ is the mean vector for class $( k )$.
- $( N_k )$ is the number of samples in class $( k )$.
- $( x_i )$ represents feature values.

### 2️⃣ **Compute the Scatter Matrices**
#### **Within-Class Scatter Matrix (Sw):**

 $S_W = \sum_{k=1}^{K} \sum_{i=1}^{N_k} (x_i - \mu_k) (x_i - \mu_k)^T$

This captures the variance within each class.

#### **Between-Class Scatter Matrix (Sb):**

 $S_B = \sum_{k=1}^{K} N_k (\mu_k - \mu)(\mu_k - \mu)^T$

where $( \mu )$ is the overall mean of the dataset.

### 3️⃣ **Compute the Discriminant Directions**
To maximize class separation, we solve the eigenvalue problem:

 $S_W^{-1} S_B v = \lambda v$

where:
- $( v )$ are the eigenvectors (discriminant directions).
- $( \lambda )$ are the eigenvalues, representing the importance of each direction.

### 4️⃣ **Project the Data**
The dataset is projected onto the top $( d )$ discriminant directions, where $( d )$ is the number of classes minus one.

---

## 📊 LDA vs. PCA
| Feature | LDA | PCA |
|---------|-----|-----|
| Type | Supervised | Unsupervised |
| Goal | Maximizes class separation | Maximizes variance |
| Works with Labels? | Yes | No |
| Output | Discriminant components | Principal components |
| Best for | Classification tasks | Dimensionality reduction |

---

## 🏗️ Advantages and Disadvantages
✅ **Advantages**
- Works well for **classification problems**.
- Reduces overfitting by lowering dimensionality.
- Improves computational efficiency.

⚠️ **Disadvantages**
- Assumes **normally distributed data**.
- Requires classes to have similar **covariance structures**.
- Struggles when **class distributions overlap** significantly.

---

## 📌 Conclusion
Linear Discriminant Analysis is a powerful **classification and dimensionality reduction tool**, particularly useful when the assumptions of normality and equal covariance hold. It provides **interpretable linear boundaries** between classes and can improve model performance in classification tasks.

👉 **Next Steps:** Implement LDA in Python and compare it with PCA for dimensionality reduction!

