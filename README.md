# FBI Crime Investigation – Monthly Crime Incident Forecasting

**Author:** Vrushali Phaltane  
**Project type:** Time-Series Forecasting / Regression  
**Environment:** Python, Google Colab  
**Repository:** [FBI-Crime-Investigation-Monthly-Crime-Incident-Forecasting](https://github.com/vrushaliphaltane11-ctrl/FBI-Crime-Investigation-Monthly-Crime-Incident-Forecasting)

## Project Overview

This project analyzes historical crime incident records and forecasts monthly crime incident counts. It explores time-based trends and seasonality, then compares a seasonal-naive baseline, SARIMA, and XGBoost to identify a suitable forecasting approach. The analysis can inform public-safety planning and resource allocation; forecasts should not be treated as predictions of individual crimes.

## Problem Statement

Public-safety organizations need to understand historical patterns and estimate future crime volumes to support staffing, patrol scheduling, and resource planning. This project transforms incident-level records into a monthly time series and evaluates forecasting methods using a chronological validation period.

## Objectives

- Explore the dataset, inspect missing values and duplicates, and visualize crime trends.
- Aggregate incident records into monthly crime counts.
- Investigate seasonal patterns across months and crime categories.
- Build and evaluate Seasonal Naive, SARIMA, and XGBoost forecasting models.
- Generate a month-by-month forecast for 2012 and interpret XGBoost features.

## Dataset

The notebook describes the following data:

| Item | Description |
|---|---|
| Training file | `Train.xlsx` |
| Test file | `Test.csv` |
| Training records | 474,565 |
| Training features | 13 |
| Historical period | 1999–2011 |
| Test records | 162 |
| Test period | 2012–2013 |
| Crime categories | 9 |
| Monthly crime-category observations | 1,404 |

The original records include fields such as `TYPE`, `HUNDRED_BLOCK`, `NEIGHBOURHOOD`, latitude, longitude, year, month, day, hour, and minute. For the overall monthly forecasting models, the target is the **total incident count per month**.

> **Dataset availability:** `Train.xlsx` and `Test.csv` are required to rerun the notebook. They are uploaded manually in Colab. If the files are not included in this repository, obtain them from the authorized project dataset source before running. The notebook does not establish an external download link.

## Workflow

1. **Load data:** Upload `Train.xlsx` and `Test.csv` into Google Colab.
2. **Inspect quality:** Examine rows, data types, missing values, and duplicates.
3. **Aggregate incidents:** Group records by `YEAR`, `MONTH`, and `TYPE`, then derive overall monthly incident counts.
4. **Explore trends:** Plot historical counts, crime-type trends, monthly seasonality, and heatmaps.
5. **Build baseline:** Use a 12-month seasonal-naive forecast.
6. **Fit SARIMA:** Model the monthly time series with seasonal structure.
7. **Train XGBoost:** Use lagged counts, rolling means, and calendar features.
8. **Validate:** Compare model predictions against the final historical 12-month validation period (2011).
9. **Forecast:** Refit the selected XGBoost approach on available history and recursively forecast monthly totals for 2012.
10. **Interpret:** Examine feature importance and feature correlations.

## Technologies

- Python
- pandas and NumPy
- Matplotlib and Seaborn
- scikit-learn
- statsmodels (SARIMA / SARIMAX)
- XGBoost
- joblib and openpyxl
- Google Colab

## Forecasting Models

### Seasonal Naive

Uses the observed incident count from the same month of the previous year as the forecast. It provides a simple seasonal benchmark.

### SARIMA

A seasonal autoregressive integrated moving-average approach that models temporal dependence and seasonality in monthly crime counts.

### XGBoost

An ensemble regression model trained on engineered features, including:

- Lags: 1, 2, 3, 6, and 12 months
- Rolling means: 3, 6, and 12 months
- Calendar features such as month

The notebook also includes time-series-aware cross-validation and a hyperparameter search.

## Model Comparison

The following values are **reported in the notebook's model-comparison cell**:

| Model | MAE | RMSE | MAPE |
|---|---:|---:|---:|
| Seasonal Naive | 201.83 | 284.64 | 6.75% |
| SARIMA | 216.89 | 294.36 | 7.17% |
| **XGBoost** | **153.04** | **190.83** | **5.12%** |

**Finding:** XGBoost has the lowest reported errors in this comparison. These results reflect the notebook's historical validation setup, not independently verified future performance. Re-run the notebook to reproduce the metrics.

## Run the Notebook in Google Colab

1. Open the `.ipynb` notebook from this repository in Google Colab, or upload the notebook to Colab.
2. Run the dependency installation cell:

   ```python
   !pip install -q pandas numpy matplotlib seaborn scikit-learn statsmodels xgboost joblib openpyxl
   ```

3. Run the dataset upload cells and select `Train.xlsx` and `Test.csv`.
4. Confirm the files appear in `/content/` (the notebook expects `/content/Train.xlsx` and `/content/Test.csv`).
5. Select **Runtime → Run all** and review the charts, evaluation metrics, and forecasts.

**Note:** Colab session storage is temporary. Upload the input files again when starting a new session if they are no longer available.

## Outputs

The notebook produces:

- Data-quality summaries and missing-value visualizations
- Overall monthly crime incident trend charts
- Crime-type and monthly seasonality charts
- Actual-versus-predicted plots for forecasting models
- A model-comparison table
- A 2012 monthly incident forecast and historical-versus-forecast plot
- XGBoost feature-importance chart
- Feature-correlation matrix and heatmap

## Limitations

- The historical records end in 2011; the 2012 values are forecasts, not confirmed observed outcomes.
- The notebook's model comparison focuses on **overall monthly incident totals**, not separate forecasts for each crime category or neighborhood.
- Changes in crime reporting, policing, policy, population, and external conditions may affect forecast accuracy.
- A single historical validation period is not a guarantee of future performance.
- The repository name uses “FBI,” but the notebook alone does not verify that the source records are an official FBI dataset; check dataset provenance before making that claim publicly.

## Future Improvements

- Add rolling-origin backtesting over multiple years.
- Forecast individual crime categories and neighborhoods.
- Incorporate relevant external predictors, when available and appropriate.
- Add automated data validation and reproducible data-access instructions.
- Monitor forecast drift and refresh models as new observations become available.

## Conclusion

This project demonstrates an end-to-end workflow for converting historical incident records into a monthly forecasting problem. Among the three evaluated approaches, XGBoost reports the strongest validation metrics in the notebook. The resulting analysis is intended to support aggregate planning and should be interpreted with its data and modeling limitations in mind.

---

**Developed by Vrushali Phaltane**
