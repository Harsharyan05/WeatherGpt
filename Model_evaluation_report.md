WeatherGPT — Model Evaluation: Main Points
- Model: Random Forest Regressor
- Prediction: Next-hour temperature forecasting.
- Test samples: 26,280 across five cities.
- MAE: 0.374°C.
- RMSE: 0.563°C.
- R² score: 0.99295.
- Within ±1°C: 93.34% of predictions.
- Within ±2°C: 99.05% of predictions.
- Baseline improvement: 43.60% lower MAE than the persistence model.
- Best-performing city by MAE/RMSE: Mumbai.
- Highest RMSE and maximum error: Chennai.
- Mean error bias: −0.038°C, indicating slight average underprediction.
- Maximum absolute error: 8.236°C.
- Confidence score: Not yet calculated; calibrated prediction intervals are future work.
- Future improvements: Investigate large errors, check for temporal data leakage, validate live predictions, and add calibrated uncertainty estimates.
Conclusion: WeatherGPT demonstrates strong historical next-hour temperature prediction performance, outperforming the persistence baseline across all five evaluated cities. These results do not guarantee equivalent performance on future live data.
