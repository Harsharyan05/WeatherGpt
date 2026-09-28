# WeatherGPT 🌦️

### Hybrid Machine Learning Framework for Weather Forecasting, Explainability, and Conversational Weather Intelligence

WeatherGPT is a machine-learning-driven weather intelligence system designed to analyze historical meteorological data and forecast future weather conditions.

The project combines traditional machine learning, ensemble learning, and deep learning approaches to study weather forecasting performance. The system evaluates **Linear Regression, Random Forest, Support Vector Regression (SVR), XGBoost, and LSTM** under a common experimental framework.

A key component of the project is **explainable AI using SHAP**, which helps identify the meteorological features that contribute to model predictions.

The long-term objective is to connect the numerical forecasting layer with a conversational AI interface, allowing complex weather predictions and information to be presented in an understandable natural-language format.

---

## 🚀 Project Overview

Weather data is highly dynamic and depends on multiple interacting variables such as:

- Temperature
- Humidity
- Atmospheric pressure
- Precipitation
- Wind speed
- Wind direction
- Cloud cover
- Time and seasonal patterns

Traditional statistical approaches may struggle to capture complex nonlinear relationships between these variables.

WeatherGPT investigates whether modern machine learning and deep learning techniques can effectively model these relationships while maintaining an interpretable forecasting pipeline.

The project follows the pipeline:

```text
Historical Weather Data
        ↓
Data Preprocessing
        ↓
Exploratory Data Analysis
        ↓
Feature Engineering
        ↓
Chronological Data Split
        ↓
┌───────────────────────────────────┐
│       Machine Learning Models     │
│                                   │
│  Linear Regression                │
│  Random Forest                    │
│  SVR                              │
│  XGBoost                          │
└───────────────────────────────────┘
        ↓
     LSTM Model
        ↓
Model Comparison
        ↓
Error Analysis
        ↓
SHAP Explainability
        ↓
Forecasting Intelligence
        ↓
Conversational Weather Interface
