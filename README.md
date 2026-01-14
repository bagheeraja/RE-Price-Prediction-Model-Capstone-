# Real Estate Price Prediction Model (Capstone)

This project is a proof-of-concept machine learning tool that predicts residential sale prices in King County, Washington, to support an instant-buying (iBuyer) workflow for a fictional brokerage, **Moving On Up Real Estate**.

## Overview

Using the Kaggle **House Sales in King County, USA** dataset, several supervised regression models are trained and evaluated to estimate single-family home prices.  
A simple notebook-based widget lets internal users input key property characteristics and receive an estimated sale price for quick, data-driven valuations.

## Data

- Source: Kaggle – *House Sales in King County, USA* (King County, WA home sales).  
- Target: `price` (sale price).  
- Features: bedrooms, bathrooms, living area, lot size, condition, grade, waterfront, view, above/below‑grade area, location (zipcode, lat/long), and neighborhood aggregates.  

The CSV file from Kaggle should be downloaded manually and placed next to the notebook.

## Methods

- Workflow: CRISP‑DM (business understanding → data understanding → preparation → modeling → evaluation → deployment).  
- Preprocessing: data inspection, invalid row removal (e.g., zero beds/baths), type and distribution checks, correlation analysis, log transforms for skewed numeric features.  
- Models: Linear Regression, Ridge, Lasso, KNN, Random Forest, SVR, Extreme Gradient Boosting (XGBoost), evaluated with MSE, RMSE, MAE, \(R^2\), and MAPE.  

Initial results show Gradient Boosting and SVR performing best, but still above the targeted 5% MAPE required for production iBuyer use.

## User interface

The Jupyter notebook includes a small internal-use widget (ipywidgets).

- Input: living area, above‑grade area, nearby average living area, bedrooms, bathrooms, construction grade, and waterfront flag.  
- Output: predicted sale price after clicking a **Predict** button.  

This is intended for a secure intranet, not public deployment.

## Quick start

1. Install Python 3 and Jupyter Notebook.  
2. Install dependencies:
   ```bash
   pip install numpy pandas matplotlib seaborn scikit-learn xgboost ipywidgets joblib

