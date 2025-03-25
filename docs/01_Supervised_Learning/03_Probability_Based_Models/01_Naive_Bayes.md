# 📘 Naïve Bayes

## 📌 Introduction
Naïve Bayes is a **probabilistic classification algorithm** based on **Bayes' Theorem**. It is widely used for text classification, spam detection, and medical diagnosis due to its simplicity and efficiency.

### 🔹 Why Use Naïve Bayes?
- **Fast and scalable**, even with large datasets.
- **Performs well with categorical and text data**.
- **Handles missing data efficiently**.
- **Works well when features are independent (though this assumption is often violated in practice).**

---

## 📐 How Naïve Bayes Works
### 🔹 Bayes' Theorem
Naïve Bayes is based on **Bayes' Theorem**, which describes the probability of an event given prior knowledge:

$P(A | B) = \frac{P(B | A) P(A)}{P(B)}$

where:
- $( P(A | B) )$ is the **posterior probability** (probability of class given features).
- $( P(B | A) )$ is the **likelihood** (probability of features given class).
- $( P(A) )$ is the **prior probability** (probability of class before observing features).
- $( P(B) )$ is the **evidence** (probability of features overall).

### 🔹 Why "Naïve"?
The algorithm assumes that **features are conditionally independent given the class**:

$P(X_1, X_2, ..., X_n | C) = P(X_1 | C) P(X_2 | C) ... P(X_n | C)$

means that all **features are conditionally independent given the class C**, In other words, if we already know the class, the probability of a feature occurring does not depend on the other features. This assumption is called the naïve assumption and simplifies the computation of probabilities significantly. However, in real-world scenarios, it is often not true for the following reasons:

#### 🔹 Why is this assumption problematic?
1. Feature Correlation

- Many real-world datasets have correlated features. For example, in spam classification, the presence of the words “free” and “win” are highly correlated. However, Naïve Bayes treats them as independent.
- When features are correlated, the model can **double-count information**, leading to **biased probability estimates.**

2. Loss of Information.

- Since features are assumed independent, the algorithm does not capture interactions between them.
- For example, in medical diagnosis, symptoms often depend on one another. The presence of fever and cough together is more informative than each feature individually, but Naïve Bayes assumes they contribute separately.

3. Incorrect Probability Estimates

- The product of individual probabilities can become artificially small or large due to ignored dependencies.
This can make Naïve Bayes overconfident or underconfident in its predictions.

#### 🔹 When is it still useful?

Despite this unrealistic assumption, Naïve Bayes often works well in practice because:

- The decision boundary can still be good enough for classification, even if probability estimates are off.
- In text classification, where features (words) often appear independently in different documents, the assumption holds reasonably well.
- It is computationally efficient and performs well with high-dimensional data.


### 🔹 Classification Rule
The model predicts the class $( C )$ that maximizes the posterior probability:

$C^* = \arg\max_C P(C) \prod_{i=1}^{n} P(X_i | C)$

This means we select the class with the highest computed probability.

---

## 📊 Types of Naïve Bayes Classifiers

Naïve Bayes classifiers come in different variants depending on the type of data they handle. Each version adapts Bayes’ Theorem to suit different types of feature distributions. Understanding these types is crucial to applying Naïve Bayes effectively in real-world problems.

### 🔹 Why Different Types of Naïve Bayes?
- Features can be **continuous, categorical, binary, or frequency-based**, requiring different probability models.
- Choosing the right type **improves model performance** and ensures proper likelihood estimation.
- Some types perform better for **text data**, while others work well for **numerical or binary features**.

---

## 📐 1️⃣ Gaussian Naïve Bayes
### **🔹 What is it?**
- Assumes that **continuous features** follow a **Gaussian (Normal) distribution**.
- Instead of counting occurrences (like in categorical models), it models the likelihood of features using:

$P(X_i | C) = \frac{1}{\sqrt{2 \pi \sigma^2}} e^{-\frac{(X_i - \mu)^2}{2 \sigma^2}}$

- Where **$( \mu )$** is the mean and **$( \sigma^2 )$** is the variance of feature $( X_i )$ within class $( C )$.

### **🔹 When to Use It?**
✅ When features are **continuous** and approximately **normally distributed**.
✅ Works well for **medical diagnosis, fraud detection, and sensor data**.

### **🔹 Example Data**
| Sample | Feature: Temperature (°C) | Class (Disease Present: 1, Absent: 0) |
|--------|--------------------------|----------------------------------|
| 1      | 36.5                     | 0                                |
| 2      | 37.8                     | 1                                |
| 3      | 38.3                     | 1                                |
| 4      | 36.2                     | 0                                |
| 5      | 39.1                     | 1                                |


---

## 📐 2️⃣ Multinomial Naïve Bayes
### **🔹 What is it?**
- Designed for **categorical features** where each feature represents a **frequency count** (e.g., how many times a word appears in a document).
- The likelihood is computed using:

