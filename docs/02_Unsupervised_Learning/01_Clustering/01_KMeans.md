# 📌 K-Means Clustering

## 📖 What is K-Means?

K-Means is one of the most popular **unsupervised learning algorithms** used for **clustering**. It aims to partition a dataset into `K` distinct, non-overlapping groups (clusters), where each data point belongs to the cluster with the **nearest mean (centroid)**.

The goal is to **minimize intra-cluster distance** and **maximize inter-cluster distance**.

---

## 🧠 Intuition

Imagine having a collection of data points scattered across a 2D space. K-Means tries to:

- Place `K` centroids (means) randomly.
- Assign each data point to its closest centroid.
- Recalculate centroids as the average of assigned points.
- Repeat until convergence.

This process groups similar data points together based on their features.

---
## 🧮 Mathematical Formulation of K-Means Clustering (Step-by-Step)

K-Means is a centroid-based clustering algorithm that aims to partition data into \( K \) groups where each point belongs to the cluster with the closest centroid.

Let’s break down the **entire mathematical formulation** step-by-step, including how the algorithm initializes, assigns, updates, and converges.

---

### 📌 Problem Setup

Let:
- $X = \{x_1, x_2, ..., x_n\}$, where each $x_i \in \mathbb{R}^d$, be the dataset of $n$ points in $d$-dimensional space.
- $K$: the number of clusters (user-defined).
- $\mu_1, \mu_2, ..., \mu_K \in \mathbb{R}^d$: the centroids of the clusters.
- $c_i \in \{1, ..., K\}$: the cluster assignment for point $x_i$.

---

### 🔁 Step-by-Step K-Means Algorithm

### Step 1: Initialization of Centroids

We randomly initialize $K$ centroids $\mu_1, \mu_2, ..., \mu_K$ by choosing **K points randomly from the dataset**:

$\mu_k^{(0)} \in \{x_1, x_2, ..., x_n\} \quad \text{for } k = 1, ..., K$

#### 💡 Intuition:
This gives us a starting point for each cluster. The randomness means different runs may give different results. A better method is **K-Means++**, which spreads out initial centroids more intelligently (more on that later).

---

### Step 2: Cluster Assignment (Expectation Step)

For each point $x_i$, assign it to the closest centroid based on **squared Euclidean distance**:

$c_i = \arg\min_{k \in \{1,...,K\}} \| x_i - \mu_k \|^2$

This step partitions the space into **Voronoi regions**, where each region belongs to one cluster.

#### 💡 Intuition:
A point “belongs” to the cluster whose centroid is **geometrically closest**. We're essentially labeling points with cluster IDs.

---

### Step 3: Centroid Update (Minimization Step)

Once all points are assigned to clusters, recompute each centroid as the **mean of all points** assigned to it:

$\mu_k = \frac{1}{|C_k|} \sum_{x_i \in C_k} x_i$

Where:
- $C_k = \{x_i \mid c_i = k\}$ is the set of points assigned to cluster $k$,
- $|C_k|$ is the number of points in that cluster.

#### 💡 Intuition:
We “pull” the centroid to the **center of mass** of its current members. This helps the centroid better represent its cluster.

---

### Step 4: Repeat Until Convergence

Repeat **Steps 2 and 3** until convergence. The stopping criteria can be:

1. **No change in assignments**: $c_i^{(t+1)} = c_i^{(t)}$ for all $i$,
2. **Centroids stop moving significantly**:$\| \mu_k^{(t+1)} - \mu_k^{(t)} \| < \epsilon$,
3. **Max iterations reached**: Typically set to a reasonable constant like 300.

---

### 🎯 Objective Function

K-Means implicitly minimizes the following **cost function** (within-cluster sum of squares):

$J = \sum_{k=1}^{K} \sum_{x_i \in C_k} \| x_i - \mu_k \|^2$

Each iteration of the algorithm **does not increase** this cost. Since the number of partitions is finite and the cost decreases or stays constant, the algorithm **guarantees convergence** (though not necessarily to the global minimum).

#### 💡 Intuition:
We're trying to make clusters **tight** (low variance), so that members of a cluster are as close as possible to their centroid.

---

## 📌 Notes on Initialization (K-Means++)

Random initialization can lead to poor results (bad local minima). **K-Means++** improves this by spreading out the initial centroids:

1. Choose the first centroid randomly from the data.
2. For each data point \( x \), compute its distance \( D(x) \) to the nearest chosen centroid.
3. Choose the next centroid with probability proportional to \( D(x)^2 \).
4. Repeat until \( K \) centroids are chosen.

This often yields **better convergence and lower final cost**.

---

## 📌 Summary Table

| Step              | Formula                                                                 | Description                                     |
|-------------------|-------------------------------------------------------------------------|-------------------------------------------------|
| Initialization    | $\mu_k \leftarrow \text{random sample from } X $                     | Pick K initial centroids from the data          |
| Assignment        | $c_i = \arg\min_k \|x_i - \mu_k\|^2 $                         | Assign point to nearest centroid                |
| Update            | $\mu_k = \frac{1}{C_k} \sum_{x_i \in C_k} x_i$                   | Recompute centroid as mean of its cluster       |
| Objective         | $J = \sum_{k=1}^{K} \sum_{x_i \in C_k} \|x_i - \mu_k\|^2$            | Total intra-cluster variance to minimize        |

---

> ✅ K-Means is simple, elegant, and fast. But its power lies in the clear geometric interpretation of minimizing variance through centroid updates. Each mathematical step has a clean and intuitive purpose.


---

## 📊 Visualization

![KMeans Animation](https://upload.wikimedia.org/wikipedia/commons/e/ea/K-means_convergence.gif)  
*K-Means iteratively refines cluster boundaries and centroid positions.*

---

## ⚙️ Hyperparameters

- **K (number of clusters)**: The most critical parameter.
  - Use the **Elbow Method** or **Silhouette Score** to choose the optimal \( K \).
  
---

## 📎 Pros and Cons

### ✅ Advantages:
- Simple and easy to implement.
- Scales well with large datasets.
- Efficient in practice (linear complexity).

### ❌ Disadvantages:
- Must choose $K$  in advance.
- Sensitive to initial centroids (use **K-Means++** for better initialization).
- Assumes spherical clusters of similar size.
- Can get stuck in local minima.

---

## 🛠️ Practical Tips

- **Standardize your features** before applying K-Means.
- **Run the algorithm multiple times** with different initializations.
- Try **KMeans++** for smarter centroid initialization.
- Consider **MiniBatchKMeans** for large datasets.

---

## ✅ Conclusion

K-Means is a powerful yet simple unsupervised learning algorithm that partitions data into clusters by minimizing the intra-cluster variance. Its strength lies in its clear geometric interpretation and computational efficiency.

Despite its assumptions (e.g., spherical clusters, sensitivity to initialization), K-Means remains widely used in practice due to its interpretability and scalability.

Understanding the mathematical foundation behind each step — initialization, assignment, update, and convergence — is essential to apply K-Means effectively and diagnose potential issues in real-world datasets.

---

## 📓 Next Step: Hands-On with K-Means

Now that you've explored the mathematical foundation of K-Means, it's time to **see it in action**! [here](/notebooks/02_Unsupervised_Learning/01_Clustering/01_KMeans.ipynb)!


