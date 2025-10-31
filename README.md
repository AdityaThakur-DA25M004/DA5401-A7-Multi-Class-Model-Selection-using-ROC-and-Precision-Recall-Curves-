# DA5401 Assignment-7: Multi-Class Model Selection using ROC & Precision-Recall Curves

#### Name: Aditya Thakur &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Roll No: DA25M004

This project implements and analyzes multiple machine learning models for **multi-class satellite land-cover classification** using the **UCI Landsat Satellite dataset**.  
The focus is on **threshold-based model evaluation** using:

- ✅ Multi-Class ROC Curves (OvR)
- ✅ Multi-Class Precision–Recall Curves (OvR)
- ✅ Weighted AUC & Average Precision (AP)
- ✅ Weighted F1-Score & Accuracy

The assignment applies both **baseline classical ML models** and **ensemble models** for bonus points, identifies a **model performing worse than random**, and recommends the **best performing model** for deployment.

---

## 🎯 Learning Objectives

| Task | Skill Demonstrated |
|---|---|
Data preparation | Clean dataset, verify splits |
Baseline modeling | Six classical models |
Evaluation | Accuracy, weighted-F1, ROC-AUC (OvR), PR-AUC |
Curve interpretation | ROC & PR insights |
Model tuning | RF & XGBoost |
Failure case | Model with AUC < 0.5 |

---

## 📊 Dataset — UCI Landsat Satellite

- 6 land-cover classes
- Moderate imbalance (classes 1, 3, 7 dominant)
- Multispectral continuous features

---

## ✅ Part A — Data Preparation & Baseline Performance

### ✔ Models Trained
| Model | Purpose |
|---|---|
Dummy Classifier | Baseline |
Logistic Regression | Linear model |
KNN | Distance-based |
Decision Tree | Interpretable baseline |
Gaussian NB | Probabilistic baseline |
SVC | Kernel decision model |

### 🎯 Baseline Results
| Model | Accuracy | Weighted-F1 | Notes |
|---|---|---|---|
Dummy | ~0.23 | ~0.09 | Majority class |
Naive Bayes | ~0.80 | ~0.80 | Independence assumption |
Logistic Regression | ~0.83 | ~0.82 | Strong linear baseline |
Decision Tree | ~0.85 | ~0.86 | High variance |
KNN | ~0.90 | ~0.90 | Top baseline |
SVC | ~0.90 | ~0.89 | Most stable |

---

## 🧠 Part B — Multi-Class ROC-AUC (OvR)

| Model | Macro AUC | Notes |
|---|---|---|
SVC | ~0.985 | Best separation |
KNN | ~0.979 | Very close second |
Decision Tree | Moderate | Variance hurts ranking |
Gaussian NB | Good, weaker precision | |
Dummy | ~0.50 | Random baseline |
**Isolation Forest** | **~0.497** | **Worse than random (AUC < 0.5)** 

---

## 🎯 Part C — Multi-Class Precision-Recall (OvR)

| Model | Avg Precision | Behavior |
|---|---|---|
KNN | ~0.93 | Best |
SVC | ~0.93 | Most stable |
Naive Bayes | ~0.82 | Precision drop |
Decision Tree | ~0.74 | Fit instability |
Dummy | ~0.18 | Random baseline |

---

## 🧾 Part D — Final Recommendation

| Metric | Best |
|---|---|
Accuracy | KNN / SVC |
Weighted-F1 | KNN / SVC |
ROC-AUC | SVC |
PR-AUC | KNN ≈ SVC |

### ✅ Final Pick: **SVC**
- Highest ROC-AUC
- Excellent PR-AUC
- Stable across thresholds

KNN = strong runner-up

---

## ⭐ Brownie Points — Random Forest & XGBoost (Tuned Models)

| Model | Accuracy | Weighted-F1 |
|---|---|---|
Random Forest (tuned) | `0.9050` | `0.9046` |
**XGBoost (tuned)** | **`0.9075`** | **`0.9057`** |

### Ranking Among All Models

| Rank | Model |
|---|---|
🥇 | XGBoost (Tuned) |
🥈 | SVC |
🥉 | KNN |
4️⃣ | Random Forest (Tuned) |
---

## ❌ Additional Low-Performance Models (AUC < 0.5)

### 📉 Isolation Forest

**Extracted Results**
- ROC-AUC: **≈0.497**

**Interpretation**
- Performs **worse than random**
- Flags normal pixels as anomalies
- Not suitable since land-cover classes are not "outliers"

> 🔴 Works for anomaly detection — not multi-class classification.

### 📉 BernoulliNB

- Accuracy: `0.2305`
- Weighted-F1: `0.0864`
- AUC: **0.4937** (≈ random)

Fails due to binary-feature assumption on continuous data.

---

## 📊 Final Model Ranking

| Rank | Model |
|---|---|
1 | XGBoost (Tuned) |
2 | SVC |
3 | KNN |
4 | Random Forest (Tuned) |
5 | Logistic Regression |
6 | Gaussian NB |
7 | Decision Tree |
8 | **Isolation Forest & BernoulliNB (AUC < 0.5)** |
9 | Dummy baseline |

---

## ✅ Key Takeaways

- PRC more informative under imbalance
- AUC < 0.5 signals inverted scoring
- SVC best baseline
- XGBoost best tuned model

---
