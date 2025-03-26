# 🔗 Apriori Algorithm – Association Rule Mining

## 📌 What is the Apriori Algorithm?

The **Apriori algorithm** is a fundamental method used in **Association Rule Mining**, particularly useful in *market basket analysis*. It helps identify frequent itemsets (collections of items) and derive association rules that highlight relationships between items in large datasets.

🛒 **Example**:  
If many customers who buy *bread* and *butter* also buy *jam*, an association rule might be:

{Bread, Butter} ⇒ {Jam}

This rule implies a relationship among the items based on their co-occurrence.

---

## 📚 Key Concepts

### 1️⃣ **Itemset**
A collection of one or more items (e.g., {Milk}, {Milk, Bread}, {Butter, Eggs}).

### 2️⃣ **Support**
Indicates how frequently an itemset appears in the dataset.

$\text{Support}(A) = \frac{\text{Number of transactions containing } A}{\text{Total number of transactions}}$

🧠 *Intuition*: High support means the itemset is commonly bought together.

---

### 3️⃣ **Confidence**
Measures the reliability of the inference made by a rule.

$\text{Confidence}(A \Rightarrow B) = \frac{\text{Support}(A \cup B)}{\text{Support}(A)}$

🧠 *Intuition*: Given that A is bought, how likely is B also bought?

---

### 4️⃣ **Lift**
Evaluates the importance of a rule, by comparing observed co-occurrence to independence.

$\text{Lift}(A \Rightarrow B) = \frac{\text{Confidence}(A \Rightarrow B)}{\text{Support}(B)}$

🧠 *Intuition*:  
- Lift > 1: Positive association  
- Lift = 1: No association (independent)  
- Lift < 1: Negative association

---

## ⚙️ How the Apriori Algorithm Works

The Apriori algorithm operates in two main stages:

### 🔍 Step 1: Find Frequent Itemsets
- Start with individual items and calculate their support.
- Eliminate items below a **minimum support threshold**.
- Generate new itemsets by joining previously found frequent itemsets.
- Repeat until no more frequent itemsets can be generated.

⏳ This process uses the **Apriori Property**:  
> *All non-empty subsets of a frequent itemset must also be frequent.*

This property helps prune the search space and avoid unnecessary calculations.

---

### 🧮 Example of Support Calculation

Given 5 transactions:

| Transaction ID | Items Bought          |
|----------------|------------------------|
| T1             | Milk, Bread            |
| T2             | Milk, Bread, Butter    |
| T3             | Bread, Butter          |
| T4             | Milk, Bread, Butter    |
| T5             | Milk, Butter           |

Support of {Milk, Butter}:

$\text{Support}(\{Milk, Butter\}) = \frac{3}{5} = 0.6$

---

### 🧠 Step 2: Generate Association Rules

From the frequent itemsets, generate all possible **association rules** and compute **confidence** and **lift**.

Example rule:  

{Milk, Bread} ⇒ {Butter}


- Support = 0.4  
- Confidence = Support({Milk, Bread, Butter}) / Support({Milk, Bread})  
- Lift = Confidence / Support({Butter})

Rules are filtered by **minimum confidence** and **minimum lift** thresholds.

---

## 💡 Intuition Behind the Algorithm

- The Apriori algorithm is **bottom-up**: it starts with single items and expands them.
- By leveraging the **Apriori property**, it avoids testing itemsets that cannot possibly be frequent.
- It balances **exploration** (finding combinations) and **efficiency** (eliminating low-support sets early).

---

## ⚠️ Limitations

- **Computationally expensive**: Can be slow on large datasets due to candidate generation.
- **High memory usage**: Stores many itemsets in memory.
- **Requires setting thresholds**: Choosing good minimum support and confidence values is critical.

---

## ✅ Advantages

- Simple and interpretable.
- Effective for **market basket analysis** and rule discovery.
- Can be optimized with techniques like **hash-based counting** and **transaction reduction**.

---

## 📦 Use Cases

- Retail: Product placement & recommendations  
- Healthcare: Symptom co-occurrence patterns  
- Web Usage Mining: Page visit sequences  
- Finance: Co-occurring transactions or fraud patterns  

---

## 🏁 Summary
The Apriori algorithm is a foundational tool in unsupervised learning for discovering item associations in transactional datasets. By using support, confidence, and lift, it helps businesses and analysts uncover meaningful relationships and patterns in large-scale data.