$P(X_i | C) = \frac{(N_i + \alpha)}{(N + \alpha \cdot k)}$

- Where:
  - $( N_i )$ = Count of feature $( X_i )$ in class $( C )$.
  - $( N )$ = Total count of all features in class $( C )$.
  - $( k )$ = Number of unique features.
  - $( \alpha )$ = Smoothing parameter (Laplace smoothing to avoid zero probabilities).

### **🔹 When to Use It?**
✅ **Text classification** (spam detection, topic modeling, sentiment analysis).
✅ **Document classification** where word frequencies matter.
✅ Works well with **word count features (Bag-of-Words or TF-IDF)**.

### **🔹 Example Data**
| Sample | Word: "Free" | Word: "Win" | Word: "Offer" | Class (Spam: 1, Not Spam: 0) |
|--------|------------|------------|-------------|--------------------------|
| 1      | 3          | 1          | 2           | 1                        |
| 2      | 0          | 0          | 0           | 0                        |
| 3      | 2          | 3          | 1           | 1                        |
| 4      | 0          | 1          | 0           | 0                        |

---

## 📐 3️⃣ Bernoulli Naïve Bayes
### **🔹 What is it?**
- Works with **binary features** (1 if a word appears, 0 if it doesn’t).
- The likelihood is modeled as:

$P(X_i | C) = P_i^{X_i} (1 - P_i)^{(1 - X_i)}$

- Where:
  - $( P_i )$ = Probability of feature $( X_i )$ occurring in class $( C )$.
  - $( X_i )$ is **1** if the feature is present, **0** if absent.

### **🔹 When to Use It?**
✅ **Binary text classification** (e.g., spam detection, document filtering).
✅ When presence/absence of words is more important than frequency.
✅ Suitable for **small text datasets** with sparse features.

### **🔹 Example Data**
| Sample | Word: "Free" | Word: "Win" | Word: "Offer" | Class (Spam: 1, Not Spam: 0) |
|--------|------------|------------|-------------|--------------------------|
| 1      | 1          | 1          | 1           | 1                        |
| 2      | 0          | 0          | 0           | 0                        |
| 3      | 1          | 1          | 0           | 1                        |
| 4      | 0          | 1          | 0           | 0                        |

---

## 📐 4️⃣ Complement Naïve Bayes
### **🔹 What is it?**
- A variation of Multinomial Naïve Bayes designed for **imbalanced datasets**.
- Instead of modeling $( P(X_i | C) )$, it models **$( P(X_i | \neg C) )$** (probability of feature occurring in other classes).
- Helps when the dataset is highly skewed (e.g., when spam emails are only 5% of the data).

### **🔹 When to Use It?**
✅ **Text classification on imbalanced datasets** (e.g., medical records, fraud detection).
✅ When Multinomial Naïve Bayes underperforms due to class imbalance.

### **🔹 Example Data**
| Sample | Word: "Free" | Word: "Win" | Word: "Offer" | Class (Spam: 1, Not Spam: 0) |
|--------|------------|------------|-------------|--------------------------|
| 1      | 4          | 1          | 3           | 1                        |
| 2      | 0          | 0          | 1           | 0                        |
| 3      | 1          | 5          | 2           | 1                        |
| 4      | 0          | 1          | 0           | 0                        |

---

## 🔥 **Choosing the Right Naïve Bayes Model**
| Type                | Feature Type           | Best Use Case                              |
|--------------------|----------------------|-------------------------------------------|
| **Gaussian NB**   | Continuous           | Medical diagnosis, fraud detection, sensors |
| **Multinomial NB** | Categorical (counts) | Spam filtering, text classification, NLP  |
| **Bernoulli NB**   | Binary (0/1)         | Document filtering, short-text classification |
| **Complement NB**  | Categorical (counts) | Imbalanced text classification, fraud detection |

---

Different variants of Naïve Bayes are suited for different types of data. Choosing the right one **ensures better classification performance** while maintaining the efficiency of Naïve Bayes models.

---

## 🏗️ Advantages and Disadvantages
✅ **Advantages**
- Extremely fast and efficient.
- Works well with high-dimensional data (text, categorical features).
- Requires small amounts of training data.

⚠️ **Disadvantages**
- Assumes **feature independence**, which is rarely true in real-world problems.
- Struggles with **correlated features**.
- **Poor performance with very small datasets**.

---

## 📌 Conclusion
Naïve Bayes is a simple yet powerful probabilistic classifier, particularly useful for **text classification** and **real-time predictions**. Despite its strong assumptions, it often performs well in practice.

👉 **Next Steps:** Implement Naïve Bayes in Python and compare its performance [here](/notebooks/01_Supervised_Learning/03_Probability_Based_Models/01_Naive_Bayes.ipynb)!