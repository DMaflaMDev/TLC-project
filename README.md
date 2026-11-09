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
```
---

## 📊 Key Phases & Technical Highlights

### 1. Exploratory Data Analysis & A/B Hypothesis Testing
* **Anomaly Detection:** Flagged structural inconsistencies, such as trips with recorded distances of $0.0$ miles paired with positive total fares ($+\$80$), which were subsequently filtered out from modeling pipelines.
* **A/B Test Results:** Performed a Welch’s t-test comparing credit card and cash transactions. Results proved that credit card fares ($\$16.35$) are statistically higher ($p < 0.001$) than cash fares ($\$13.54$), supporting digital payment promotion strategies.

### 2. Multiple Linear Regression (Fare Prediction)
* **Performance Metrics:** Achieved an $R^2$ of $0.868$ (explaining ~86.8% of fare variance) with an MAE of $\$2.13$ and RMSE of $\$3.77$.
* **Feature Engineering:** Calculated route-level aggregates (`mean_distance` and `mean_duration` grouped by pickup/drop-off zone pairs) to mitigate multicollinearity.
* **Deterministic Rules:** Implemented post-prediction rule-based imputation for JFK Airport flat-rate trips (`RatecodeID 2` / Location 132) to guarantee 100% accuracy on fixed routes.

### 3. Machine Learning Classification (Generous Tipping Prediction)
* **Classification Target:** Predict whether a rider will leave a generous tip ($\ge 20\%$ of fare). Restricted to credit card transactions where tip data is reliably captured.
* **Model Comparison:** 
  * **Random Forest (Champion):** $F_1\text{-score} = 0.72$ | $\text{Recall} = 0.74$ | $\text{Precision} = 0.70$
  * **XGBoost Classifier:** $F_1\text{-score} = 0.71$
* **Feature Importance (Gini Importance):** Identified `VendorID_2`, `predicted_fare`, `mean_distance`, and `mean_duration` as the primary drivers of tree-based split decisions.

---

## 💡 Strategic Recommendations & Expert Evaluation

### 1. Model Deployment Verdicts
* **Multiple Linear Regression (Fare Prediction) — RECOMMENDED FOR DEPLOYMENT:** 
  * **Performance Metrics:** Achieved an **$R^2$ of $0.868$** (explaining ~86.8% of total fare variance) with a **Mean Absolute Error (MAE) of $\$2.13$** and a **Root Mean Squared Error (RMSE) of $\$3.77$**.
  * **Use Case:** Highly effective for upstream pre-ride fare estimations in driver and customer apps, providing transparent pricing before trips take place.
  * **How to Improve for Production:**
    * *Post-Prediction Rule Imputation:* Automatically override model outputs for flat-rate routes (e.g., forcing a fixed $\$52.00$ fare for JFK Airport trips under `RatecodeID 2` / Location 132).
    * *Time-Series & Congestion Adjustments:* Incorporate real-time traffic density APIs and dynamic surge pricing flags as additive multipliers.
    * *Non-Linear Traffic Dynamics:* Transition to Gradient Boosting regression (XGBoost/LightGBM) to better model non-linear interactions between peak hours and specific borough corridors.

* **Random Forest (Generous Tip Prediction) — NOT RECOMMENDED IN CURRENT FORM:**
  * **Performance Metrics (Random Forest Champion):** $F_1\text{-score} = 0.72$ | $\text{Recall} = 0.74$ | $\text{Precision} = 0.70$
  * **Verdict:** Deploying the tipping classification model is **not recommended**. Increasing driver revenue should not rely on predicting passenger tips, and classification errors (false positives/negatives) risk introducing driver bias and platform frustration.

### 2. Advanced Feature Engineering Roadmap (Future Iterations)
* **Cost-per-Distance / Speed Ratio:** Calculate `predicted_fare` divided by `mean_distance` or `mean_duration` to estimate fare density and traffic congestion levels.
* **Interaction Terms:** Combine temporal peak hour flags (`am_rush`, `pm_rush`) with specific pickup/drop-off location pairs (`PULocationID` / `DOLocationID`).
* **High-Impact Data Requirements:** Integrate **Passenger Historical Behavior** (aggregated tipping frequency across past rides) and **Driver Service Quality Metrics** (ratings and feedback history) to enhance signal clarity.

---

## 🛠️ Tech Stack & Libraries
* **Python** 🐍
* **Data Manipulation & Analysis:** Pandas, NumPy
* **Machine Learning & Stats:** Scikit-Learn (Random Forest, XGBoost, GridSearchCV, OLS Regression, Welch's t-test)
* **Visualization:** Matplotlib, Seaborn
* **Environment:** Jupyter Notebooks
