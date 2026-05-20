# 🚗 Accident Risk & Severity Prediction

> *This project was developed as part of the **Digilians Initiative** – a collaborative program supervised by the **Ministry of Communication and Information Technology (MCIT)** and the **Egyptian Military Academy**.*

---

## 📌 Overview

Road accidents remain a major global safety challenge, causing injuries, fatalities, and significant economic losses every year. Many transportation authorities still rely on historical reports and descriptive statistics rather than predictive analytics, limiting their ability to proactively identify risks and implement effective safety measures.

This project presents a **data-driven machine learning framework** that analyzes large-scale traffic accident data to predict accident severity and identify key risk patterns. By leveraging the **US Accidents dataset** (over 7 million records), we built and compared multiple gradient boosting models to provide actionable insights for road safety improvement.

The final system helps answer critical questions like:
- ❓ **What factors** (weather, time, road infrastructure) most influence accident severity?
- 📍 **Where are the high-risk locations**?
- ⚠️ **How severe is an accident likely to be** given specific conditions?

---

## 🎯 Key Beneficiaries

| Stakeholder | How They Benefit |
| :--- | :--- |
| 🚑 **Emergency Services & EMS** | Prioritize response, optimize ambulance dispatch, and prepare medical teams based on predicted severity and risk levels. |
| 🚦 **Road Safety Authorities** | Identify high-risk locations and improve infrastructure (signals, crossings, traffic calming). |
| 🏥 **Hospitals & Trauma Centers** | Anticipate incoming critical cases, allocate ICU beds, and improve emergency preparedness. |
| 🏙️ **Urban Planners & Policy Makers** | Design safer transportation systems using data-driven decisions. |
| 👨‍👩‍👧‍👦 **Drivers & the Public** | Increase awareness of dangerous areas and conditions, helping reduce personal risk. |

---

## 📊 Dataset

