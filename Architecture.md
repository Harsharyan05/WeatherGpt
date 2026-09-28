┌──────────────────────────────────────────────────────────────┐
│                    WEATHER DATA SOURCE                       │
│                                                              │
│                    Open-Meteo Historical Data                │
│                                                              │
│ Temperature | Humidity | Pressure | Rainfall | Wind | Cloud │
└─────────────────────────────┬────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────┐
│                 DATA PREPROCESSING LAYER                     │
│                                                              │
│  • Missing Value Handling                                    │
│  • Duplicate Removal                                         │
│  • Timestamp Processing                                      │
│  • Data Validation                                           │
│  • Outlier / Invalid Value Checking                          │
└─────────────────────────────┬────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────┐
│                 EXPLORATORY DATA ANALYSIS                    │
│                                                              │
│  • Statistical Analysis                                      │
│  • Distribution Analysis                                     │
│  • Correlation Analysis                                      │
│  • Time-Series Visualization                                 │
│  • Missing Data Analysis                                     │
└─────────────────────────────┬────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────┐
│                  FEATURE ENGINEERING                         │
│                                                              │
│  Original Features                                           │
│          +                                                   │
│  Lag Features                                                │
│          +                                                   │
│  Rolling Statistics                                          │
│          +                                                   │
│  Temporal Features                                           │
│                                                              │
│  → Final Feature Matrix                                      │
└─────────────────────────────┬────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────┐
│                CHRONOLOGICAL DATA SPLIT                      │
│                                                              │
│        ┌────────────┐  ┌────────────┐  ┌────────────┐        │
│        │   TRAIN    │  │ VALIDATION │  │    TEST    │        │
│        │    70%     │  │    15%     │  │    15%     │        │
│        └────────────┘  └────────────┘  └────────────┘        │
│                                                              │
│             No random shuffling                              │
└─────────────────────────────┬────────────────────────────────┘
                              │
                 ┌────────────┴────────────┐
                 │                         │
                 ▼                         ▼
      ┌─────────────────────┐   ┌─────────────────────┐
      │  CLASSICAL ML LAYER  │   │ DEEP LEARNING LAYER │
      └──────────┬──────────┘   └──────────┬──────────┘
                 │                         │
       ┌─────────┼─────────┐               │
       │         │         │               │
       ▼         ▼         ▼               ▼
    Linear    Random      SVR             LSTM
   Regression  Forest
       │         │         │               │
       └─────────┼─────────┘               │
                 │                         │
                 ▼                         ▼
              XGBoost                Sequential
             (Primary)                Forecasting
                 │                         │
                 └──────────┬──────────────┘
                            │
                            ▼
              ┌──────────────────────────┐
              │    MODEL EVALUATION      │
              │                          │
              │  • MAE                   │
              │  • RMSE                  │
              │  • R²                    │
              └────────────┬─────────────┘
                           │
                           ▼
              ┌──────────────────────────┐
              │     ERROR ANALYSIS       │
              │                          │
              │ • Actual vs Predicted    │
              │ • Residual Analysis      │
              │ • Error Distribution     │
              └────────────┬─────────────┘
                           │
                           ▼
              ┌──────────────────────────┐
              │   SHAP EXPLAINABILITY    │
              │                          │
              │ Feature Contributions    │
              │ Feature Importance       │
              │ Prediction Explanation   │
              └────────────┬─────────────┘
                           │
                           ▼
              ┌──────────────────────────┐
              │      FINAL FORECAST      │
              │                          │
              │ Future Temperature       │
              │ / Weather Prediction     │
              └──────────────────────────┘
