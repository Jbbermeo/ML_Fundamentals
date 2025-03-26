# 🌳 Hierarchical Clustering

Hierarchical Clustering is an **unsupervised learning algorithm** used to group similar data points into clusters based on their proximity. Unlike K-Means, which requires you to specify the number of clusters in advance, hierarchical clustering builds a **hierarchy of clusters**, represented by a tree-like diagram called a **dendrogram**.

---

## 🔍 Overview

There are two main types of hierarchical clustering:

1. **Agglomerative (Bottom-Up)**  
   Starts with each data point as its own cluster, and iteratively merges the closest clusters.

2. **Divisive (Top-Down)**  
   Starts with all data in one cluster and recursively splits the clusters.

> 🔔 Agglomerative clustering is more common and widely used, so we’ll focus on that here.

---

## 📐 Step-by-Step Algorithm (Agglomerative)

1️⃣ Compute the **distance matrix** for all data points.  
2️⃣ Treat each point as a separate cluster.  
3️⃣ Merge the two **closest** clusters.  
4️⃣ Recompute distances between new clusters and the others.  
5️⃣ Repeat until all points belong to a single cluster.

---
## 🧮 Mathematical Formulation of Hierarchical Clustering

Hierarchical Clustering is fundamentally driven by **distance computations** and **cluster linkage** strategies. In this section, we'll build the mathematical foundation **step by step**, from the raw data to the final dendrogram.

---

### 1️⃣ Data Representation

Assume a dataset with $n$ data points:

$\mathcal{X} = \{x_1, x_2, \dots, x_n\}, \quad x_i \in \mathbb{R}^d$

Each data point $x_i$ is a vector in $d$-dimensional space.

---

## 2️⃣ Distance Between Points

To begin, we compute a **distance matrix** $D \in \mathbb{R}^{n \times n}$, where each entry $D_{ij}$ is the distance between points $x_i$ and $x_j$.

### 🔹 Euclidean Distance (Default)

$D_{ij} = d(x_i, x_j) = \sqrt{\sum_{k=1}^{d} (x_{ik} - x_{jk})^2}$

🔍 **Intuition**: Measures how far two points are in straight-line space. Suitable when features are continuous and scale is meaningful.

---

## 3️⃣ Initial Cluster Setup

Each point starts in its own cluster:

$\mathcal{C}^{(0)} = \{\{x_1\}, \{x_2\}, \dots, \{x_n\}\}$

We now have $n$ singleton clusters.

---

## 4️⃣ Linkage Criterion – Cluster Distance

To merge clusters, we define **inter-cluster distance functions**. These are the rules for determining the distance between clusters $A$ and $B$.

### 🔹 Single Linkage (Minimum Pairwise Distance)

$D(A, B) = \min_{a \in A, b \in B} d(a, b)$

🔍 **Intuition**: Merge clusters based on the closest two points. Forms elongated, "chain-like" clusters.

---

### 🔹 Complete Linkage (Maximum Pairwise Distance)

$D(A, B) = \max_{a \in A, b \in B} d(a, b)$

🔍 **Intuition**: Merge only if *all* points are close. Encourages tight, spherical clusters.

---

### 🔹 Average Linkage (Mean Pairwise Distance)

$D(A, B) = \frac{1}{|A||B|} \sum_{a \in A} \sum_{b \in B} d(a, b)$

🔍 **Intuition**: Takes into account all pairwise distances, balancing single and complete linkage.

---

### 🔹 Ward’s Method (Increase in Variance)

Let $\mu_A$ and $\mu_B$ be centroids of clusters $A$ and $B$. The distance is:

$D(A, B) = \frac{|A||B|}{|A| + |B|} \cdot \|\mu_A - \mu_B\|^2$

🔍 **Intuition**: Merge the two clusters that result in the **smallest increase in total within-cluster variance**. Produces compact and balanced clusters.

---

## 5️⃣ Iterative Merging

