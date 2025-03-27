# 📘 FP-Growth Algorithm

## 🧠 What is FP-Growth?

FP-Growth (Frequent Pattern Growth) is an efficient and scalable algorithm for **mining frequent itemsets** from transactional databases, which can be used to generate **association rules**. It is an alternative to the Apriori algorithm, but unlike Apriori, it avoids the costly candidate generation step by using a compact data structure called the **FP-tree (Frequent Pattern Tree)**.

---

## 🧩 Why Use FP-Growth?

- 🚀 **Faster** than Apriori, especially on large datasets.
- 📦 **Compact representation** of data via FP-tree.
- 🔄 **Avoids candidate generation**, which is expensive in Apriori.

---

## 📚 Problem Definition

Given:
- A set of transactions $T = \{ t_1, t_2, \ldots, t_n \}$, where each transaction $t_i$ is a set of items.
- A **minimum support threshold** $\sigma$

Goal:
- Find all **frequent itemsets** $X \subseteq I$ such that:

$\text{support}(X) = \frac{|\{ t_i \in T \mid X \subseteq t_i \}|}{|T|} \geq \sigma$

Where:
- $\text{support}(X)$: The proportion of transactions that contain the itemset $X$.
- $\sigma$: The user-defined minimum support threshold.

---

## 🌲 FP-Tree Construction: Step-by-Step

The FP-Growth algorithm builds a **tree-based structure** to efficiently represent and explore frequent itemsets.

### Step 1: Count Item Frequencies
Scan the database once to calculate the frequency of each item. Discard items with support below $\sigma$.

### Step 2: Build the FP-Tree
1. Sort items in each transaction in **descending order of frequency**.
2. Insert each transaction into the tree:
   - Shared prefixes result in branch merging.
   - Maintain a **header table** that links occurrences of each item.

### Example:

Suppose the following transactions and $\sigma = 3$:

| Transaction ID | Items           |
|----------------|------------------|
| T1             | A, B, D          |
| T2             | B, C, E          |
| T3             | A, B, C, E       |
| T4             | B, E             |
| T5             | A, B, C, E       |

After filtering and sorting by frequency, insert into the FP-tree.

---

## 🔄 FP-Growth Algorithm: Mining Frequent Itemsets

Once the FP-tree is built:

1. Start from the **least frequent item** in the header table.
2. For each item:
   - Extract its **conditional pattern base** (prefix paths leading to the item).
   - Build a **conditional FP-tree** from that base.
   - Recursively mine the conditional tree to extract patterns.

This recursive process finds all frequent itemsets that include the current item.

---

## 🧮 Mathematical Intuition

Let’s define some notation:

- Let $\mathcal{I}$ be the set of all items.
- Let $\mathcal{T}$ be the set of all transactions.
- Let $\sigma$ be the minimum support.

A frequent itemset $X \subseteq \mathcal{I}$ is one such that:

$\text{support}(X) = \frac{|\{ t \in \mathcal{T} \mid X \subseteq t \}|}{|\mathcal{T}|} \geq \sigma$

The FP-Growth algorithm mines all such $X$ by:
- Decomposing the support counts using prefix paths (conditional pattern bases).
- Avoiding enumeration of all $2^{|\mathcal{I}|}$ possible itemsets.
- Exploiting the **downward closure property**:  
  If $X$ is frequent, all subsets of $X$ are also frequent.

---

## ⚖️ FP-Growth vs Apriori

| Feature                 | Apriori               | FP-Growth              |
|------------------------|-----------------------|------------------------|
| Candidate generation   | ✅ Yes                | ❌ No                  |
| Database scans         | 🔁 Multiple           | ✅ 2 only              |
| Data structure         | None (Flat)           | FP-Tree                |
| Memory usage           | High with large itemsets | Lower with compression |
| Speed on large data    | ⛔ Slower             | 🚀 Faster              |

---

## ✅ Advantages

- Highly efficient for large datasets with long frequent patterns.
- Requires fewer database scans.
- Uses a compressed data structure (FP-tree).

---

## ⚠️ Limitations

- FP-tree may still become large for dense datasets.
- Requires enough memory to store the tree and conditional trees.

---

## 🔗 Use Cases

- Market Basket Analysis 🛒  
- Recommender Systems 🎯  
- Web Usage Mining 🌐  
- Intrusion Detection 🛡️

---

## 📌 Summary

The FP-Growth algorithm is a powerful and efficient method for mining frequent itemsets without generating candidate sets. Its use of a compact FP-tree structure enables it to handle large-scale datasets better than Apriori. By understanding the recursive pattern-growth strategy, one can uncover valuable associations in transactional data.

## 📓 Next Step: Hands-On with FPGrowth

Now that you've explored the mathematical foundation of FPGrowth, it's time to **see it in action**! [here](/notebooks/02_Unsupervised_Learning/03_Association_Rules/01_FPGrowth.ipynb)!

