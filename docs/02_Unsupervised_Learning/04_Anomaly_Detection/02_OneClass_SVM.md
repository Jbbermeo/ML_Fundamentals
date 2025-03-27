# 🧠 One-Class SVM – Anomaly Detection

## 📌 Overview

One-Class Support Vector Machine (One-Class SVM) is a powerful algorithm used for **unsupervised anomaly detection**. It learns a decision function that distinguishes data points similar to the "normal" class from all other possible observations, without having explicit labels for anomalies.

It is especially useful when:
- Only normal data is available during training
- Anomalies are rare and diverse
- A boundary around the "normal" region needs to be defined

---

## 📐 Intuition Behind One-Class SVM

Instead of classifying between two or more classes, **One-Class SVM** finds a **boundary** that encloses most of the training data points (assumed to be normal) in the feature space. Points that fall **outside this boundary** are considered **anomalies**.

It operates in a high-dimensional space using the **kernel trick**, making it capable of capturing **non-linear boundaries**.

Think of it as trying to:
> *"Fit a tight envelope around the majority of data points and flag any point lying outside that envelope as an outlier."*

---

## 🧮 Mathematical Formulation

Given a set of training data points $\{ \mathbf{x}_1, \mathbf{x}_2, \ldots, \mathbf{x}_n \} \in \mathbb{R}^d$, we aim to find a function $f(\mathbf{x})$ such that:

$f(\mathbf{x}) > 0 \Rightarrow \text{normal}, \quad f(\mathbf{x}) < 0 \Rightarrow \text{anomaly}$

We map the input data into a high-dimensional feature space using a kernel function $\phi(\cdot)$, and then solve the following optimization problem:

### 🎯 Primal Optimization Problem

$\min_{\mathbf{w}, \rho, \xi} \frac{1}{2} \|\mathbf{w}\|^2 + \frac{1}{\nu n} \sum_{i=1}^{n} \xi_i - \rho$

Subject to:

$(\mathbf{w} \cdot \phi(\mathbf{x}_i)) \geq \rho - \xi_i, \quad \xi_i \geq 0, \quad i = 1, \ldots, n$

Where:
- $\mathbf{w}$: normal vector of the decision boundary in feature space
- $\rho$ : offset that defines the boundary
- $\xi_i $: slack variables allowing some points to lie outside the boundary
- $\nu \in (0, 1]$: controls the trade-off between the fraction of outliers and margin size

### 🧠 Intuition Behind Parameters:
- $\nu$: An upper bound on the fraction of training errors (i.e., anomalies) and a lower bound on the fraction of support vectors. A small $\nu$ means we are strict and tolerate very few outliers.

---

## 🔁 Dual Formulation (Kernel Trick Applied)

We convert the problem into its dual form using Lagrange multipliers to make use of **kernel functions**:

$\max_{\alpha} -\frac{1}{2} \sum_{i,j=1}^{n} \alpha_i \alpha_j K(\mathbf{x}_i, \mathbf{x}_j)$

Subject to:

$0 \leq \alpha_i \leq \frac{1}{\nu n}, \quad \sum_{i=1}^{n} \alpha_i = 1$

Where:
- $\alpha_i$: Lagrange multipliers (only some will be nonzero → **support vectors**)
- $K(\mathbf{x}_i, \mathbf{x}_j) = \phi(\mathbf{x}_i) \cdot \phi(\mathbf{x}_j)$: kernel function

---

## 📏 Decision Function

Once trained, the decision function is:

$f(\mathbf{x}) = \sum_{i=1}^{n} \alpha_i K(\mathbf{x}_i, \mathbf{x}) - \rho$

- If $f(\mathbf{x}) \geq 0$, then $\mathbf{x}$ is considered **normal**  
- If $f(\mathbf{x}) < 0$, then $\mathbf{x}$ is considered an **anomaly**

---

## 🔍 Choice of Kernel

Common kernel functions include:

- **Linear**: $K(\mathbf{x}_i, \mathbf{x}_j) = \mathbf{x}_i^\top \mathbf{x}_j$   
- **Polynomial**: $K(\mathbf{x}_i, \mathbf{x}_j) = (\gamma \mathbf{x}_i^\top \mathbf{x}_j + r)^d$
- **RBF (Gaussian)**: $K(\mathbf{x}_i, \mathbf{x}_j) = \exp(-\gamma \|\mathbf{x}_i - \mathbf{x}_j\|^2)$ – *most common for anomaly detection*

The **RBF kernel** maps input data to infinite dimensions, allowing flexible and nonlinear boundaries.

---

## ✅ Advantages

- Works well in **high-dimensional** settings  
- **Kernel trick** allows for modeling complex boundaries  
- Requires only **normal data** for training  
- Suitable when anomalies are **rare or unknown** in advance

---

## ❌ Limitations

- Choice of **kernel** and **hyperparameters** ($\nu$ , $\gamma$ ) is critical  
- **Not scalable** for very large datasets (complexity grows with number of samples)  
- Can be sensitive to **noise** or overlapping distributions  
- Does **not provide probability scores**—only a binary decision function

---

## 🧪 Applications

- **Fraud detection** in banking or insurance  
- **Intrusion detection** in cybersecurity  
- **Fault detection** in manufacturing systems  
- **Medical anomaly detection** in diagnostics  
- **Sensor network monitoring** and predictive maintenance

---

## 📚 Summary

One-Class SVM is a principled and mathematically elegant method for detecting outliers and novelties in unlabeled data. By learning the boundary of a "normal" class in high-dimensional space, it enables unsupervised anomaly detection in domains where anomalies are rare, unpredictable, or unknown during training.

---
## 📓 Next Step: Hands-On with OneClass SVM

Now that you've explored the mathematical foundation of OneClass SVM, it's time to **see it in action**! [here](/notebooks/02_Unsupervised_Learning/04_Anomaly_Detection/02_OneClass_SVM.ipynb)!