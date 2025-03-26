# 📌 DBSCAN: Density-Based Spatial Clustering of Applications with Noise

## 🧠 What is DBSCAN?

**DBSCAN (Density-Based Spatial Clustering of Applications with Noise)** is a popular unsupervised clustering algorithm that groups together points that are closely packed (high density) and marks as outliers the points that lie alone in low-density regions. Unlike K-Means, DBSCAN does not require the number of clusters to be specified beforehand and can identify clusters of arbitrary shape.

---

## 🎯 Key Concepts

DBSCAN relies on two main parameters:

- $ε$ (epsilon): The maximum distance between two samples for them to be considered as in the same neighborhood.
- `minPts`: The minimum number of points required to form a dense region (i.e., a cluster).

### Types of Points in DBSCAN

1. **Core Point**: A point that has at least `minPts` points within a distance `ε`.
2. **Border Point**: A point that has fewer than `minPts` within `ε`, but is in the neighborhood of a core point.
3. **Noise (Outlier) Point**: A point that is neither a core point nor a border point.

---

## 🧪 Algorithm Steps

1. For each unvisited point `p`:
   - If `p` is a **core point** (has ≥ `minPts` neighbors within distance `ε`), a new cluster is started.
   - Recursively add all **density-reachable** points from `p` to the cluster.
   - Mark all points that are **not reachable** from any core point as **noise**.

---

## 📐 Mathematical Formulation

DBSCAN (Density-Based Spatial Clustering of Applications with Noise) is built on the principle of **density-connected points** in a feature space. Unlike centroid-based methods, DBSCAN defines clusters as **dense regions** separated by areas of lower point density.

---

## 1️⃣ Distance Metric

Let $\mathbf{x}_i, \mathbf{x}_j \in \mathbb{R}^d$ be two data points in a $d$-dimensional space.

The most common distance metric used in DBSCAN is the **Euclidean distance**:

$\text{dist}(\mathbf{x}_i,\mathbf{x}_j) = \sqrt{\sum_{k=1}^{d}(x_{ik}-x_{jk})^2}$

📌 **Intuition**: This measures the "straight-line" distance between two points in Euclidean space. You can also use other metrics like Manhattan or cosine distance depending on the data.

---

## 2️⃣ ε-Neighborhood

Given a point $\mathbf{x}_i$, its **ε-neighborhood** is defined as:

$\mathcal{N}_\varepsilon(\mathbf{x}_i) = \{ \mathbf{x}_j \in \mathbb{R}^d \mid \text{dist}(\mathbf{x}_i, \mathbf{x}_j) \leq \varepsilon \}$

📌 **Intuition**: It’s the set of all points that lie within a radius $\varepsilon$ from $\mathbf{x}_i$. Think of drawing a hypersphere of radius $\varepsilon$ around $\mathbf{x}_i$.

---

## 3️⃣ Core Point Condition

A point $\mathbf{x}_i$ is a **core point** if:

$|\mathcal{N}_\varepsilon(\mathbf{x}_i)| \geq \text{minPts}$

📌 **Intuition**: A point is considered part of a dense region (a cluster seed) if enough other points fall within its ε-neighborhood.

---

## 4️⃣ Direct Density Reachability

Point $\mathbf{x}_j$ is **directly density-reachable** from $\mathbf{x}_i$ if:

- $\mathbf{x}_j \in N_\varepsilon(\mathbf{x}_i)$
- $\mathbf{x}_i$ is a **core point**

$\mathbf{x}_j \in \mathcal{N}_\varepsilon(\mathbf{x}_i) \quad \text{and} \quad |\mathcal{N}_\varepsilon(\mathbf{x}_i)| \geq \text{minPts}$

📌 **Intuition**: This establishes a one-step density connection. You must be in the ε-neighborhood of a dense (core) point.

---

## 5️⃣ Density Reachability

A point $\mathbf{x}_j$ is **density-reachable** from $\mathbf{x}_i$ if there exists a sequence of points:

$\mathbf{x}_i = \mathbf{x}_0, \mathbf{x}_1, \dots, \mathbf{x}_n = \mathbf{x}_j$

such that each $\mathbf{x}_{k+1}$ is **directly density-reachable** from $\mathbf{x}_k$.

📌 **Intuition**: A chain of direct connections through dense regions means we can reach one point from another. This relation is **not symmetric**.

---

## 6️⃣ Density Connectivity

