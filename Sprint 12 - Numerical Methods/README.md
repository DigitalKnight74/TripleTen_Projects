# Sprint 12 — Numerical Methods

## 🚗 Rusty Bargain Used Car Sales — Market Value Prediction

[![Python](https://img.shields.io/badge/Python-3.x-blue)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange)](https://jupyter.org/)

🔗 **[View Project on GitHub](https://github.com/DigitalKnight74/Rusty_Bargain_Used_Car_Sales_Service)**  
🔙 **[Back to Master Portfolio](../../README.md)**

---

## 📌 Project Overview

Rusty Bargain used car sales service is developing an app to help customers quickly find the market value of their car. Using historical data on technical specifications, trim versions, and prices, built and compared multiple regression models evaluating not just accuracy — but **prediction speed** and **training time** as well.

---

## 🎯 Objectives

- Build a model to accurately predict used car market value
- Compare models across three dimensions: prediction quality, prediction speed, and training time
- Apply gradient boosting techniques (LightGBM, CatBoost) alongside traditional methods
- Tune hyperparameters using RandomizedSearchCV

---

## 🛠️ Tools & Libraries

| Category | Tools |
|----------|-------|
| Language | Python |
| Data Manipulation | pandas, numpy |
| Date/Time | datetime, time |
| Machine Learning | scikit-learn |
| Gradient Boosting | LightGBM, CatBoost |
| Models | LinearRegression, RandomForestRegressor, DecisionTreeRegressor |
| Preprocessing | StandardScaler, TargetEncoder, OneHotEncoder |
| Tuning | RandomizedSearchCV |
| Metrics | RMSE |
| Environment | Jupyter Notebook |
| Version Control | Git / GitHub |

---

## 📊 Key Results

- LightGBM and CatBoost delivered the best prediction quality (RMSE)
- LightGBM offered the best balance of quality vs. training and prediction speed
- Linear Regression was fastest to train and predict but with lower accuracy
- Random Forest offered competitive accuracy at the cost of longer training time

---

## 📁 Project Structure

```
Sprint-12-Numerical-Methods/
│
├── README.md
└── rusty_bargain_used_car_sales.ipynb
```

---

*Part of the TripleTen Data Science Bootcamp — George Knight*
