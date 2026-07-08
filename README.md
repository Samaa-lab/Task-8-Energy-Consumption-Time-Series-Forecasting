# Task-8-Energy-Consumption-Time-Series-Forecasting
Time series forecasting of household energy consumption using historical power usage data with ARIMA, Prophet, and XGBoost models.

## Objective
Forecast short-term household energy usage using historical time-based patterns. 
The goal is to help utilities and smart-home systems anticipate near-term demand — 
useful for load management, dynamic pricing, and demand-response programs.

## Dataset
[Individual Household Electric Power Consumption](https://archive.ics.uci.edu/dataset/235/individual+household+electric+power+consumption) 
(UCI Machine Learning Repository) — 2,075,259 minute-level measurements of electric 
power consumption for a single household in Sceaux, France.

> **Note:** The full dataset (~127 MB) is not included in this repo due to size. 
> Download it from the link above, unzip it, and place `household_power_consumption.txt` 
> in the project root before running the notebook.

## Approach
- Parsed the raw semicolon-separated file, combining `Date` + `Time` into a proper 
  datetime index and converting `?` missing markers to `NaN`
- Resampled the series from minute-level to **hourly** frequency and interpolated 
  remaining gaps
- Performed exploratory time series analysis — daily and weekly usage patterns, 
  full time series visualization
- Engineered time-based features: hour of day, day of week, weekend flag, month, 
  plus lag features (1h, 2h, 3h, 24h) and a 24-hour rolling mean
- Used a **time-based train/test split** (last 7 days held out) to avoid leaking 
  future information into training
- Trained and compared three forecasting approaches:
  - **ARIMA** — classical statistical baseline modeling the series' own past values
  - **Prophet** — additive model with explicit daily/weekly seasonality
  - **XGBoost** — gradient-boosted trees using the engineered calendar/lag features
- Evaluated all three models using **MAE** and **RMSE**, and visualized actual vs. 
  forecasted usage over the test week

## Results & Findings
- Clear daily seasonality (morning and evening usage peaks) and weekly seasonality 
  (higher weekend usage) are present in the data
- See the model comparison table in the notebook for exact MAE/RMSE — in general:
  - ARIMA is a strong lightweight baseline but struggles with multiple seasonalities
  - Prophet handles daily + weekly seasonality naturally with minimal tuning
  - XGBoost can outperform both when given good lag/calendar features, at the cost 
    of more feature engineering
- Since usage peaks predictably around breakfast and evening hours, utilities could 
  target time-of-use pricing or smart-appliance scheduling around these windows

## Tools & Libraries
Python · pandas · numpy · matplotlib · seaborn · statsmodels (ARIMA) · Prophet · 
XGBoost · scikit-learn (metrics)

## Author

**Samaa Shafqat**

Data Science & Analytics Internship Project
