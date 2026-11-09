# 🗽 NYC Taxi & Limousine Commission (NYC TLC) - Predictive Analytics Project
> **Professional Data Science Portfolio Project** developed by **Automatidata** in collaboration with the New York City Taxi and Limousine Commission (NYC TLC).

---

## 📊 Data Source

The dataset used for this analysis originates from the project's official source:
* **Dataset:** [(2017 Yellow Taxi Trip Data)](https://data.cityofnewyork.us/Transportation/2017-Yellow-Taxi-Trip-Data/biws-g3hs/about_data) 
* **Descripción:** Each row represents a single trip in a yellow taxi. The trip records include fields capturing pick-up and drop-off dates/times, pick-up and drop-off taxi zone locations, trip distances, itemized fares, rate types, payment types, and driver-reported passenger counts. The TLC data comes from over 200,000 taxi and limousine licensees, making approximately one million combined trips per day.
> **Note:** This project's dataset was created for pedagogical purposes and may not be indicative of New York City taxi cab riders' behavior.

---

## 📌 Project Overview
The overarching objective of this project is to assist the **NYC TLC** in better understanding taxi trip and fare patterns, validating business hypotheses, and building high-performance predictive models to optimize driver revenue and streamline fare estimation.

This repository encompasses a complete data science lifecycle:
1. **Exploratory Data Analysis (EDA) & Data Cleaning:** Identifying anomalies (e.g., 0.0-mile trips with positive fares) and inspecting right-skewed distributions.
2. **A/B Statistical Testing:** Evaluating whether payment methods (credit card vs. cash) statistically impact total fare amounts.
3. **Multiple Linear Regression (MLR):** Building a continuous fare prediction model incorporating spatial aggregation features (`mean_distance`, `mean_duration`).
4. **Machine Learning Classification (Random Forest / XGBoost):** Predicting "generous" passenger tipping behavior ($\ge 20\%$) and evaluating model performance under strict operational constraints.

---

## 🗂️ Repository Structure

```text
TLC-project/
│
├── Notebooks/
│   ├── 01_EDA_and_Inspection.ipynb
│   ├── 02_Hypothesis_Testing_AB.ipynb
│   ├── 04_Multiple_linear_regression.ipynb
│   └── 05_Machine_learning.ipynb
│
├── Reports/
│   ├── Executive_Summary_NYC_TLC_EDA_AB.docx
│   ├── Executive_Summary_NYC_TLC_Multiple_Linear_Regression.docx
│   └── Executive_Summary_NYC_TLC_Machine_Learning.docx
│
└── README.md
