# 📘 Supervised Learning

## 🧠 What is Supervised Learning?

Supervised Learning is one of the most fundamental approaches in machine learning. In this paradigm, we train models using **labeled datasets**, where each example consists of an input and a known output (label). The objective is to learn a function that maps inputs to outputs and generalizes well to unseen data.

This section is the **first chapter of the repository** and provides a thorough exploration of supervised learning models, grouped by algorithmic family. It covers both theoretical and practical aspects of each model, along with Python notebooks and usage examples.

---

## 📁 docs/01_Supervised_Learning/

├── [Introduction.md](docs/01_Supervised_Learning/Introduction.md) – 📘 *Introduction to Supervised Learning*

---

### 📂 01_Regression/
- [01_Linear_Regression.md](docs/01_Supervised_Learning/01_Regression/01_Linear_Regression.md) – Linear Regression  
- [02_Polynomial_Regression.md](docs/01_Supervised_Learning/01_Regression/02_Polynomial_Regression.md) – Polynomial Regression  
- [03_Logistic_Regression.md](docs/01_Supervised_Learning/01_Regression/03_Logistic_Regression.md) – Logistic Regression  

---

### 📂 02_Tree_Based_Models/
- [01_Decision_Trees.md](docs/01_Supervised_Learning/02_Tree_Based_Models/01_Decision_Trees.md) – Decision Trees  
- [02_Random_Forest.md](docs/01_Supervised_Learning/02_Tree_Based_Models/02_Random_Forest.md) – Random Forest  
- [03_Gradient_Boosting.md](docs/01_Supervised_Learning/02_Tree_Based_Models/03_Gradient_Boosting.md) – Gradient Boosting  

---

### 📂 03_Probability_Based_Models/
- [01_Naive_Bayes.md](docs/01_Supervised_Learning/03_Probability_Based_Models/01_Naive_Bayes.md) – Naive Bayes  
- [02_LDA.md](docs/01_Supervised_Learning/03_Probability_Based_Models/02_LDA.md) – Linear Discriminant Analysis (LDA)  

---

### 📂 04_Distance_Based_Models/
- [01_KNN.md](docs/01_Supervised_Learning/04_Distance_Based_Models/01_KNN.md) – k-Nearest Neighbors  
- [02_SVM.md](docs/01_Supervised_Learning/04_Distance_Based_Models/02_SVM.md) – Support Vector Machines  

---

### 📂 05_Neural_Networks/
- [01_Perceptron.md](docs/01_Supervised_Learning/05_Neural_Networks/01_Perceptron.md) – Simple Perceptron  
- [02_ML.md](docs/01_Supervised_Learning/05_Neural_Networks/02_ML.md) – Multilayer Perceptron (MLP)  

---

### 📂 06_Model_Evaluation/
- [01_Evaluation_Metrics.md](docs/01_Supervised_Learning/06_Model_Evaluation/01_Evaluation_Metrics.md) – Evaluation Metrics  
- [02_Cross_Validation.md](docs/01_Supervised_Learning/06_Model_Evaluation/02_Cross_Validation.md) – Cross-Validation  
- [03_Regularization.md](docs/01_Supervised_Learning/06_Model_Evaluation/03_Regularization.md) – Regularization  
- [04_Hyperparameter_Tuning.md](docs/01_Supervised_Learning/06_Model_Evaluation/04_Hyperparameter_Tuning.md) – Hyperparameter Tuning  

---


## ✅ Closing This Chapter

This concludes the **Supervised Learning** section of the repository.

You now have a solid foundation on:
- The most important classical ML models
- How to evaluate and improve them
- When and why to use each approach

👉 Next up: **Unsupervised Learning** — where no labels are required, and structure must be discovered from raw data.

# 📘 Unsupervised Learning

## 🧠 What is Unsupervised Learning?

Unsupervised Learning is a core paradigm of machine learning where models are trained **without labeled data**. Instead of learning from known outputs, these algorithms seek to identify **inherent patterns, groupings, or structures** within the data.

This section is the **second chapter of the repository** and focuses on the theory and application of unsupervised methods. It covers a wide range of techniques, from clustering and dimensionality reduction to anomaly detection and association rule mining, along with detailed explanations, mathematical formulations, and use cases.

---

## 📁 docs/02_Unsupervised_Learning/

├── [Introduction.md](docs/02_Unsupervised_Learning/Introduction.md) – 📘 *Introduction to Unsupervised Learning*

---

### 📂 01_Clustering/
- [01_KMeans.md](docs/02_Unsupervised_Learning/01_Clustering/01_KMeans.md) – K-Means Clustering  
- [02_Hierarchical.md](docs/02_Unsupervised_Learning/01_Clustering/02_Hierarchical_Clustering.md) – Hierarchical Clustering  
- [03_DBSCAN.md](docs/02_Unsupervised_Learning/01_Clustering/03_DBSCAN.md) – DBSCAN  

---

### 📂 02_Dimensionality_Reduction/
- [01_PCA.md](docs/02_Unsupervised_Learning/02_Dimensionality_Reduction/01_PCA.md) – Principal Component Analysis (PCA)  
- [02_tSNE.md](docs/02_Unsupervised_Learning/02_Dimensionality_Reduction/02_tSNE.md) – t-SNE  

---

### 📂 03_Association_Rules/
- [01_Apriori.md](docs/02_Unsupervised_Learning/03_Association_Rules/01_Apriori.md) – Apriori Algorithm  
- [02_FPGrowth.md](docs/02_Unsupervised_Learning/03_Association_Rules/02_FPGrowth.md) – FP-Growth Algorithm  

---

### 📂 04_Anomaly_Detection/
- [01_Isolation_Forest.md](docs/02_Unsupervised_Learning/04_Anomaly_Detection/01_Isolation_Forest.md) – Isolation Forest  
- [02_OneClass_SVM.md](docs/02_Unsupervised_Learning/04_Anomaly_Detection/02_OneClass_SVM.md) – One-Class SVM  

---

### 📂 05_Model_Evaluation/
- [01_Evaluation_Metrics.md](docs/02_Unsupervised_Learning/05_Model_Evaluation/01_Evaluation_Metrics.md) – Evaluation Metrics  

---

## ✅ Closing This Chapter

This concludes the **Unsupervised Learning** section of the repository.

You now have a comprehensive understanding of:
- How to uncover hidden patterns in unlabeled data
- Core techniques like clustering, dimensionality reduction, and anomaly detection
- How to evaluate unsupervised models without relying on labeled outcomes
