# 🧠 t-SNE (t-distributed Stochastic Neighbor Embedding)

## 📌 What is t-SNE?

t-SNE (t-distributed Stochastic Neighbor Embedding) is a **non-linear dimensionality reduction technique** especially well-suited for **visualizing high-dimensional data in 2 or 3 dimensions**. It preserves the **local structure** of the data, making it great for clustering and understanding patterns in datasets like word embeddings, image features, or genetic data.

It was introduced by **Laurens van der Maaten and Geoffrey Hinton** in 2008.

---

## 🎯 Goal

To map high-dimensional data to a lower-dimensional space (typically 2D or 3D) while preserving the **probability distribution of pairwise similarities** between data points.

---

## 🔍 Intuition

- Imagine data points in high dimensions forming clusters.
- t-SNE tries to place those same points in 2D/3D space such that **similar points stay close together** and **dissimilar points stay far apart**.
- It does this by modeling the **pairwise similarities** in both spaces as **probability distributions**, and **minimizing the divergence** between them.

---
## 📐 Mathematical Formulation of t-SNE

t-SNE is built upon a clever idea: if two points are similar in high-dimensional space, they should also be close in a low-dimensional embedding.

To achieve this, t-SNE constructs **two probability distributions**: one in the **original space** and another in the **embedding space**. Then it minimizes the **divergence** between them.

Let’s walk through the process step by step.

---

## Step 1: Modeling Similarity in High-Dimensional Space

Let $\mathbf{x}_1, \mathbf{x}_2, \dots, \mathbf{x}_n \in \mathbb{R}^D$ be your high-dimensional data points.

We define the similarity between points $\mathbf{x}_i$ and $\mathbf{x}_j$ using a **conditional probability** based on a Gaussian distribution centered at $\mathbf{x}_i$:

$p_{(j|i)} = \frac{\exp\left(-\frac{\|x_i - x_j\|^2}{2\sigma_i^2}\right)}{\sum_{k \neq i} \exp\left(-\frac{\|x_i - x_k\|^2}{2\sigma_i^2}\right)}$

🔍 **Intuition:**  
We treat nearby points as more "likely neighbors" under a Gaussian. Each point has its own bandwidth $\sigma_i$, adapted to preserve a constant neighborhood size.

---

### Perplexity and Bandwidth Selection

We choose $\sigma_i$ so that the **perplexity** of the distribution matches a target value:

$\text{Perplexity}(P_i) = 2^{H(P_i)} \quad \text{where } H(P_i) = -\sum_j p_{j|i} \log_2 (p_{j|i})$


🔍 **Intuition:**  
Perplexity acts like a smooth version of "number of neighbors". The algorithm tunes $\sigma_i$ using binary search to get this value.

---

## Step 2: Symmetric Joint Probabilities

To eliminate directional bias, we symmetrize the conditional probabilities:

$p_{ij} = \frac{p_{j|i} + p_{i|j}}{2n}$

🔍 **Intuition:**  
This gives a global, symmetric view of how similar each pair of points is. Think of it as: “What is the mutual similarity between $i$ and $j$ ?”

---

## Step 3: Similarity in Low-Dimensional Space

Let $\mathbf{y}_1, \dots, \mathbf{y}_n \in \mathbb{R}^d$ be the low-dimensional representations (typically $d = 2$ ).

We define the similarity between $\mathbf{y}_i$ and $\mathbf{y}_j$ using a **Student’s t-distribution** with 1 degree of freedom:

$q_{ij} = \frac{(1 + \|\mathbf{y}_i - \mathbf{y}_j\|^2)^{-1}}{\sum_{k \neq l} (1 + \|\mathbf{y}_k - \mathbf{y}_l\|^2)^{-1}}$

🔍 **Intuition:**  
The **heavy tails** of the t-distribution allow dissimilar points to be modeled far apart. This combats the "crowding problem", where high-dimensional points get compressed too tightly in 2D.

---

## Step 4: Aligning Distributions via KL Divergence

We now want the distribution $Q = \{q_{ij}\}$ in low-dimensions to match the high-dimensional similarity distribution $P = \{p_{ij}\}$.