Two points $\mathbf{x}_i$ and $\mathbf{x}_j$ are **density-connected** if there exists a point $\mathbf{x}_k$ such that both $\mathbf{x}_i$ and $\mathbf{x}_j$ are **density-reachable** from $\mathbf{x}_k$.

$\exists \, \mathbf{x}_k \; \text{such that} \; \mathbf{x}_i, \mathbf{x}_j \in \text{DensityReachable}(\mathbf{x}_k)$

📌 **Intuition**: Even if two points aren’t directly reachable, they belong to the same cluster if there's a common dense path connecting them.

---

## 7️⃣ Cluster Definition

A **cluster** $C \subseteq \mathbb{R}^d$ satisfies:

- **Maximality**: If $\mathbf{x}_i \in C$ and $\mathbf{x}_j$ is density-reachable from $\mathbf{x}_i$, then $\mathbf{x}_j \in C$
- **Connectivity**: For any $\mathbf{x}_i, \mathbf{x}_j \in C $, $\mathbf{x}_i$ and $\mathbf{x}_j$ are density-connected

📌 **Intuition**: Clusters are maximal sets of mutually connected points based on density, not distance to a centroid.

---

## 8️⃣ Noise Points

Any point that is **not density-reachable** from any core point is labeled as **noise** or **an outlier**.

$\mathbf{x}_i\notin\bigcup_{k} C_k\Rightarrow\text{Noise}$

📌 **Intuition**: These are isolated points or lie in regions with density below the threshold.

---

## 🧭 Summary of Mathematical Flow

1. Use a distance function to define ε-neighborhoods.
2. Identify **core points** with ≥ `minPts` neighbors.
3. Define **direct density reachability** from core points.
4. Link reachability to form **density-connected clusters**.
5. Assign non-reachable points as **noise**.

---

## 🧪 Choosing ε and minPts

- **ε** can be chosen using a **k-distance graph**:
  - For each point, calculate the distance to its `k-th` nearest neighbor (usually `k = minPts - 1`).
  - Plot these distances in ascending order.
  - Look for the “elbow” point in the curve; this is a good estimate for `ε`.

- **minPts** is usually set to:

  $\text{minPts} \geq D + 1$

  where `D` is the number of dimensions.

---

## 📊 Visual Example
![Dendrogram](https://upload.wikimedia.org/wikipedia/commons/thumb/a/af/DBSCAN-Illustration.svg/1280px-DBSCAN-Illustration.svg.png)

DBSCAN groups dense regions and ignores noise.

---

## 🔍 Advantages of DBSCAN

✅ Can discover clusters of **arbitrary shape**  
✅ **Robust to outliers** (automatically labels them)  
✅ Does **not require** the number of clusters to be specified  
✅ Well-suited for **spatial data** or data with non-linear boundaries  

---

## ⚠️ Limitations

❌ Struggles when clusters have **varying density**  
❌ Requires careful tuning of `ε` and `minPts`  
❌ Not ideal for **high-dimensional data** (curse of dimensionality)

---

## 🧾 Summary

DBSCAN (Density-Based Spatial Clustering of Applications with Noise) is a powerful unsupervised learning algorithm that defines clusters as areas of high point density, separated by areas of lower density. Unlike traditional methods like K-Means, DBSCAN does not require the number of clusters to be specified in advance and can find clusters of arbitrary shape.

The algorithm relies on two key parameters: `ε` (epsilon), which defines the neighborhood radius, and `minPts`, which sets the minimum number of points required to form a dense region. Based on these parameters, DBSCAN classifies each point as a **core point**, **border point**, or **noise point** (outlier).

DBSCAN's clustering process is built around the concepts of **density reachability** and **density connectivity**. Clusters are formed by linking together core points and their reachable neighbors, while points in low-density regions are treated as noise.

Its strengths lie in its robustness to outliers and flexibility in detecting non-linear and irregular cluster shapes. However, it can be sensitive to the choice of parameters, and its performance may degrade in high-dimensional spaces or with clusters of varying densities.

In practice, DBSCAN is widely used in geospatial analysis, anomaly detection, and any scenario where traditional clustering fails to capture the true structure of the data.


## 📓 Next Step: Hands-On with Hierarchical clustering

Now that you've explored the mathematical foundation of DBSCAN, it's time to **see it in action**! [here](/notebooks/02_Unsupervised_Learning/01_Clustering/03_DBSCAN.ipynb)!

