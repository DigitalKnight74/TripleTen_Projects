# Sprint 13 — Time Series

## 🚕 Sweet Lift Taxi — Hourly Airport Demand Forecast

[![Python](https://img.shields.io/badge/Python-3.x-blue)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange)](https://jupyter.org/)

🔗 **[View Project on GitHub](https://github.com/DigitalKnight74/Sweet_Lift_Taxi_Company)**  
🔙 **[Back to Master Portfolio](../../README.md)**

---

## 📌 Project Overview

Sweet Lift Taxi company collected historical data on taxi orders at airports. To attract more drivers during peak hours, built a time series forecasting model to predict the number of taxi orders for the next hour.

Target: **RMSE on the test set must not exceed 48.**

---

## 🎯 Objectives

- Resample and prepare time series data at hourly intervals
- Decompose the series to analyze trend and seasonality
- Engineer time-based features (lag features, rolling averages)
- Build and compare multiple forecasting models
- Achieve a test RMSE of 48 or below

---

## 🛠️ Tools & Libraries

| Category | Tools |
|----------|-------|
| Language | Python |
| Data Manipulation | pandas |
| Time Utilities | time |
| Machine Learning | scikit-learn |
| Gradient Boosting | LightGBM |
| Models | LinearRegression, RandomForestRegressor |
| Preprocessing | StandardScaler |
| Time Series | Seasonal Decompose |
| Metrics | RMSE |
| Environment | Jupyter Notebook |
| Version Control | Git / GitHub |

---

## 📊 Key Results

- Time series decomposed to identify trend and seasonal patterns in taxi demand
- Lag features and rolling mean features engineered for model input
- LightGBM achieved the best RMSE, well within the target threshold of 48
- Random Forest and Linear Regression used as baseline comparisons

---

## 📁 Project Structure

```
Sprint-13-Time-Series/
│
├── README.md
└── sweet_lift_taxi_forecast.ipynb
```

---

*Part of the TripleTen Data Science Bootcamp — George Knight*
