# 📏 Evaluation Metrics in Unsupervised Learning

## ❓ Why is Evaluation Challenging?

In **unsupervised learning**, we work with **unlabeled data**, which means we do not have ground truth classes or outputs to compare against. This makes evaluation significantly more challenging than in supervised learning, where metrics like accuracy or RMSE are straightforward to compute.

Therefore, in unsupervised learning, we rely on **intrinsic** and **extrinsic** evaluation strategies to assess model performance.

---

## 🧠 Intrinsic Evaluation Metrics

These metrics measure how well the model captures the structure of the data **without external references**. Common in clustering and dimensionality reduction.

### 📌 Clustering Metrics

#### 1. **Silhouette Score**

The **Silhouette Score** measures the similarity of a point to its own cluster compared to other clusters. It ranges from -1 to 1.

$s(i) = \frac{b(i) - a(i)}{\max(a(i), b(i))}$

Where:
- $a(i)$: Average distance between $i$ and all other points in the **same** cluster.
- $b(i)$: Minimum average distance from $i$ to points in the **nearest other cluster**.

✅ **Intuition**:  
- $s(i) \approx 1$: Point well matched to its own cluster, far from others.  
- $s(i) \approx 0$: Point lies on the border between two clusters.  
- $s(i) < 0$: Point may have been assigned to the wrong cluster.

---

#### 2. **Davies–Bouldin Index**

This metric evaluates intra-cluster similarity and inter-cluster difference. Lower is better.

$DB = \frac{1}{k} \sum_{i=1}^{k} \max_{j \neq i} \left( \frac{\sigma_i + \sigma_j}{d(c_i, c_j)} \right)$

Where:
- $\sigma_i$: Average distance of points in cluster $i$ to centroid $c_i$.
- $d(c_i, c_j)$: Distance between centroids $c_i$ and $c_j$.

✅ **Intuition**:  
Clusters that are compact (low intra-cluster distance) and far apart (high inter-cluster distance) will yield low DB scores.

---

#### 3. **Calinski-Harabasz Index (Variance Ratio Criterion)**

Measures the ratio of between-cluster dispersion to within-cluster dispersion.

$CH = \frac{\text{Tr}(B_k)}{\text{Tr}(W_k)} \cdot \frac{n - k}{k - 1}$

Where:
- $\text{Tr}(B_k)$: Trace of between-group dispersion matrix.
- $\text{Tr}(W_k)$: Trace of within-group dispersion matrix.
- $n$: Total number of data points.
- $k$: Number of clusters.

✅ **Intuition**:  
Higher CH values indicate better defined and separated clusters.

---

### 🔻 Dimensionality Reduction Metrics

#### 1. **Explained Variance (PCA)**

In PCA, we evaluate how much of the original data variance is preserved in the reduced space.

$\text{Explained Variance Ratio} = \frac{\lambda_i}{\sum_{j=1}^{d} \lambda_j}$

Where $\lambda_i$ is the eigenvalue of the $i$-th principal component.

✅ **Intuition**:  
The higher the explained variance ratio for a component, the more information it retains.

---

#### 2. **Reconstruction Error**

For methods like Autoencoders, the reconstruction error measures how closely the input can be reconstructed from the reduced representation.

$\text{Reconstruction Error} = \frac{1}{n} \sum_{i=1}^{n} \|x_i - \hat{x}_i\|^2$

✅ **Intuition**:  
Lower error indicates that the reduced dimensions retain more useful information.

---

## 📊 Extrinsic Evaluation Metrics

These require external references or labels and are used when such ground truth is available (e.g., in benchmarking).

#### 1. **Adjusted Rand Index (ARI)**

Measures similarity between two clusterings, correcting for chance.

$ARI = \frac{\text{RI} - \text{Expected RI}}{\max(\text{RI}) - \text{Expected RI}}$

Where RI (Rand Index) counts how many pairs of elements are assigned consistently in both clusterings.

✅ **Range**: [-1, 1]  
✅ **Interpretation**:
- 1: Perfect match  
- 0: Random labeling  
- Negative: Worse than random

---

#### 2. **Normalized Mutual Information (NMI)**

Based on information theory; measures the mutual dependence between true labels and cluster assignments.

$\text{NMI}(U, V) = \frac{2 \cdot I(U; V)}{H(U) + H(V)}$

Where:
- $I(U; V)$: Mutual Information between clusters $U$ and labels $V$.
- $H(U)$, $H(V)$: Entropies of the clusterings.

✅ **Range**: [0, 1]  
✅ **Interpretation**:
- 1: Perfect agreement  
- 0: Completely independent

---

## 🧨 Curse of Dimensionality

### 🚨 What Is It?

As the number of dimensions increases, the **volume of the space increases exponentially**, making data increasingly sparse. This has several consequences:

- Distance metrics become less meaningful.
- Clustering becomes harder (all points seem equidistant).
- Density estimation becomes unreliable.

### 🔬 Mathematical Intuition

Consider points uniformly distributed in a $d$-dimensional unit hypercube. The distance between two random points tends toward a constant:

$\text{Expected Distance} \sim \sqrt{d}$

Thus, the relative contrast between the **nearest** and **farthest** point shrinks with $d$:


$\lim_{d \to \infty} \frac{\text{max dist} - \text{min dist}}{\text{min dist}} \to 0$

🔍 **Implications**:
- Algorithms relying on **distance or density** (e.g., k-NN, DBSCAN, Isolation Forest) perform poorly in high dimensions.
- Feature selection or dimensionality reduction becomes critical.

---

## 🧭 Best Practices for Evaluation

1. **Use Multiple Metrics**: No single metric tells the full story.
2. **Visualize Clusters**: Use PCA or t-SNE for 2D/3D visualization.
3. **Consider Domain Knowledge**: Interpretability matters.
4. **Beware of High Dimensions**: Preprocess with PCA/UMAP if necessary.
5. **If You Have Labels**: Use ARI or NMI for benchmarking only.

---

## 🏁 Summary

Evaluating unsupervised models is inherently complex due to the lack of ground truth. A combination of **intrinsic metrics** (e.g., silhouette score, explained variance) and **extrinsic metrics** (e.g., ARI, NMI) can provide valuable insights. Understanding the **curse of dimensionality** is essential to avoid misleading results and to design better preprocessing pipelines.

