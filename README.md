# Gold Return and Directional Predictability with Machine Learning

This repository contains the code used in the study *Gold Return and Directional Predictability with Machine Learning*. The project investigates whether gold returns and price directions can be forecast over short- to medium-term horizons using machine learning models and a broad set of financial, macroeconomic, and geopolitical predictors.

## Project Overview

The analysis evaluates gold futures return and directional predictability over 7-, 14-, 21-, and 28-day horizons under a strict yearly walk-forward framework. This evaluation design ensures realistic, fully out-of-sample forecasting and prevents information leakage.

Key findings:
- Gold return predictability is limited and highly state-dependent.
- Directional predictability emerges primarily at the 28-day horizon.
- Predictability is stronger during periods of market instability and frequent regime switching.
- Ensemble methods and regime-aware modeling provide economically meaningful improvements.

## Methods

The following models are implemented and compared:

- **Linear models:** Ridge Regression  
- **Tree-based ensembles:** Random Forest, Extremely Randomized Trees  
- **Boosting methods:** Gradient Boosting, XGBoost, CatBoost  
- **Neural networks:** Multi-Layer Perceptron  

Return forecasts are evaluated using out-of-sample \(R^2\).  
Directional forecasts are evaluated using Accuracy, Balanced Accuracy, and skill scores relative to naïve benchmarks.

## Data

- Gold futures (GC=F) and related financial instruments are sourced from Yahoo Finance.
- The Geopolitical Risk (GPR) Index is obtained from Caldara and Iacoviello (2022).
- Daily data cover January 2010 to October 2025.

## Implementation

- Models are trained using a rolling yearly walk-forward procedure with four-year training windows.
- Hyperparameter tuning and evaluation are conducted using the **PyCaret** framework with time-series-aware cross-validation.
- Ensemble forecasts are constructed via averaging (regression) and majority voting (classification).


## Requirements

- Python 3.9+
- PyCaret
- scikit-learn
- pandas
- numpy
- matplotlib

## Notes

This repository is intended to support reproducibility of the empirical results reported in the paper. 

