# 📘 Simple Perceptron

## 📌 Introduction
The **Perceptron** is one of the earliest and simplest types of artificial neural networks. It is a **linear binary classifier** that learns a **hyperplane** to separate two classes of data using a very intuitive learning algorithm.

Introduced by **Frank Rosenblatt** in 1958, the perceptron laid the groundwork for modern neural networks and deep learning. Although limited in what it can learn (only linearly separable problems), it remains a foundational concept in machine learning.

---

## 🧠 How the Perceptron Works
The perceptron is inspired by the functioning of a biological neuron. It receives multiple input signals, processes them, and emits a binary output (firing or not firing). Let’s break this down into its fundamental mathematical steps:

### 1️⃣ Inputs and Weights
We start with an input vector:

$\mathbf{x} = [x_1, x_2, ..., x_n]^T$

Each component $( x_i )$ is a feature (or signal). Associated with these inputs is a weight vector:

$\mathbf{w} = [w_1, w_2, ..., w_n]^T$

Each weight $( w_i )$ represents the strength or importance of the corresponding input feature.

There is also an additional parameter called the **bias** $( b )$, which shifts the decision boundary and allows the model to generalize beyond the origin.

### 2️⃣ Weighted Sum
The perceptron computes a **linear combination** (also called the net input):

$z = \mathbf{w}^T \mathbf{x} + b = \sum_{i=1}^n w_i x_i + b$

This value $( z )$ is a single scalar and represents how much evidence there is for the input belonging to the positive class.

### 3️⃣ Activation Function
The perceptron then applies a **step function** (also known as the Heaviside function):

$\hat{y} = \begin{cases} 1 & \text{if } z \geq 0 \\ 0 & \text{otherwise} \end{cases}$

This function outputs a binary prediction:
- $( \hat{y} = 1 )$: input is classified as belonging to the positive class
- $( \hat{y} = 0 )$: input is classified as belonging to the negative class

### 4️⃣ Decision Boundary
Because the perceptron is a linear model, its decision boundary (the surface separating the two predicted classes) is a **hyperplane** defined by:

$\mathbf{w}^T \mathbf{x} + b = 0$

This hyperplane divides the input space into two regions. Points on one side are classified as one class, and points on the other side as the opposite class.

### 5️⃣ Learning and Updates
The perceptron learns through a process of **mistake-driven learning**. It updates its weights **only when it makes a wrong prediction**.

Given a training sample $( (\mathbf{x}_i, y_i) )$, where:
- $( y_i \in \{0, 1\} )$ is the true label
- $( \hat{y}_i )$ is the predicted label
- $( \eta )$ is the learning rate

We compute the prediction $( \hat{y}_i )$ as described above.

If $( \hat{y}_i = y_i )$, no update is made.
If $( \hat{y}_i \neq y_i )$, the update is:

📐 Deriving the Update Rule

The update is not derived from a loss function in the traditional gradient descent sense. Instead, the perceptron algorithm is based on a heuristic rule that aims to correct classification errors by modifying the decision boundary.


This leads to the following intuitive update:
- For each weight:

$\Delta w_j = \eta (y_i - \hat{y}_i) x_{ij}$

- For the bias:

$\Delta b = \eta (y_i - \hat{y}_i)$


These updates push the decision boundary **toward the misclassified point**, nudging the model to improve on the error it just made.

This rule is derived from a very intuitive principle: reinforce weights in the direction of the correct class, and penalize them when the model predicts the wrong class.

### 6️⃣ Iterative Learning
The perceptron algorithm loops over the training data multiple times (epochs). In each epoch, it updates its weights and bias based on misclassified samples until:
- All training samples are correctly classified (if possible)
- Or a maximum number of iterations is reached

This process is **guaranteed to converge** only if the data is **linearly separable**.

---

## 🔎 Limitations
- Works **only for linearly separable datasets**.
- Does **not converge** if the data cannot be separated with a linear boundary.
- Uses a **non-differentiable activation function** (step function), limiting extensions to more complex networks.

---

## ✅ Advantages
- Simple to understand and implement
- Fast convergence when data is linearly separable
- Foundational for understanding more complex neural architectures

---

## 📌 Conclusion
The perceptron is a foundational algorithm that captures the essence of a neuron: weighted input, bias, activation. Though limited to linear problems, it plays an important role in the history and development of neural networks.

👉 **Next Steps:** Implement a perceptron in Python and visualize its decision boundary [here](/notebooks/01_Supervised_Learning/05_Neural_Networks/01_Perceptron.ipynb)!
