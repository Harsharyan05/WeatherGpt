WeatherGPT — Model Evaluation and Prediction Analysis
Project: WeatherGPT — Conversational AI for Weather Forecasting, Alerts, and Climate Information
Model: Random Forest Regressor
Target: Next-hour temperature prediction (°C)
Evaluation: Chronological held-out test set
Command: python -m src.evaluate
1. Executive Summary
WeatherGPT's Random Forest model was evaluated on 26,280 held-out samples across Bengaluru, Chennai, Delhi, London, and Mumbai. It achieved MAE = 0.3744°C, RMSE = 0.5632°C, and R² = 0.99295.

Against a persistence baseline—which uses the current temperature as the next-hour estimate—the model reduced MAE from 0.6638°C to 0.3744°C, a relative improvement of 43.60%. 93.34% of predictions were within ±1°C of the observed next-hour temperature, and 99.05% were within ±2°C.

These results are strong for the evaluated dataset and test period, but they do not guarantee equivalent performance on future live weather, unseen cities, unusual weather events, or other forecast variables. The evaluation measures next-hour temperature prediction; it does not establish the accuracy of precipitation, severe-weather alerts, or every other weather variable.
2. Evaluation Setup
- Test samples: 26,280
- Cities: Bengaluru, Chennai, Delhi, London, Mumbai
- Samples per city: 5,256
- Prediction horizon: Next hour
- Target unit: Degrees Celsius
- Split: Chronological held-out test period, as implemented by the project evaluation script
- Baseline: Persistence prediction, using current temperature as the next-hour estimate
- Metrics: MAE, RMSE, R², median absolute error, mean error bias, error standard deviation, 90th/95th percentile absolute error, maximum absolute error, tolerance-based rates, and baseline comparison
This report describes the results printed by the supplied evaluation run. For reproducibility, retain the dataset version, feature-engineering code, model artifact, and metric files alongside the report.
3. Overall Test Results
Metric	Result	Interpretation
Test samples	26,280	Number of evaluated predictions
MAE	0.3744°C	Mean absolute difference between prediction and actual temperature
RMSE	0.5632°C	Penalizes larger errors more strongly than MAE
R²	0.99295	About 99.29% of target variance explained on this test set
Median absolute error	0.2529°C	Half of absolute errors were at or below this value
Mean error bias	-0.0376°C	Small average underprediction, with error defined as prediction minus actual
Error standard deviation	0.5619°C	Dispersion of signed errors as calculated by the evaluation script
90th percentile absolute error	0.8352°C	90% of absolute errors were at or below this value
95th percentile absolute error	1.1214°C	95% of absolute errors were at or below this value
Maximum absolute error	8.2363°C	Largest absolute error observed in this test set
Within ±0.5°C	75.53%	Share of predictions with absolute error no greater than 0.5°C
Within ±1°C	93.34%	Share of predictions with absolute error no greater than 1°C
Within ±2°C	99.05%	Share of predictions with absolute error no greater than 2°C
Baseline MAE	0.6638°C	MAE from persistence prediction
Baseline RMSE	0.9120°C	RMSE from persistence prediction
MAE improvement vs. baseline	43.60%	Relative reduction in MAE compared with persistence


Interpretation
- Typical error: MAE of about 0.37°C and median absolute error of about 0.25°C indicate that typical test predictions were close to observed temperatures.
- Tolerance rates: About three quarters of predictions were within half a degree, more than nine in ten were within one degree, and about 99% were within two degrees.
- Large-error tail: Maximum absolute error was 8.24°C. The P95 absolute error was 1.12°C, but larger misses remain possible and deserve investigation.
- Bias: Mean error bias was -0.038°C, indicating a small average underprediction in this test set. Near-zero mean bias does not mean every city or individual prediction is unbiased.
- Baseline comparison: The model outperformed the persistence baseline on both MAE and RMSE. The 43.60% figure is relative MAE reduction, not a classification-accuracy improvement.
4. City-Wise Results
City	Samples	MAE (°C)	RMSE (°C)	R²	Median AE (°C)	Bias (°C)	P90 AE (°C)	P95 AE (°C)	Max AE (°C)	Within ±1°C	Within ±2°C	Baseline MAE (°C)	MAE improvement
Bengaluru	5,256	0.3520	0.5329	0.96984	0.2352	+0.0172	0.7983	1.0822	4.1600	93.99%	99.16%	0.7163	50.85%
Chennai	5,256	0.4010	0.6444	0.95950	0.2516	-0.0462	0.9056	1.2344	8.2363	91.86%	98.17%	0.6364	36.99%
Delhi	5,256	0.4048	0.6167	0.99126	0.2582	-0.0972	0.9391	1.2898	7.1185	91.04%	98.93%	0.8033	49.62%
London	5,256	0.3729	0.5306	0.99230	0.2695	-0.0269	0.8113	1.0682	4.2939	94.03%	99.22%	0.5925	37.06%
Mumbai	5,256	0.3411	0.4741	0.96713	0.2494	-0.0351	0.7385	0.9408	5.3917	95.81%	99.75%	0.5703	40.19%


