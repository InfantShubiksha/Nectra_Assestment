# Nectra_Assestment
## Project Overview

This project was developed as part of the Nectar Data Scientist Challenge for analyzing IoT telemetry data from commercial buildings.

The objective is to transform sensor and asset data into actionable insights for:

- Equipment reliability
- Predictive maintenance
- Energy optimization
- Anomaly detection
- Multi-asset dependency analysis

The project covers five tasks:

1. Exploratory Data Analysis
2. Predictive Maintenance
3. Energy Consumption Forecasting
4. Anomaly Detection
5. Multi-Asset Connectivity Analysis


## Dataset

Three datasets 

### 1. telemetry.csv

Contains historical sensor readings including:

- timestamp
- site_id
- building_id
- asset_id
- temperature
- humidity
- pressure
- vibration
- power_consumption
- occupancy_count
- operating_mode
- fault_flag

### 2. asset_metadata.csv

Contains asset information including:

- asset_id
- site_id
- asset_name
- asset_type
- manufacturer
- installation_date
- capacity
- parent_asset_id

### 3. connectivity.csv

Contains relationships between assets including:

- source_asset_id
- target_asset_id
- connection_type
- relationship_strength

# Task 1 – Exploratory Data Analysis

The telemetry data was analyzed to understand sensor distributions, data quality, temporal patterns, asset behavior, energy consumption, and equipment failures.

The analysis included:

- Missing-value analysis
- Statistical summaries
- Sensor distributions
- Temporal energy-consumption patterns
- Building-level analysis
- Asset-level analysis
- Failure analysis
- Correlation analysis
- Energy-consumption drivers

## Key Insights

The analysis identified differences in operating behavior across buildings and assets and highlighted relationships between telemetry variables, energy consumption, and equipment failures.

These insights were used to guide feature engineering and subsequent machine-learning tasks.



# Task 2 – Predictive Maintenance

## Objective

Predict whether an asset is likely to experience a failure within the next 24 hours.

## Approach

A future-failure target was created using the historical `fault_flag`.

Feature engineering included:

- Current sensor measurements
- 24-hour rolling averages
- Lag features
- Temperature trends
- Vibration trends
- Power-consumption trends

A **Random Forest Classifier** was selected because it can capture nonlinear relationships between equipment telemetry variables and failure behavior.

Due to the imbalance between failure and non-failure cases, probability-threshold tuning was performed to improve failure detection.

## Evaluation

The model was evaluated using:

- Precision
- Recall
- F1 Score
- ROC-AUC
- Confusion Matrix

The final model achieved:

- Accuracy: **72.74%**
- Precision: **49.14%**
- Recall: **24.09%**
- F1 Score: **32.33%**
- ROC-AUC: **0.672**

Threshold analysis was also performed. A threshold of **0.35** provided a higher failure recall and was considered more suitable for a preventive-maintenance scenario where missing a potential failure can be costly.

## Important Features

Feature importance analysis was performed to identify telemetry variables contributing to model predictions.

The results can help maintenance teams understand which operational signals are most useful for identifying potential failures.



# Task 3 – Energy Consumption Forecasting

## Objective

Forecast energy consumption for the next 24 hours for each building.

Historical energy-consumption patterns were used to generate building-level forecasts.

## Evaluation Metrics

Forecast performance was evaluated using:

- MAE
- RMSE
- MAPE

Forecast plots were generated to compare actual and predicted energy consumption.

## Business Impact

The forecasts can support:

- Proactive energy planning
- Identification of high-demand periods
- Energy-saving initiatives
- Building-level operational optimization


# Task 4 – Anomaly Detection

## Objective

Identify abnormal equipment behavior from historical telemetry.

The analysis considered operational variables such as:

- Temperature
- Vibration
- Power consumption
- Humidity
- Pressure

Anomaly detection was used to identify unusual combinations of sensor readings that may indicate equipment abnormalities, sensor issues, or unusual energy behavior.

The detected anomalies were exported for further analysis.

### Business Recommendations

- Investigate repeated high-vibration events.
- Monitor sudden power-consumption spikes.
- Investigate abnormal temperature patterns.
- Prioritize assets with repeated anomalies.
- Combine anomaly results with predictive-maintenance predictions for better maintenance prioritization.



# Task 5 – Multi-Asset Connectivity Analysis

## Objective

Analyze relationships and dependencies between assets across sites and buildings.

## Asset Hierarchy

The available parent-child relationships were used to represent the asset hierarchy:

**Site → Building → Asset**

The hierarchy captures relationships between equipment such as chillers, AHUs, pumps, sensors, and energy meters.

## Connectivity Analysis

Connectivity relationships were analyzed using:

- Supplies
- Controls
- Monitors

A dependency graph was created to visualize relationships between connected assets.

## Failure Impact Analysis

Downstream assets were identified for each asset using the connectivity graph.

This allows the potential operational impact of a critical asset failure to be assessed.

## Data Quality Assessment

The following checks were performed:

- Missing values
- Duplicate asset IDs
- Duplicate connections
- Orphan/top-level assets
- Parent-child relationships

The analysis identified six top-level assets without parent assets, corresponding to the primary chiller assets.

## Business Impact

The connectivity analysis can support:

- Failure propagation analysis
- Root-cause analysis
- Maintenance prioritization
- Dependency monitoring
- Operational risk assessment


# Overall Business Value

The combined analysis provides a foundation for an intelligent facilities monitoring platform.

The solution can help organizations:

- Predict potential equipment failures
- Plan maintenance proactively
- Forecast energy consumption
- Detect abnormal equipment behavior
- Understand asset dependencies
- Prioritize critical equipment
- Reduce potential downtime
- Improve energy efficiency



# Assumptions

- A failure occurring within the next 24 hours is treated as a positive future-failure event.
- Historical telemetry is assumed to represent the operating behavior of the assets.
- The provided connectivity dataset is treated as the available source of truth for asset relationships.
- Assets without a parent asset are treated as top-level assets.
- Forecasting is based on historical energy-consumption patterns.
- The predictive-maintenance probability threshold can be adjusted depending on the business cost of false alarms versus missed failures.



# Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- NetworkX
- Jupyter Notebook



# Project Structure


Nectar_Data_Scientist_Challenge/
│
├── data/
│   ├── telemetry.csv
│   ├── asset_metadata.csv
│   └── connectivity.csv
│
├── notebooks/
│   ├── 01_EDA.ipynb
│   ├── 02_Predictive_Maintenance.ipynb
│   ├── 03_Energy_Forecasting.ipynb
│   ├── 04_Anomaly_Detection.ipynb
│   └── 05_Connectivity_Analysis.ipynb
│
├── outputs/
│   ├── identified_equipment_anomalies.csv
│   ├── asset_anomaly_summary.csv
│   ├── failure_impact_analysis.csv
│   └── asset_connectivity_report.csv
│
├── README.md
└── requirements.txt
