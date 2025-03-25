# 📘 Support Vector Machines (SVM)

## 📌 Introduction
Support Vector Machines (SVM) are powerful **supervised learning algorithms** used for both **classification** and **regression** tasks. SVMs aim to find the **optimal hyperplane** that best separates the data into classes by maximizing the margin between them.

### 🔹 Why Use SVM?
- **Effective in high-dimensional spaces**
- **Robust to overfitting**, especially in cases with a clear margin of separation
- **Can model non-linear decision boundaries** using kernel tricks

---
## 📌 Objective of SVM
Support Vector Machines (SVMs) aim to find a **hyperplane** that best separates a dataset into classes by **maximizing the margin** between them. The fundamental idea is to define a decision boundary that is as far as possible from the closest points of each class, known as **support vectors**.
![SVM](https://static.wixstatic.com/media/8f929f_7ecacdcf69d2450087cb4a898ef90837~mv2.png)  

---

## 🔹 Step-by-Step Mathematical Breakdown

### 1️⃣ Problem Setup
We are given a training dataset:

$(x_1, y_1), (x_2, y_2), ..., (x_n, y_n), \quad x_i \in \mathbb{R}^d, \quad y_i \in \{-1, 1\}$

Each $( x_i )$ is a feature vector in a $( d )$-dimensional space, and $( y_i )$ is its binary class label.

We want to find a hyperplane defined by:

$\mathbf{w}^T x + b = 0$

This hyperplane should divide the space such that:
- All points from class \(+1\) lie on one side
- All points from class \(-1\) lie on the other

For correct classification:

$y_i(\mathbf{w}^T x_i + b) > 0 \quad \forall i$

---

### 2️⃣ Functional Margin
To formalize this, we introduce the concept of **functional margin**, which is defined as:

$\hat{\gamma}_i = y_i(\mathbf{w}^T x_i + b)$

This value tells us how confidently a sample is classified:
- If $( \hat{\gamma}_i > 1 )$: correctly classified and far from boundary
- If $( \hat{\gamma}_i = 1 )$: on the margin
- If $( \hat{\gamma}_i < 1 )$: either within the margin or misclassified

To ensure a clean margin, we impose the constraint:

$y_i(\mathbf{w}^T x_i + b) \geq 1$

This constraint simplifies further optimization.

---

### 3️⃣ Geometric Margin
However, functional margin is **scale-dependent** (i.e., multiplying $( \mathbf{w}, b )$ by a constant scales $( \hat{\gamma}_i )$. We care about the actual geometric distance between a point and the hyperplane:

$\gamma_i = \frac{\hat{\gamma}_i}{\|\mathbf{w}\|} = \frac{y_i(\mathbf{w}^T x_i + b)}{\|\mathbf{w}\|}$

So the **true objective** becomes maximizing the **minimum geometric margin** across all samples:

$\max_{\mathbf{w}, b} \ \min_i \ \gamma_i$


---

### 4️⃣ Margin Maximization → Optimization Problem
To remove the scale ambiguity and simplify the problem, we fix the functional margin to $( \hat{\gamma}_i = 1 )$ and convert our geometric maximization into the equivalent optimization problem:

$\min_{\mathbf{w}, b} \ \frac{1}{2} \|\mathbf{w}\|^2 \quad \text{subject to} \quad y_i(\mathbf{w}^T x_i + b) \geq 1, \quad \forall i$

- Objective: minimize the squared norm of $( \mathbf{w} )$, which increases the margin
- Constraints: ensure correct classification and proper margin

This is a **quadratic programming problem with linear constraints**—convex and solvable efficiently.

![Maximunmh](https://static.packt-cdn.com/products/9781783555130/graphics/3547_03_07.jpg)
---

### 5️⃣ Lagrangian Dual Formulation
To solve this constrained optimization, we introduce **Lagrange multipliers** $( \alpha_i \geq 0 )$ for each constraint. The primal Lagrangian is:

$\mathcal{L}(\mathbf{w}, b, \alpha) = \frac{1}{2} \|\mathbf{w}\|^2 - \sum_{i=1}^n \alpha_i \left[y_i(\mathbf{w}^T x_i + b) - 1\right]$

To find the saddle point, we take the derivatives and set them to zero:
- $( \frac{\partial \mathcal{L}}{\partial \mathbf{w}} = 0 \Rightarrow \mathbf{w} = \sum_{i=1}^n \alpha_i y_i x_i )$
- $( \frac{\partial \mathcal{L}}{\partial b} = 0 \Rightarrow \sum_{i=1}^n \alpha_i y_i = 0 )$

Substitute back into $( \mathcal{L} )$ to get the **dual problem**:

$\max_{\alpha} \sum_{i=1}^n \alpha_i - \frac{1}{2} \sum_{i=1}^n \sum_{j=1}^n \alpha_i \alpha_j y_i y_j x_i^T x_j$

Subject to:

$\alpha_i \geq 0, \quad \sum_{i=1}^n \alpha_i y_i = 0$

This is the **dual formulation**, which depends only on the dot products of inputs.

---

### 6️⃣ Final Classifier
After solving the dual problem, we obtain $( \alpha_i )$, and then compute:
- $( \mathbf{w} = \sum \alpha_i y_i x_i )$
- Choose any support vector $( x_s )$ (where $( \alpha_s > 0 )$) to compute $( b )$:

$b = y_s - \mathbf{w}^T x_s$

The final classifier becomes:

$f(x) = \text{sign}(\mathbf{w}^T x + b)$

Or, in terms of $( \alpha )$:

$f(x) = \text{sign}\left(\sum_{i=1}^n \alpha_i y_i x_i^T x + b\right)$

This version is key for introducing **kernels**.

---

## 🌐 Kernel Trick Integration
Sometimes the data is **not linearly separable** in the original feature space. Rather than explicitly mapping the data to a higher-dimensional space using a transformation $( \phi(x) )$, SVM uses the **kernel trick**:

Instead of computing $( x_i^T x_j )$, we compute:

$K(x_i, x_j) = \phi(x_i)^T \phi(x_j)$

This lets us use SVMs in very high (even infinite) dimensional spaces **without ever computing $( \phi(x) )$ explicitly**.

### 🔁 Dual Problem with Kernel
With kernels, the dual becomes:

$\max_{\alpha} \sum_{i=1}^n \alpha_i - \frac{1}{2} \sum_{i=1}^n \sum_{j=1}^n \alpha_i \alpha_j y_i y_j K(x_i, x_j)$

Subject to:

$\alpha_i \geq 0, \quad \sum_{i=1}^n \alpha_i y_i = 0$


### 🔁 Final Classifier with Kernel
The classifier becomes:

$f(x) = \text{sign}\left(\sum_{i=1}^n \alpha_i y_i K(x_i, x) + b\right)$

---

## 🔧 Hyperparameters in SVM
| Hyperparameter | Description |
|----------------|-------------|
| **C** | Controls trade-off between margin and misclassification. Low C = wider margin, high C = fewer misclassified points |
| **kernel** | Function used to map data to higher dimensions: 'linear', 'poly', 'rbf', 'sigmoid' |
| **gamma** | Controls how far the influence of a single training example reaches in RBF/polynomial kernels |
| **degree** | Degree of the polynomial kernel function (if `kernel='poly'`) |

---

## 📊 SVM vs. Other Models
| Feature               | SVM         | Logistic Regression | k-NN     |
|-----------------------|-------------|---------------------|----------|
| Handles non-linearity | Yes (with kernels) | Limited          | Yes      |
| Works in high dimensions | Excellent    | Good                | Poor     |
| Sensitive to noise    | Yes         | Moderate             | High     |
| Interpretability      | Low         | High                 | Low      |
| Training time         | Slow        | Fast                 | Fast     |

---

## 🏗️ Advantages and Disadvantages
✅ **Advantages**
- Works well for **high-dimensional data**
- Effective for **margin-based classification**
- **Versatile** through different kernel choices

⚠️ **Disadvantages**
- **Computationally expensive** for large datasets
- **Difficult to interpret** compared to linear models
- Requires careful tuning of hyperparameters (C, gamma, kernel)

---

## 📌 Conclusion
SVM is a powerful and flexible algorithm, ideal for complex decision boundaries and high-dimensional data. With appropriate kernel choice and hyperparameter tuning, it can achieve excellent performance in both linear and non-linear classification problems.

👉 **Next Steps:** Implement SVM in Python using scikit-learn and experiment with different kernels [here](/notebooks/01_Supervised_Learning/04_Distance_Based_Models/02_SVM.ipynb)!