AE = absolute error; P90/P95 AE = 90th/95th percentile absolute error. Bias is prediction minus actual, as defined by the evaluation script.
City-level observations
- Mumbai has the lowest MAE (0.3411°C) and RMSE (0.4741°C); 95.81% of its predictions were within ±1°C.
- Bengaluru shows the largest MAE improvement over its baseline (50.85%).
- Chennai has the highest RMSE (0.6444°C) and the largest maximum absolute error (8.2363°C).
- Delhi has the highest MAE (0.4048°C) and most negative mean bias (-0.0972°C), indicating a small average underprediction in this test set.
- London has the highest city-wise R² (0.99230). R² should be read alongside absolute-error metrics because it depends on actual-temperature variability.
- MAE is lower than the persistence baseline in every listed city.
5. Prediction and Error Analysis
The evaluation suggests that most held-out next-hour temperature predictions are close to observed values. Percentiles add information beyond the average:
- Median absolute error: 0.253°C. Half of absolute errors were at or below this value.
- P90 absolute error: 0.835°C. Nine out of ten absolute errors were at or below approximately 0.84°C.
- P95 absolute error: 1.121°C. About 5% of absolute errors exceeded approximately 1.12°C.
- Maximum absolute error: 8.236°C. Rare large misses exist and should be reviewed.
Recommended follow-up for large-error cases:
1. Export rows with the largest absolute errors, including city, timestamp, actual temperature, prediction, and recent lag features.
2. Check for abrupt weather changes, missing or stale observations, API inconsistencies, and unusual conditions.
3. Plot residuals by time, city, month, hour, temperature range, and weather conditions.
4. Compare the model with persistence on the exact same test timestamps.
5. Evaluate on a later time period not used for model or feature selection.
The summary metrics alone do not identify the cause of any individual error.
6. Accuracy and R²: Correct Interpretation
This is a regression model, so it does not have classification accuracy in the usual sense. The percentages within ±0.5°C, ±1°C, and ±2°C are tolerance-based prediction rates, not classification accuracy.

R² = 0.99295 does not mean 99.295% of predictions are exactly correct. It describes the proportion of target variance explained relative to a mean-prediction reference on this test set.

For scientific reporting, present MAE and RMSE in °C, R², error percentiles, tolerance-based rates, and baseline comparison together.
7. Confidence Scores and Prediction Intervals
This evaluation did not calculate a calibrated confidence score or prediction interval. MAE, RMSE, R², and error percentiles are aggregate metrics; they do not provide the probability that a particular prediction is correct.

A recommended next step is to implement a documented uncertainty method, such as conformal prediction, using a separate calibration set. Evaluate it on separate test data and report:
- target coverage level (for example, 90% or 95%);
- empirical coverage;
- average and city-wise interval width;
- coverage by season, city, and weather regime.
Do not label a point prediction “95% confident” unless the score is clearly defined and validated. Any future interval should be evaluated for coverage and width on data not used to calibrate it.
8. Limitations and Validity Notes
1. Geographic scope: Results cover the five evaluated cities only; they do not establish performance in unseen cities or climates.
2. Forecast horizon: These metrics concern next-hour temperature. They do not establish seven-day ML performance or accuracy for rain, wind, humidity, or severe-weather alerts.
3. Historical evaluation: Held-out historical performance may differ from future live performance, especially during unusual or rapidly changing weather.
4. Data dependence: Results depend on the dataset, cleaning, feature engineering, target construction, and split logic used in this run.
5. Potential temporal leakage: Before publication, audit every feature to ensure it is available at the prediction timestamp. Verify lag construction, timestamps, target alignment, and whether any observations would be unavailable in live use.
6. Error extremes: The maximum absolute error shows that large misses remain possible.
7. No calibrated uncertainty: These metrics do not constitute per-prediction confidence scores or calibrated intervals.
8. No causal conclusions: The evaluation measures predictive performance; it does not explain why errors occur under particular conditions.
9. Reproducibility and Output Files
The evaluation run reported these outputs:
- results/metrics/comprehensive_metrics.json — overall held-out test metrics.
- results/metrics/city_wise_comprehensive_metrics.csv — city-wise metrics.
Run from the repository root with the virtual environment activated:
python -m src.evaluate
For reproducibility, record the model artifact version, dataset version or checksum, Python and package versions, evaluation date, and exact Git commit. Regenerate this report whenever the model or evaluation dataset changes.
10. Conclusion
On the reported chronological held-out test set, WeatherGPT's Random Forest achieved MAE 0.3744°C, RMSE 0.5632°C, and R² 0.99295 across 26,280 next-hour temperature predictions. It reduced MAE by 43.60% relative to persistence and placed 93.34% of predictions within ±1°C of observed temperature.

Performance by MAE/RMSE was strongest in Mumbai, while Chennai had the largest RMSE and maximum observed error. The results indicate promising historical next-hour temperature performance. Before making stronger reliability claims, investigate large errors, verify that there is no temporal leakage, test live-data behavior, and calibrate prediction uncertainty.
Reporting note: Numerical results in this report come from the evaluation output supplied for this run. They are not a guarantee of future performance and should be regenerated after material changes to data, features, or model code.
