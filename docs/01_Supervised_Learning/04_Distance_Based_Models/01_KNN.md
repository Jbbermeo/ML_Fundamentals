# 📘 k-Nearest Neighbors (k-NN)

## 📌 Introduction
k-Nearest Neighbors (k-NN) is a **supervised learning algorithm** used for **classification and regression**. It is a **non-parametric, instance-based** method that classifies a data point based on the majority class of its **k nearest neighbors**.

### 🔹 Why Use k-NN?
- **Simple and intuitive** – No need for complex mathematical models.
- **No training phase** – It stores all training data and makes predictions on the fly.
- **Works well for multi-class classification**.
- **Can handle both classification and regression tasks**.

---

## 📐 How k-NN Works
### **1️⃣ Choose the Value of k**
- The **number of neighbors (k)** determines how many nearby points will influence classification.
- **Low $( k )$ (e.g., 1 or 3):** More sensitive to noise.
- **High $( k )$ (e.g., 10 or 20):** More stable but might smooth decision boundaries too much.

### **2️⃣ Compute the Distance to All Points**
- The distance between the new data point and all training points is computed using a metric like:
  - **Euclidean Distance** (most common):

    $d(A, B) = \sqrt{\sum_{i=1}^{n} (A_i - B_i)^2}$

  - **Manhattan Distance**:

    $d(A, B) = \sum_{i=1}^{n} |A_i - B_i|$

  - **Minkowski Distance** (generalization of Euclidean and Manhattan):

    $d(A, B) = \left(\sum_{i=1}^{n} |A_i - B_i|^p \right)^{1/p}$

  - **Cosine Similarity** (useful for text classification).

### **3️⃣ Identify the k Nearest Neighbors**
- Sort all training points by distance and select the **k closest ones**.

### **4️⃣ Assign the Class (for Classification)**
- Use **majority voting**: The most common class among the neighbors is assigned to the new point.

### **5️⃣ Compute the Average (for Regression)**
- The predicted value is the **mean or median** of the nearest neighbors.

---

## 🔢 Choosing the Best k
While building the kNN classifier model, one question that come to my mind is what should be the value of nearest neighbours (k) that yields highest accuracy. This is a very important question because the classification accuracy depends upon our choice of k.

The number of neighbours (k) in kNN is a parameter that we need to select at the time of model building. Selecting the optimal value of k in kNN is the most critical problem. A small value of k means that noise will have higher influence on the result. So, probability of overfitting is very high. A large value of k makes it computationally expensive in terms of time to build the kNN model. Also, a large value of k will have a smoother decision boundary which means lower variance but higher bias.

The data scientists choose an odd value of k if the number of classes is even. We can apply the elbow method to select the value of k. To optimize the results, we can use Cross Validation technique. Using the cross-validation technique, we can test the kNN algorithm with different values of k. The model which gives good accuracy can be considered to be an optimal choice. It depends on individual cases and at times best process is to run through each possible value of k and test our result.

### **The Elbow Method**
The **Elbow Method** is a technique used to determine the best value of $( k )$ by plotting the **error rate** or **classification accuracy** against different values of $( k )$. The point where the error stops decreasing significantly (forming an "elbow" shape) is the best choice for $( k )$.

#### **Steps to Apply the Elbow Method:**
1️⃣ Train k-NN with different values of $( k )$ (e.g., from 1 to 20).  
2️⃣ Calculate the error rate or accuracy for each $( k )$.  
3️⃣ Plot $( k )$ vs. error rate.  
4️⃣ Choose $( k )$ at the "elbow" where the error stabilizes.


---

## 📊 k-NN vs. Other Models
| Feature        | k-NN  | Decision Tree | SVM   |
|---------------|------|--------------|------|
| Training Speed | Fast | Fast         | Slow |
| Prediction Speed | Slow | Fast        | Medium |
| Works with Non-Linear Data | Yes | Yes | Yes |
| Handles Noise Well | No  | Yes | Yes |
| Works Well with High-Dimensional Data | No  | Yes | Yes |

---

## 🏗️ Advantages and Disadvantages
✅ **Advantages**
- **Simple to understand and implement**.
- **No training required** – Stores all data and classifies on demand.
- **Can model complex decision boundaries.**

⚠️ **Disadvantages**
- **Slow prediction speed** – Must compute distances for every new prediction.
- **Sensitive to irrelevant features and feature scaling**.
- **Not efficient for high-dimensional data** – Suffering from the **curse of dimensionality**.

---

## 📌 Conclusion
k-NN is a powerful, **non-parametric model** that works well for **small datasets** and **classification problems**. However, it **scales poorly** with large datasets due to its high computational cost during prediction.

👉 **Next Steps:** Implement k-NN in Python [here](/notebooks/01_Supervised_Learning/04_Distance_Based_Models/01_KNN.ipynb)!