This is done by minimizing the **Kullback-Leibler divergence**:

$\text{KL}(P \| Q) = \sum_{i \neq j} p_{ij} \log\left( \frac{p_{ij}}{q_{ij}} \right)$

🔍 **Intuition:**  
This loss penalizes large differences between $p_{ij}$ and $q_{ij}$. If two points are similar in high dimensions, but distant in low dimensions, the KL divergence will be large — and the optimizer will correct that.

---

## Step 5: Gradient Descent Optimization

The coordinates $\mathbf{y}_1, \dots, \mathbf{y}_n$ are initialized randomly and optimized using **gradient descent**.

The gradient of the KL divergence w.r.t. $\mathbf{y}_i$ is:

$\frac{\partial \text{KL}}{\partial \mathbf{y}_i} = 4 \sum_j (p_{ij} - q_{ij}) (1 + \|\mathbf{y}_i - \mathbf{y}_j\|^2)^{-1} (\mathbf{y}_i - \mathbf{y}_j)$

🔍 **Intuition:**  
This moves $\mathbf{y}_i$ closer to $\mathbf{y}_j$ when $p_{ij} > q_{ij}$ \), and pushes them apart when $p_{ij} < q_{ij}$.

---

## 🧭 Summary of the Process

1. Compute **pairwise similarities** $p_{ij}$ in high dimensions using Gaussian kernels.
2. Compute **similarities** $q_{ij}$ in low dimensions using a Student’s t-distribution.
3. **Minimize KL divergence** $\text{KL}(P \| Q)$ to align both distributions.
4. Optimize with **gradient descent**, updating the low-dimensional coordinates.

This elegant mechanism turns an abstract space into a meaningful 2D map — all without needing labels.

---

## 📈 Perplexity: Tuning the Neighborhood Size

The **perplexity** controls how many neighbors each point is compared to. It affects the shape of the neighborhood:

- Low perplexity → focus on local structure
- High perplexity → more global structure

Typical values range between **5 and 50**.

---

## 📊 Visual Example
![tSNE](https://upload.wikimedia.org/wikipedia/commons/thumb/f/f1/T-SNE_Embedding_of_MNIST.png/1280px-T-SNE_Embedding_of_MNIST.png)

---

## 🚀 Advantages

✅ Excellent for **visualization of high-dimensional data**  
✅ Captures **non-linear structures**  
✅ Handles **clusters and manifolds** well  
✅ **No assumptions** on linearity or feature importance

---

## ⚠️ Disadvantages

❌ **Computationally expensive** (O(n²) complexity)  
❌ **Non-deterministic** unless seed is fixed  
❌ **Not suitable for general-purpose dimensionality reduction**  
❌ Can **distort global relationships** (focuses on local structure)

---

## 🧪 Example Use Cases

- Visualizing **word embeddings** (e.g., Word2Vec, GloVe)
- Understanding **clusters** in image recognition or genomics
- Inspecting the **structure of high-dimensional neural network activations**
- Reducing noise before applying clustering algorithms

---

## 🧰 Practical Tips

- Always **standardize or normalize** your data before applying t-SNE.
- Try different values of **perplexity** (start with 30).
- Use **PCA as a preprocessing step** to reduce dimensions to ~50 before t-SNE.
- Run multiple times with different seeds to ensure stability.

---

## 🏁 Summary

t-SNE is a non-linear dimensionality reduction technique used mainly for visualizing high-dimensional data in 2D or 3D. It preserves local structure by converting distances into probabilities and minimizing the KL divergence between high- and low-dimensional distributions. Using a Gaussian in the original space and a Student's t-distribution in the embedding, t-SNE captures clusters and neighborhood relationships effectively. The perplexity parameter controls the number of neighbors considered. While powerful for visualization, it's not ideal for preserving global distances or scaling to very large datasets

---
## 📓 Next Step: Hands-On with tSNE

Now that you've explored the mathematical foundation of tSNE, it's time to **see it in action**! [here](/notebooks/02_Unsupervised_Learning/02_DImensionality_Reduction/02_tSNE.ipynb)!