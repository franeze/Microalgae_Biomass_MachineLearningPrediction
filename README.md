# Predicting Microalgae Biomass Using Machine Learning and Sensor Data
Machine learning project to predict microalgae biomass from environmental and physicochemical data. Compares Linear Regression, Random Forest, and XGBoost, with hyperparameter tuning. Results show strong performance and capture non-linear biological dynamics like nutrient consumption and metabolism.

![AI-PBR](image/correlation_matrix.png)

## Overview
This project develops a machine learning model to predict microalgae biomass concentration (g/L) using environmental and physicochemical variables collected during cultivation.

By leveraging sensor data instead of direct measurement methods such as dry weight analysis, the model provides a faster and scalable alternative for biomass estimation, enabling more efficient monitoring of cultivation processes.

Multiple models were evaluated, including Linear Regression (baseline), Random Forest, and XGBoost. Results show that tree-based models significantly outperform linear approaches, capturing the non-linear dynamics of biological systems.

---

## Scientific Problem
Estimating microalgae biomass typically requires direct measurement techniques that are accurate but time-consuming and labor-intensive. This limits their use for real-time monitoring and process optimization.

The objective of this project is to develop a predictive model capable of estimating biomass concentration from readily available environmental and physicochemical parameters, enabling indirect, faster, and more scalable monitoring.

---

## Dataset
The dataset includes measurements from microalgae cultivation experiments, combining environmental conditions and physicochemical variables:

| Variable         | Description                                                         | Unit      |
|------------------|---------------------------------------------------------------------|----------|
| Biomass          | Biomass concentration (dry weight method)                          | g/L      |
| Irradiance       | Light intensity                                                    | µmol/m²/s|
| Temperature      | Culture temperature                                                | °C       |
| pH               | Acidity/alkalinity                                                 | -        |
| NO₃              | Nitrate concentration                                              | mg/L     |
| O₂ Gas           | Oxygen concentration (gas phase)                                   | %        |
| CO₂ Gas          | Carbon dioxide concentration (gas phase)                           | ppm      |
| OD               | Dissolved oxygen                                                   | mg/L     |
| Conductivity     | Ionic concentration indicator                                      | µS/cm    |

Source: https://www.sciencedirect.com/science/article/pii/S2352340925007279

---

## Exploratory Data Analysis
Exploratory analysis revealed:

- A **non-normal and potentially multimodal distribution** of biomass, reflecting different growth phases.
- Strong correlations between biomass and key variables:
  - Negative: NO₃, O₂ Gas, CO₂ Gas
  - Positive: pH, Conductivity
- High **multicollinearity**, particularly among variables related to system dynamics.

These patterns indicate that the dataset represents a **dynamic biological system**, where variables are interdependent and evolve together over time.

---

## Methodology
Due to the absence of explicit temporal structure, the problem was formulated as a **static regression task**, where each observation represents a snapshot of the system state.

Feature selection was performed to reduce multicollinearity and improve interpretability. The final feature set included:

- Irradiance  
- NO₃  
- Temperature  
- Dissolved Oxygen (OD)  
- Conductivity  

Tree-based models were selected to capture non-linear relationships and interactions between variables.

---

## Model Development
Three models were implemented and compared:

- **Linear Regression** (baseline)
- **Random Forest**
- **XGBoost**

For Random Forest and XGBoost, **hyperparameter tuning** was performed using GridSearchCV to identify optimal configurations.

Model performance was evaluated using:
- RMSE (Root Mean Squared Error)
- R² (Coefficient of Determination)

---

## Results

| Model            | RMSE  | R²    |
|------------------|------|------|
| Linear Regression| 0.177 | 0.960 |
| Random Forest    | 0.099 | 0.987 |
| XGBoost          | 0.107 | 0.985 |

- Random Forest achieved the best overall performance.
- Tree-based models significantly outperformed the linear baseline.

---

## Visual Results

### Correlation Matrix
![image/Correlation Matrix](correlation_matrix.png)

The correlation matrix highlights strong relationships between biomass and key variables, particularly the inverse relationship with NO₃ and gas concentrations, reflecting nutrient consumption and metabolic processes.



### Predicted vs Actual Biomass (Random Forest)
![Predicted vs Actual](predicted_vs_actual.png)

The close alignment between predicted and actual values indicates high model accuracy and strong generalization performance.



### Feature Importance (Random Forest)
![Feature Importance](feature_importance.png)

NO₃ dominates the model, confirming its role as the primary driver of biomass variability, while other variables contribute marginally.

---

## Key Insights
- Biomass is primarily driven by **nitrate availability (NO₃)**, which dominates model predictions.
- The model captures **non-linear biological dynamics**, including nutrient consumption and metabolic activity.
- The dataset reflects a **process-driven system**, not independent observations.

---

## Conclusion
The results demonstrate that microalgae biomass can be accurately predicted using indirect measurements from sensor data.

This approach provides a practical alternative to traditional measurement methods, enabling faster and more scalable monitoring. It also highlights the potential of machine learning for modeling complex biological systems and supporting real-time decision-making in biotechnology applications.

---

## Technologies Used
- Python
- pandas
- numpy
- scikit-learn
- xgboost
- matplotlib
- seaborn
