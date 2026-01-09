# Gold Return and Directional Predictability with Machine Learning

This repository contains the code used in the study *Gold Return and Directional Predictability with Machine Learning*.  
The project investigates whether **gold futures returns and price direction** can be forecast over short- to medium-term horizons using machine learning models and a broad set of financial, macroeconomic, and geopolitical predictors.

The primary goal is to assess whether modern machine learning methods can uncover economically meaningful predictive signals in gold prices when evaluated under a **strict, fully out-of-sample framework**.

---

## Project Overview

The analysis evaluates gold futures return and directional predictability over **7-, 14-, 21-, and 28-day forecast horizons** using a **yearly walk-forward evaluation design**.

This framework closely mimics real-time forecasting conditions by ensuring that:
- models are trained only on past information,
- test data are strictly out-of-sample,
- and information leakage is avoided throughout preprocessing and model selection.

### Key Findings

- Gold return predictability is generally limited and highly **state-dependent**
- Directional predictability emerges primarily at the **28-day horizon**
- Predictability is stronger during periods of **market instability and frequent regime switching**
- **Ensemble methods** and **regime-aware modeling** provide economically meaningful improvements relative to individual models

---

## Methods

### Models

The following classes of models are implemented and compared:

- **Linear models**
  - Ridge Regression  

- **Tree-based ensemble models**
  - Random Forest  
  - Extremely Randomized Trees (Extra Trees)  

- **Boosting methods**
  - Gradient Boosting  
  - XGBoost  
  - CatBoost  

- **Neural networks**
  - Multi-Layer Perceptron (MLP)  

### Forecast Tasks and Evaluation

Two prediction tasks are considered at each forecast horizon:

1. **Return prediction**  
   - Continuous cumulative returns  
   - Evaluated using out-of-sample \( R^2 \)

2. **Directional prediction**  
   - Binary up/down price movement  
   - Evaluated using Accuracy, Balanced Accuracy, and skill scores relative to naïve benchmarks

---

## Data

- **Gold futures:** GC=F (Yahoo Finance)
- **Financial and macroeconomic predictors:** Yahoo Finance
- **Geopolitical Risk (GPR) Index:** Caldara and Iacoviello (2022)
- **Frequency:** Daily
- **Sample period:** January 2010 – October 2025

> Note: Yahoo Finance data may be revised over time.  
> For exact replication, results should be generated using the datasets provided in the `data/` directory.

---

## Implementation Details

- Models are trained using a **rolling yearly walk-forward procedure**
- Each model is estimated using a **four-year rolling training window**
- Hyperparameter tuning and model comparison are conducted using the **PyCaret** framework with time-series-aware cross-validation
- Ensemble forecasts are constructed using:
  - **Averaging** for regression models
  - **Majority voting** for classification models
- Results and figures are automatically exported for further analysis

---

## Repository Structure

```text
├── gold_prediction_code.ipynb   # Main notebook (full pipeline)
├── data/                        # Input datasets
├── result/                      # Exported ML traning results
├── plot/                        # Exported figures
├── requirements.txt             # Python dependencies
└── README.md
