# Gold Return and Directional Predictability with Machine Learning

This repository contains the code used in the study *Gold Return and Directional Predictability with Machine Learning*.  
The project investigates whether **gold futures returns and price direction** can be forecast over short- to medium-term horizons using machine learning models and a broad set of financial, macroeconomic, and geopolitical predictors.

All models are evaluated under a **strict yearly walk-forward (fully out-of-sample) framework**, ensuring realistic forecasting conditions and preventing information leakage.

---

## Project Overview

The analysis evaluates gold futures return and directional predictability over **7-, 14-, 21-, and 28-day forecast horizons** using a **yearly walk-forward evaluation design**.

This framework closely mimics real-time forecasting conditions by ensuring that:
- models are trained only on past information,
- test data are strictly out-of-sample,
- and information leakage is avoided throughout preprocessing and model selection.

### Key Findings

- Gold return predictability is limited and highly **state-dependent**
- Directional predictability emerges primarily at the **28-day horizon**
- Predictability is stronger during periods of **market instability and frequent regime switching**
- **Ensemble methods** and **regime-aware modeling** provide economically meaningful improvements

---

## Methods

### Models

The following classes of models are implemented and compared:

- **Linear models**
  - Ridge Regression  

- **Tree-based ensembles**
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
> For exact replication, results should be generated using the datasets saved in the `data/` directory.

---

## Implementation Details

- Models are trained using a **rolling yearly walk-forward procedure**
- Each model is estimated using a **four-year rolling training window**
- Hyperparameter tuning and model comparison are conducted using the **PyCaret** framework with time-series-aware cross-validation
- Ensemble forecasts are constructed using:
  - **Averaging** for regression models
  - **Majority voting** for classification models
- Numerical results and figures are automatically exported for further analysis

---

## Execution Order

The project is implemented as a **single, self-contained Jupyter notebook**.  
All code must be executed **sequentially from top to bottom** to reproduce the results.

### Step 1 — Environment Setup
- Import required Python libraries
- Set global configuration options and random seeds

---

### Step 2 — Data Acquisition and Preprocessing
- Download gold futures (GC=F) and related financial series from Yahoo Finance
- Load the Geopolitical Risk (GPR) Index
- Align time series and handle missing values
- Save the final merged dataset to the `data/` directory

---

### Step 3 — Feature Construction and Target Definition
- Construct lagged financial, macroeconomic, and technical predictors
- Standardize and transform features where appropriate
- Construct return targets for 7-, 14-, 21-, and 28-day horizons
- Create binary directional labels
- Perform exploratory analysis (target–feature and feature–feature relationships)

---

### Step 4 — Regression Analysis

#### 4.1 Walk-Forward Evaluation
- Define yearly walk-forward splits
- Specify rolling four-year training windows
- Ensure all preprocessing is performed using training data only
- Train regression models using the PyCaret framework
- Perform time-series-aware three-fold cross-validation within each training window
- Generate out-of-sample return forecasts
- Save evaluation tables to the `result/` directory
- Generate figures of model–target \( R^2 \) over the full test period

#### 4.2 Ensemble Construction
- Combine individual model forecasts using averaging
- Evaluate all model combinations consisting of at least two models
- Identify ensemble combinations with improved predictive performance

#### 4.3 Regime-Based Analysis
- Compute yearly out-of-sample \( R^2 \) for each model and forecast horizon
- Identify periods of elevated predictability (e.g., 2018, 2022)
- Apply K-means clustering to classify daily market regimes
- Compute normalized entropy as a measure of regime instability
- Relate high regime-switching frequency to forecast performance
- Determine the optimal entropy threshold using the F1 score

---

### Step 5 — Classification Analysis

#### 5.1 Walk-Forward Evaluation
- Define yearly walk-forward splits
- Specify rolling four-year training windows
- Ensure all preprocessing is performed using training data only
- Train classification models using the PyCaret framework
- Perform time-series-aware three-fold cross-validation
- Generate out-of-sample directional forecasts
- Evaluate Accuracy and Balanced Accuracy
- Compare model performance against naïve benchmarks
- Save evaluation tables to the `result/` directory

#### 5.2 Ensemble Construction
- Combine individual classification models using majority voting
- Evaluate all ensemble combinations with at least two models
- Observe performance improvements, particularly for the 28-day horizon

---

> **Important:**  
> Cells must be run in order. Skipping or reordering cells may result in errors or inconsistent results.

---

## Repository Structure

```text
├── gold_prediction_code.ipynb   # Main notebook (full pipeline)
├── data/                        # Input datasets
├── result/                      # Exported tables and evaluation metrics
├── plot/                        # Exported figures
├── requirements.txt             # Python dependencies
└── README.md


