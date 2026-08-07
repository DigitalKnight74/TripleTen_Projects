# Sprint 8 — Supervised Learning

## 🏦 Beta Bank Customer Churn Prediction

[![Python](https://img.shields.io/badge/Python-3.x-blue)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange)](https://jupyter.org/)

🔗 **[View Project on GitHub](https://github.com/DigitalKnight74/Beta_Bank_Churn)**  
🔙 **[Back to Master Portfolio](../../README.md)**

---

## 📌 Project Overview

Beta Bank customers are leaving — little by little, chipping away every month. The bank determined it's cheaper to retain existing customers than acquire new ones.

Built a classification model to predict whether a customer will leave the bank soon, using historical behavior and contract termination data. Target metric was an **F1 score of at least 0.59**, with additional AUC-ROC analysis.

---

## 🎯 Objectives

- Predict customer churn using supervised classification models
- Address class imbalance in the dataset
- Achieve a minimum F1 score of 0.59 on the test set
- Measure and compare AUC-ROC alongside F1

---

## 🛠️ Tools & Libraries

| Category | Tools |
|----------|-------|
| Language | Python |
| Data Manipulation | pandas, numpy |
| Visualization | matplotlib, seaborn |
| Machine Learning | scikit-learn |
| Models | DecisionTreeClassifier, RandomForestClassifier, ExtraTreesClassifier |
| Metrics | F1 Score, AUC-ROC |
| Environment | Jupyter Notebook |
| Version Control | Git / GitHub |

---

## 📊 Key Results

- Successfully handled class imbalance using upsampling and class weight adjustments
- ExtraTrees and Random Forest models achieved F1 scores above the 0.59 threshold
- AUC-ROC analysis confirmed strong discriminating ability of the final model

---

## 📁 Project Structure

```
Sprint-08-Supervised-Learning/
│
├── README.md
└── beta_bank_churn.ipynb
```

---

*Part of the TripleTen Data Science Bootcamp — George Knight*
