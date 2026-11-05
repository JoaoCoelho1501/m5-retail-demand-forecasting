# Retail Demand Forecasting — Walmart M5

A comparative time-series forecasting project evaluating statistical, machine-learning, deep-learning, and foundation models on a subset of the Walmart M5 dataset.

**Academic context:** MSc in Business Intelligence & Analytics, ISCAP (2025/26)  
**Authors:** Beatriz Teixeira and João Coelho

## Project overview

The objective is to forecast daily sales for **216 product series** from the **FOODS_1 department at store TX_1 (Texas)** over a **28-day horizon**. The experiment compares different model families under a shared chronological validation setup, using **Root Mean Squared Scaled Error (RMSSE)** as the primary metric.

This repository documents an academic benchmark on a selected subset of the M5 data; it is not a reproduction of the full competition.

## Experiment design

| Stage | Notebook(s) | Methods evaluated |
|---|---|---|
| 1. Statistical models | `01a_phase1_baselines.ipynb`, `01b_phase1_ets.ipynb`, `01c_phase1_arima.ipynb` | Naive and seasonal-naive baselines, historical average, AutoETS, AutoARIMA, AutoARIMAX |
| 2. Machine learning | `02_phase2_machine_learning.ipynb` | Linear/Ridge Regression, Random Forest, Extra Trees, XGBoost, LightGBM; univariate and multivariate approaches |
| 3. Deep learning and foundation models | `03_phase3_deep_learning.ipynb` | NHITS, LSTM, AutoNHITS, AutoLSTM, Chronos, TimeGPT, AutoGluon |

All model families are compared using the same forecast horizon and validation period. Lower RMSSE values indicate better performance.

## Selected validation results

| Model | Model family | RMSSE |
|---|---|---:|
| **AutoARIMAX** | Statistical | **0.7443** |
| AutoETS | Statistical | 0.7457 |
| TimeGPT (univariate) | Foundation model | 0.7470 |
| XGBoost (univariate) | Machine learning | 0.7498 |
| Seasonal Naive | Baseline | 0.9560 |

The complete results table is available in [`results/final_results.csv`](results/final_results.csv).

### Main finding

AutoARIMAX achieved the lowest RMSSE among the evaluated models. The result illustrates an important practical point: more complex architectures do not necessarily outperform well-specified statistical models, particularly when forecasting retail series with challenging demand patterns.

## Repository structure

```text
.
├── notebooks/
│   ├── 01a_phase1_baselines.ipynb
│   ├── 01b_phase1_ets.ipynb
│   ├── 01c_phase1_arima.ipynb
│   ├── 02_phase2_machine_learning.ipynb
│   └── 03_phase3_deep_learning.ipynb
└── results/
    └── final_results.csv
```

## Technology stack

- **Data analysis:** Python, pandas, scikit-learn
- **Statistical forecasting:** StatsForecast
- **Machine learning:** MLForecast, XGBoost, LightGBM
- **Deep learning:** NeuralForecast, PyTorch
- **Foundation models and AutoML:** Chronos, TimeGPT, AutoGluon
- **Environment:** Google Colab

## Reproducing the experiments

The notebooks were developed for Google Colab and expect the source data to be made available separately.

1. Download the required files from the [Kaggle M5 Forecasting Accuracy competition](https://www.kaggle.com/competitions/m5-forecasting-accuracy).
2. Upload or mount the dataset in Google Drive.
3. Update the dataset paths in the notebook configuration cells.
4. Run the notebooks in sequence, following the phase numbering.

**Optional API dependency:** the TimeGPT experiment requires a Nixtla API key. Store it in the `NIXTLA_API_KEY` environment variable; do not hard-code credentials in a notebook. The TimeGPT section can be skipped if the API is unavailable.

## Scope and limitations

- The analysis focuses on 216 product series from one department and one store.
- Results are specific to the selected validation period and experimental configuration.
- Re-running API-based or library-based models may produce different results depending on package versions, service availability, and model defaults.
- The reported metrics should be interpreted as an academic comparison on this subset, not as a claim about performance across the entire M5 competition dataset.
