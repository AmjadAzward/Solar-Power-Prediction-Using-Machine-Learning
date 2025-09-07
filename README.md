# Solar Power Generation Forecasting  

This project predicts **AC Power output** from solar plants using machine learning. It integrates inverter-level generation data and plant-level weather sensor data collected from two solar plants in India over **34 days**.  

**Dataset:** [Solar Power Generation Data (Kaggle)](https://www.kaggle.com/datasets/anikannal/solar-power-generation-data)  

The pipeline covers data cleaning, feature engineering, model training, evaluation, and real-time forecasting.  

---

## Dataset Overview  
- **Generation Data (Plant 1 & 2):** Inverter-level power generation.  
- **Weather Data (Plant 1 & 2):** Environmental sensor measurements.  

**Key Features:**  
- *Power & Yield:* `DC_POWER`, `AC_POWER`, `DAILY_YIELD`, `TOTAL_YIELD`  
- *Weather Conditions:* `AMBIENT_TEMPERATURE`, `MODULE_TEMPERATURE`, `IRRADIATION`  

---

##  Workflow  

### 1. Data Preprocessing  
- Merge generation and weather data by timestamp.  
- Handle missing values (forward-fill).  
- Convert timestamps and extract time-based features.  

### 2. Feature Engineering  
- **Rolling Features:**  
  - 1-hour mean & standard deviation  
  - 3-hour maximum irradiation  
- **Lag Features:** Previous interval values (DC power, irradiation).  
- **Cumulative Features:** Daily yield progression.  
- **Interaction Features:** Irradiation × Temperature.  
- **Efficiency Metric:** `DC Power / Irradiation`.  

### 3. Model Training  
Algorithms evaluated:  
- Linear Regression  
- Decision Tree  
- Random Forest  
- Gradient Boosting  
- K-Nearest Neighbors (KNN)  
- Neural Network (MLP)  

**Training Setup:**  
- Data split: 70% train, 15% validation, 15% test  
- Preprocessing: Imputation + Standard Scaling  
- Metrics: **R² Score**, **RMSE**  

### 4. Model Evaluation  
- Select best model by validation R².  
- Evaluation includes:  
  - Scatter plots (Actual vs Predicted)  
  - Time series comparison  
  - Residual analysis  

### 5. Deployment  
- Save artifacts: `best_model.pkl`, `scaler.pkl`, `imputer.pkl`, `feature_cols.pkl`.  
- Supports **real-time predictions** with history buffer for lag/rolling features.  
- Batch forecasting for short-term (few hours ahead) power prediction.  

---

## Results  
- **Best Model:** Random Forest (achieved highest R²).  
- **Performance:** Strong alignment between predicted and actual AC power.  
- **Visualization:** Predictions accurately follow solar generation trends.  

---

## Final Output  
- **Real-time AC power prediction**  
- **Short-term AC power forecasting** (few hours ahead)  
