
***

## PROJECT_OVERVIEW.md (more detailed narrative)

```markdown
# Project Overview

This document summarizes the capstone project for C964 (Computer Science Capstone) and mirrors the narrative from the formal Task 2 submission.

## Problem and client

**Client:** Moving On Up Real Estate, a fictional brokerage operating in King County, Washington.  

The client wants to expand into direct seller purchases (iBuying), where homeowners receive fast, firm offers instead of following a traditional listing, showings, and long closing timeline.  
A key challenge is **valuation**: traditional appraisals, Broker Price Opinions, and desktop appraisals can be too slow, labor‑intensive, and often inconsistent or biased for an iBuyer model that depends on speed and volume.

## Proposed solution

The project delivers a **machine learning–based valuation tool** that predicts residential sale prices using historical transaction data.

- Train supervised regression models on King County sales data to estimate home prices based on physical characteristics, quality indicators, and location.  
- Deploy the best-performing model behind the company intranet as a simple prediction widget that staff can use to obtain quick internal pricing guidance.  

The long‑term goal is to reduce offer turnaround time, increase pricing accuracy, and support profitable acquisition decisions in the iBuyer segment.

## Data summary

- **Source:** Kaggle – *House Sales in King County, USA* dataset.  
- **Coverage:** One year of residential sales in King County, WA, with 21,613 records and 21 columns.  
- **Key fields:** price, bedrooms, bathrooms, living area, lot size, floors, waterfront, view, condition, grade, above/below‑grade area, year built, year renovated, zipcode, latitude, longitude, neighborhood averages for living area and lot size.  

### Processing and quality

- Initial inspection confirms no null values in this version of the dataset, but some clearly invalid entries (e.g., zero bedrooms and zero bathrooms) are removed.  
- Categorical and ordinal fields (waterfront, view, condition, grade, zipcode) are treated appropriately for modeling.  
- Correlation analysis identifies features most strongly associated with price, such as living area, above‑grade area, grade, and nearby living area.  
- Log transformations are applied to skewed numeric variables (including price and living area) to stabilize variance and improve model performance.  

Ethically, the dataset does not contain personal identifiers beyond an internal `id` column that cannot be traced to an actual homeowner; `id` is used for internal tracking but dropped prior to training.

## Methodology

Development follows **CRISP‑DM**, a standard process model for data mining and machine learning projects.

1. **Business understanding**  
   - Clarify the client’s goals (enter the iBuyer market, grow market share, maintain profitability).  
   - Identify how fast, consistent valuations can support conversions and competitive advantage.  

2. **Data understanding**  
   - Acquire and profile the dataset, checking formats, distributions, outliers, and potential data entry issues.  
   - Explore relationships via visualizations and correlations.  

3. **Data preparation**  
   - Clean and filter records (e.g., remove impossible bedroom/bathroom combinations).  
   - Engineer and transform features (log transforms, potential derived attributes such as age, price per square foot, etc.).  

4. **Modeling**  
   - Split the data into train and test sets (e.g., 80/20).  
   - Train multiple regression algorithms: Linear Regression, Ridge, Lasso, KNN, Random Forest, SVR, and Extreme Gradient Boosting.  
   - Scale/normalize inputs as needed and compare models on standard regression metrics.  

5. **Evaluation**  
   - Compare models using MSE, RMSE, MAE, \(R^2\), and MAPE to understand both absolute and relative error.  
   - For this use case, MAPE is emphasized to express error as a percentage and to align with a business target of ≤5%.  

6. **Deployment (prototype)**  
   - Wrap the selected trained model in a Jupyter notebook widget accessible on the company intranet.  
   - Staff can enter core features and obtain a predicted price to support acquisition decisions.  

## Implementation details

### Technology

- **Language:** Python 3.x.  
- **Environment:** Jupyter Notebook.  
- **Libraries:** pandas, numpy, seaborn, matplotlib, scikit‑learn, xgboost, ipywidgets, joblib.  

### Application behavior

- Loads and preprocesses the Kaggle King County dataset.  
- Trains multiple models and prints evaluation metrics for comparison.  
- At the end of the notebook, instantiates a prediction widget with text and dropdown inputs for key features and a **Predict** button that displays a price estimate.  

The prototype is intended as an internal tool and a technical demonstration, not a deployed consumer‑facing product.

## Evaluation and current performance

The model suite demonstrates that machine learning can capture a substantial portion of price variation, but the current best model (Extreme Gradient Boosting) still shows error above the desired business threshold.

- Example: \(R^2\) around 0.61 and MAPE around 27–28% in one configuration.  

This indicates that additional work is needed—more feature engineering, more aggressive outlier handling, and thorough hyperparameter tuning—to reach iBuyer‑grade performance (≤5% MAPE).

## Timeline and costs (high level)

The original capstone proposal outlines a multi‑month project schedule and a notional budget:

- **Timeline:** roughly 4 months from initial meetings to internal deployment, followed by ongoing quarterly monitoring and annual retraining aligned with assessor updates.  
- **Roles:** project manager, data scientist, and machine learning engineer.  
- **Costs:** itemized estimates for staff time, shared office space, workstations, and software (e.g., IDE licenses and version control), plus ongoing monitoring and retraining effort.  

These details are primarily relevant to the fictional client scenario, but they demonstrate how the technical work fits into a realistic business plan.

## Future work

Planned and recommended improvements include:

- More advanced feature engineering (e.g., age, price per square foot, distance to amenities).  
- Refined outlier treatment to focus on the price bands and property types targeted by iBuyers.  
- Systematic hyperparameter tuning using grid and randomized search.  
- Migration from notebook widget to a standalone web service (Flask/FastAPI) with a lightweight frontend.  
- Automated monitoring for drift and scheduled annual retraining when new assessor data is available.  