At each step $t$, we merge the pair of clusters $(A, B)$ that minimizes $D(A, B)$:

$ (\hat{A}, \hat{B}) = \arg\min_{(A,B) \in C^{(t)}} D(A, B) $

Update the cluster set:

$C^{(t+1)} = \left( C^{(t)} \setminus \{\hat{A}, \hat{B}\} \right) \cup \{\hat{A} \cup \hat{B}\}$

Repeat until only one cluster remains.

---

## 6️⃣ Dendrogram Construction

Each merge can be represented by a triple:

$(z_i, z_j, d_{ij})$

Where:
- $z_i, z_j$: Indices of merged clusters
- $d_{ij}$: Distance between them at the time of merging

We store these in a linkage matrix $Z \in \mathbb{R}^{(n-1) \times 3}$, used to plot the dendrogram.

---

## 7️⃣ Cutting the Dendrogram

To extract $k$ clusters:

- **Cut** the dendrogram at a height where there are $k$ branches.
- This defines a **flat clustering** result.

---

## 🧠 Summary of Core Math Components

| Component                | Math Expression | Purpose |
|--------------------------|-----------------|---------|
| Point Distance           | $d(x_i, x_j)$ | Compute base similarity |
| Cluster Distance         | $D(A, B)$    | Linkage strategy |
| Ward Variance Formula    | $\frac{AB}{A + B} \mu_A - \mu_B\^2$ | Compactness criterion |
| Merge Rule               | $\arg\min D(A, B)$ | Greedy clustering |
| Dendrogram Entry         | $(z_i, z_j, d_{ij})$| Tree structure storage |

---

## 📌 Final Notes

- Hierarchical clustering builds a **greedy tree** structure.
- The math revolves around **distance computation**, **merge criteria**, and **bookkeeping of cluster structure**.
- The **linkage function is the heart** of how clusters evolve — choose it based on your data and goal.

---

> 🧭 Tip: Ward's method is often a good starting point for numerical data and performs well with Euclidean distances.


---

## 🌲 Dendrogram

A **dendrogram** is a tree diagram that shows the order and distances of merges.

![Dendrogram](https://upload.wikimedia.org/wikipedia/commons/thumb/1/1a/Dendroexample.png/800px-Dendroexample.png?20230823003024)

- Y-axis shows **distance** at which clusters were merged.
- By cutting the dendrogram at a specific height, you can choose the number of clusters.

---

## 📦 Applications

- Customer segmentation
- Gene expression analysis
- Document clustering
- Social network analysis

---

## 🧠 Intuition Behind the Math

Imagine placing each data point in its own group. We want to combine groups that are "close" to each other. But how do we define *close*?

- If you care about **the closest two points**, use **Single Linkage**.
- If you want to avoid long, spread-out clusters, use **Complete Linkage**.
- If you want **compact clusters**, **Ward’s Method** minimizes the increase in total within-cluster variance.

> Think of Ward's Method as trying to "keep the total cluster error small" while merging clusters.

---

## 📊 Pros and Cons

### ✅ Pros:
- No need to pre-specify number of clusters
- Dendrograms give interpretability
- Works well with various distance metrics

### ❌ Cons:
- Computationally expensive (time complexity: **O(n³)**)
- Sensitive to noise and outliers
- Not scalable for large datasets

---

## ✅ Conclusion

Hierarchical clustering is a powerful and interpretable clustering method, especially useful when you want to understand the nested relationships in your data. It doesn’t require specifying the number of clusters ahead of time and offers a visual hierarchy of cluster merges. For small to medium datasets, it provides valuable insights with minimal assumptions.

---

## 📓 Next Step: Hands-On with Hierarchical clustering

Now that you've explored the mathematical foundation of Hierarchical clustering, it's time to **see it in action**! [here](/notebooks/02_Unsupervised_Learning/01_Clustering/02_Hierarchical_Clustering.ipynb)!


