# 📉 Principal Component Analysis (PCA)

## 🧠 What is PCA?

**Principal Component Analysis (PCA)** is an unsupervised linear dimensionality reduction technique that transforms a dataset with possibly correlated features into a set of linearly uncorrelated variables called **principal components**. These components capture the directions of maximum variance in the data.

PCA is commonly used for:
- Reducing the number of features while preserving as much variance as possible.
- Visualizing high-dimensional data in 2D or 3D.
- Noise filtering and preprocessing for other ML algorithms.

---

## 💡 Intuition Behind PCA

Imagine you have a cloud of points in 3D space. PCA finds new axes (principal components) that:
- Align with the directions where the data varies the most.
- Are orthogonal (perpendicular) to each other.
- Are ranked in order of importance (variance captured).

By projecting the data onto the top **k** components (e.g., top 2), we can reduce dimensions while keeping most of the "information" in the data.

🖼️ *Illustration idea: Show a 2D scatter plot and how PCA rotates axes to align with the data’s spread.*

---

## 📐 Mathematical Formulation

### 1. **Given**:
A dataset $X \in \mathbb{R}^{n \times d}$, where:
- $n$ is the number of samples
- $d$ is the number of original features

### 2. **Center the Data**:
Subtract the mean of each column (feature):

$X_{\text{centered}} = X - \mu$

Where $\mu \in \mathbb{R}^d $ is the mean vector.

---

### 3. **Compute the Covariance Matrix**:

$\Sigma = \frac{1}{n - 1} X_{\text{centered}}^T X_{\text{centered}}$

This matrix shows how features vary together.

---

### 4. **Compute Eigenvalues and Eigenvectors**:

Solve:

$\Sigma \mathbf{v}_i = \lambda_i \mathbf{v}_i$

- $\lambda_i$: eigenvalue (variance explained)
- $\mathbf{v}_i$: eigenvector (principal direction)

---

### 5. **Select Top k Components**:

Choose the top $k$ eigenvectors with the largest eigenvalues:

$W_k = [\mathbf{v}_1, \mathbf{v}_2, ..., \mathbf{v}_k]$

---

### 6. **Project the Data**:

Transform the original data to the new space:

$Z = X_{\text{centered}} \cdot W_k$

$Z \in \mathbb{R}^{n \times k}$ is the data in reduced dimension.

---

## 🧠 Intuition of Eigenvectors and Eigenvalues

- **Eigenvectors** define the new axes (principal components).
- **Eigenvalues** indicate how much variance is captured by each axis.
- The first component captures the most variance, the second the next most, and so on.
---

## 📊 Visual Example
![PCA](https://upload.wikimedia.org/wikipedia/commons/thumb/f/f5/GaussianScatterPCA.svg/1280px-GaussianScatterPCA.svg.png)

---

## 📊 Scree Plot

A Scree Plot visualizes eigenvalues (variance explained) by each component:

- Helps decide how many components to keep (look for the "elbow").
- Can be normalized to show **explained variance ratio**.

$\text{Explained Variance Ratio} = \frac{\lambda_i}{\sum \lambda}$

![ScreePlot](https://upload.wikimedia.org/wikipedia/commons/a/ac/Screeplotr.png)

---

## ✅ Pros and Cons of PCA

### ✅ Advantages:
- Simple and fast
- Reduces dimensionality effectively
- Decorrelates features
- Can improve training time and performance

### ❌ Limitations:
- Assumes linear relationships
- Components are not easily interpretable
- Sensitive to scaling — **standardization is crucial**
- Not ideal for non-Gaussian or nonlinear datasets

---

## 🔍 Real-World Applications
- **Image compression** (e.g., reducing 1024-pixel images to 50 principal components)

- **Gene expression analysis** in bioinformatics

- **Topic modeling** in NLP as a preprocessing step

- **Customer segmentation** and visualization

- **Noise reduction** in audio/signal processing

---
## 🏁 Summary
PCA is a powerful tool to reduce data dimensionality while preserving variance. It finds orthogonal axes of maximum variance and projects the data onto them. Despite its simplicity, PCA is widely used across many fields for exploration, visualization, and preprocessing.

## 📓 Next Step: Hands-On with PCA

Now that you've explored the mathematical foundation of PCA, it's time to **see it in action**! [here](/notebooks/02_Unsupervised_Learning/02_Dimensionality_Reduction/01_PCA.ipynb)!