- **Source**: [US Accidents Dataset on Kaggle](https://www.kaggle.com/datasets/sobhanmoosavi/us-accidents) (created by Sobhan Moosavi)
- **Size**: > 7 million accident records across the United States
- **Features include**:
  - 📍 **Location**: Coordinates, city, county, state, zipcode
  - ⏰ **Temporal**: Start time, end time, sunrise/sunset, twilight conditions
  - 🌦️ **Weather**: Temperature, humidity, pressure, visibility, wind speed/direction, precipitation
  - 🛣️ **Road infrastructure**: Traffic signals, bumps, crossings, junctions, railways, roundabouts
  - 📋 **Accident characteristics**: Severity (target variable, levels 1–4), distance affected, description

---

## ⚙️ Methodology

### 🧹 Preprocessing & Feature Engineering
- Removed irrelevant/redundant columns (`ID`, `End_Time`, `End_Lat`, `End_Lng`, etc.)
- Handled missing values: **median** for numerical features, **mode** for categorical features
- Extracted temporal features: hour, day of week, month, year, rush hour indicator
- Applied **frequency encoding** to high-cardinality categorical variables (city, weather condition, etc.)
- Used **binary encoding** for boolean infrastructure flags
- Scaled numerical features with **StandardScaler**

### ⚖️ Handling Class Imbalance
The dataset is heavily imbalanced (Severity 2 dominates). We applied:
- ⬇️ **Downsampling** of the majority class
- ⬆️ **Oversampling** of minority classes (Severity 1 and 4)
- 🎯 **Class weights** to force the model to pay more attention to rare but critical events

### 🤖 Models Evaluated
- **XGBoost** (best performer) 🏆
- **LightGBM**
- **CatBoost**
- Neural Network (baseline)

**Evaluation Metrics** (primary: F1-score due to imbalance):
- Precision, Recall, F1-score (per class + macro/weighted averages)
- Confusion Matrix

---

## 📈 Results

### Overall Model Performance

| Rank | Model | Macro F1-Score | Weighted F1-Score | Accuracy |
|:----:|:------|:--------------:|:-----------------:|:--------:|
| 🥇 **1** | **XGBoost** | **0.674** | **0.861** | 0.857 |
| 🥈 2 | LightGBM | 0.660 | 0.854 | 0.850 |
| 🥉 3 | Neural Network | 0.640 | 0.850 | 0.850 |
| 4 | CatBoost | 0.640 | 0.848 | 0.850 |

### 🔍 XGBoost Classification Report (Detailed)

| Severity Class | Precision | Recall | F1-Score | Support |
|:--------------|----------:|-------:|---------:|--------:|
| 1️⃣ | 0.626 | 0.772 | **0.691** | 13,473 |
| 2️⃣ | 0.924 | 0.908 | **0.916** | 1,231,396 |
| 3️⃣ | 0.698 | 0.661 | **0.679** | 259,868 |
| 4️⃣ | 0.321 | 0.569 | **0.411** | 40,942 |

**Key Takeaways**:
- ✅ XGBoost achieved the highest macro and weighted F1-scores, making it the recommended model.
- ✅ Performance on the majority class (Severity 2) is excellent (>0.90 F1).
- ⚠️ The minority classes, especially **Severity 4** (most severe), remain challenging due to extreme class imbalance.
- 🔄 Most misclassifications occur between **adjacent severity levels** – an expected pattern given the ordinal nature of the target.

---

## 🔁 System Pipeline

1. 🧠 **Problem Definition** – Predict accident severity and identify risk patterns.
2. 📥 **Data Collection** – US Accidents dataset (Kaggle).
3. 🧹 **Data Preprocessing** – Cleaning, imputation, encoding, scaling.
4. 📊 **Exploratory Data Analysis (EDA)** – Temporal trends, weather impacts, geographic hotspots.
5. 🤖 **Model Development** – Training XGBoost, LightGBM, CatBoost, and a Neural Network.
6. 📉 **Model Evaluation** – Precision, recall, F1-score, confusion matrix.
7. 🖥️ **Deployment (Insights)** – Interactive Power BI dashboard (planned).
8. 🔁 **Monitoring** – Continuous improvement with new data.

---

## ⚠️ Limitations

- ❓ **Missing data** in weather, wind chill, and precipitation fields required imputation.
- 🗺️ **Geographic bias** – the dataset is US-focused; results may not generalize globally.
- ⏱️ **No real-time information** – predictions are based on historical patterns.
- 🧑‍✈️ **Driver behavior data** (speed, fatigue, distraction) is not included, which could improve accuracy.
- ⚖️ **Class imbalance** remains a challenge for predicting the most severe accidents.

---

## 🚀 Future Work

- 🚦 **Integrate real-time traffic data** (live congestion, flow) to improve prediction accuracy.
- 🧠 **Apply deep learning models** (LSTMs for temporal patterns, CNNs for spatial feature extraction).
- 📡 **Develop a live traffic risk monitoring system** with real-time dashboards.
- 📱 **Incorporate driver behavior data** (telematics, speed, fatigue indicators).
- 🎯 **Advanced class imbalance techniques** (SMOTE, cost-sensitive learning).
- 🛠️ **Expand feature engineering** (road geometry, historical accident density, seasonal patterns).

---

## 👥 Team Contributions
| Team Member     |
| :-------------- |
| **Dina Ali**  |
| **Nada Shady**    |
| **Marwa Ashraf**|

**Project Supervisors**:
- Dr. Walaa H. Elashmawi (Academic Supervisor)
- Digilians Initiative – MCIT & Egyptian Military Academy

---

## 🛠️ Tools & Environment

- **Platform**: Kaggle
- **Libraries**:
  - 🐼 `pandas`, `numpy` – data manipulation
  - 📊 `matplotlib`, `seaborn` – visualization
  - 🔧 `scikit-learn` – preprocessing, scaling, metrics, train-test split
  - 🏷️ `category_encoders` – target encoding
  - ⚡ `xgboost`, `lightgbm`, `catboost` – gradient boosting models

---

## 🧪 How to Run (Brief)

1. 📥 Download the US Accidents dataset from [Kaggle](https://www.kaggle.com/datasets/sobhanmoosavi/us-accidents).
2. 🧹 Run the preprocessing notebook to clean and engineer features.
3. 🤖 Train models using the provided scripts (XGBoost recommended).
4. 📊 Evaluate using the classification report and confusion matrix functions.
5. 📈 (Optional) Load the Power BI dashboard for interactive exploration of risk patterns.

> *📝 Note: Full code and notebooks are available in the repository.*

---

## 📚 References

- Moosavi, S. et al. "US Accidents Dataset." Kaggle. [Link](https://www.kaggle.com/datasets/sobhanmoosavi/us-accidents)
- [New York Car Accident Statistics](https://www.rosenbaumnylaw.com/new-york-car-accident-lawyer/statistics/)
- [Medium: EDA & Predictive Modeling of US Vehicle Accidents](https://medium.com/@hamzah110/exploratory-data-analysis-predictive-modeling-of-us-vehicle-accidents-ffe0155b7e4c)

---

## 🙏 Thank You

For questions or collaboration opportunities, please reach me out .
