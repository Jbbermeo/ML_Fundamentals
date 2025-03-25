# 📘 Evaluation Metrics for Machine Learning Models

## 📌 Introduction
Once a machine learning model is trained, it's crucial to evaluate how well it performs on unseen data. The choice of **evaluation metrics** depends on the type of task: **classification**, **regression**, or **clustering**. Using appropriate metrics allows us to understand model performance, compare different models, and guide model improvement.

This section provides an overview of common evaluation metrics, focusing on classification and regression.

---

## ✅ Classification Metrics

### 1️⃣ Accuracy
Measures the proportion of correct predictions:
$\text{Accuracy} = \frac{\text{TP} + \text{TN}}{\text{TP} + \text{TN} + \text{FP} + \text{FN}}$
Where:
- TP: True Positives
- TN: True Negatives
- FP: False Positives
- FN: False Negatives

### 2️⃣ Precision
Measures how many predicted positives are truly positive:
$\text{Precision} = \frac{\text{TP}}{\text{TP} + \text{FP}}$ 
Useful when the cost of false positives is high.

### 3️⃣ Recall (Sensitivity or True Positive Rate)
Measures how many actual positives are correctly predicted:
$\text{Recall} = \frac{\text{TP}}{\text{TP} + \text{FN}}$
Useful when the cost of false negatives is high.

### 4️⃣ F1 Score
Harmonic mean of precision and recall:
$\text{F1} = 2 \cdot \frac{\text{Precision} \cdot \text{Recall}}{\text{Precision} + \text{Recall}}$ 
Balances false positives and false negatives.

### 5️⃣ Confusion Matrix
A table that shows TP, TN, FP, FN values in a structured format, helping visualize classification results.

### 6️⃣ ROC Curve & AUC
- **ROC Curve**: Plots True Positive Rate vs. False Positive Rate
- **AUC (Area Under Curve)**: Measures overall separability; higher is better

---

## 📉 Regression Metrics

### 1️⃣ Mean Absolute Error (MAE)
$\text{MAE} = \frac{1}{n} \sum_{i=1}^n |y_i - \hat{y}_i|$ 
Average of absolute errors; robust to outliers.

### 2️⃣ Mean Squared Error (MSE)
$\text{MSE} = \frac{1}{n} \sum_{i=1}^n (y_i - \hat{y}_i)^2$ 
Penalizes larger errors more than MAE.

### 3️⃣ Root Mean Squared Error (RMSE)
$\text{RMSE} = \sqrt{\text{MSE}}$ 
Same scale as target variable, easier to interpret.

### 4️⃣ R-squared (Coefficient of Determination)
$R^2 = 1 - \frac{\sum (y_i - \hat{y}_i)^2}{\sum (y_i - \bar{y})^2}$
Represents the proportion of variance explained by the model. Closer to 1 is better.

---

## ⚠️ Choosing the Right Metric
- Use **Accuracy** only when classes are balanced
- Prefer **Precision/Recall/F1** for imbalanced classes
- Use **ROC-AUC** when you care about ranking predictions
- Use **MAE/MSE/RMSE** depending on the importance of outlier sensitivity in regression

---

## 📌 Conclusion
Choosing appropriate evaluation metrics is essential for building effective and reliable ML models. These metrics allow us to quantify model performance, identify strengths and weaknesses, and make informed improvements.

👉 In the next sections, we’ll demonstrate how to calculate these metrics using Python and interpret them with real-world datasets.