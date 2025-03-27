# 🌲 Isolation Forest for Anomaly Detection

## 🧠 Intuition

**Isolation Forest** is an ensemble-based anomaly detection algorithm that isolates anomalies instead of profiling normal data points.

The core idea is simple:  
> Anomalies are rare and different — they are more likely to be isolated from the rest of the data in fewer random splits.

This approach builds on the assumption that:
- Normal points are usually surrounded by other points and require more partitions to be isolated.
- Anomalies are few and lie far from dense clusters, so they are isolated quickly.

---

## 🧪 How It Works

Isolation Forest works by constructing multiple **binary trees** called *isolation trees* (`iTrees`). These trees are built by randomly selecting:
- A feature,
- A split value between the minimum and maximum value of that feature.

This process recursively partitions the data until:
- A point is isolated (i.e., it's alone in a partition),
- Or a maximum tree height is reached.

### 🏗️ Building an Isolation Tree

For a given sample $x$:

1. Randomly select a feature $f$.
2. Randomly select a split value $s$ in the range of values for $f$.
3. Partition the data:
   - Left if $x[f] < s$
   - Right otherwise
4. Repeat until:
   - The sample is isolated,
   - Or the tree reaches a height limit.

---

## 📏 Anomaly Score

The number of splits required to isolate a point is called the **path length** $h(x)$. Shorter paths indicate higher chances of being an anomaly.

To convert this into an **anomaly score**, we compute the average path length over all trees and normalize it using:

### 📐 Expected Path Length
For a dataset with $n$ instances, the average path length of an unsuccessful search in a Binary Search Tree (BST) is:

$c(n) = 2H(n - 1) - \frac{2(n - 1)}{n}$

Where $H(i)$ is the harmonic number:

$H(i) \approx \ln(i) + \gamma \quad (\text{Euler-Mascheroni constant } \gamma \approx 0.5772)$

---

### 🧮 Anomaly Score Formula

Let $h(x)$ be the average path length for data point $x$, and $c(n)$ the average path length for data size $n$:

$s(x, n) = 2^{-\frac{h(x)}{c(n)}}$

Where:
- $s(x, n) \in (0, 1)$ is the anomaly score.
- Scores close to 1 → likely anomaly.
- Scores close to 0.5 → normal.
- Thresholds like 0.7–0.8 are commonly used to flag outliers.

---

## ⚙️ Algorithm Steps

1. Subsample the data (typically ~256 points).
2. Build multiple isolation trees on different subsamples.
3. For each point, compute the average path length across all trees.
4. Convert to anomaly score using the formula above.
5. Classify points based on score threshold.

---

## 🔍 Advantages

✅ Efficient for high-dimensional datasets.  
✅ Works well without assumptions about data distribution.  
✅ Handles large datasets using subsampling.  
✅ Linear time complexity $\mathcal{O}(n \log n)$.  
✅ Few hyperparameters to tune.

---

## ⚠️ Limitations

❌ Sensitive to contamination parameter (expected proportion of anomalies).  
❌ May underperform when anomalies are not well-isolated.

---
📈 Visualization

Anomaly points are isolated early in the random partitioning process.
![Anomaly](https://upload.wikimedia.org/wikipedia/commons/c/ce/Isolating_a_Non-Anomalous_Point.png)

---
## 🏁 Summary
Isolation Forest is a powerful, scalable, and intuitive algorithm for anomaly detection. It operates by isolating points using random partitions and uses path lengths as a measure of normality. Shorter paths indicate potential outliers.

---
## 📓 Next Step: Hands-On with Isolation Forest

Now that you've explored the mathematical foundation of Isolation Forest, it's time to **see it in action**! [here](/notebooks/02_Unsupervised_Learning/04_Anomaly_Detection/01_Isolation_Forest.ipynb)!