# WeatherGPT — System Architecture

## 1. Overview

WeatherGPT is a machine-learning-based weather forecasting framework that processes historical meteorological data, performs feature engineering, trains multiple machine learning and deep learning models, evaluates their performance, and provides explainable predictions.

The overall ML pipeline is:

```mermaid
flowchart TD

    A["Historical Weather Data<br/>Open-Meteo"] --> B["Data Preprocessing"]

    B --> C["Exploratory Data Analysis<br/>EDA"]

    C --> D["Feature Engineering<br/>Lag Features<br/>Rolling Statistics<br/>Temporal Features"]

    D --> E["Chronological Data Split<br/>70% Train | 15% Validation | 15% Test"]

    E --> F["Classical Machine Learning"]

    F --> F1["Linear Regression"]
    F --> F2["Random Forest"]
    F --> F3["Support Vector Regression"]
    F --> F4["XGBoost"]

    E --> G["Deep Learning"]
    G --> G1["LSTM"]

    F1 --> H["Model Evaluation"]
    F2 --> H
    F3 --> H
    F4 --> H
    G1 --> H

    H --> I["MAE | RMSE | R²"]

    I --> J["Error Analysis"]

    J --> J1["Actual vs Predicted"]
    J --> J2["Residual Analysis"]
    J --> J3["Error Distribution"]

    J --> K["SHAP Explainability"]

    K --> K1["Feature Importance"]
    K --> K2["Feature Contributions"]
    K --> K3["Prediction Explanation"]

    K --> L["Final Weather Forecast"]
