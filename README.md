# Flight Price Prediction ✈️

## Overview
An end-to-end regression project in R predicting flight ticket prices from
route, airline, timing, and class features, using the Indian domestic flight
dataset (Business + Economy class, ~300K records).

## Methodology
- **Data:** Combined Business and Economy class datasets (`business.csv`,
  `economy.csv`), 300,261 rows total
- **Feature Engineering:**
  - Parsed flight duration text (e.g., "02h 15m") into numeric hours
  - Extracted weekday, weekend flag, and cyclical weekday features (sin/cos)
  - Bucketed arrival time into Morning / Afternoon / Evening / Night
  - Cleaned and simplified the "stops" category (non-stop / 1-stop / 2+ stops)
- **Feature Selection:**
  - Correlation analysis for numeric features vs. price
  - ANOVA testing for categorical features vs. price (airline, route, class,
    stop count, time of day all significant at p < .001)
  - Multicollinearity check via VIF
  - Stepwise regression and LASSO for final feature selection
- **Modeling:** trained and compared Linear Regression, Random Forest, and a
  Regression Tree (rpart, tuned via 5-fold cross-validation)

## Key Findings
- **Ticket class** is by far the strongest predictor of price (economy vs.
  business), followed by airline, stop count, and route
- Best model: **Random Forest** — RMSE ≈ 1,775, R² ≈ 0.785, MAE ≈ 1,171 on
  the validation set (vs. a mean-only baseline RMSE of ~3,824)
- Linear Regression achieved R² ≈ 0.734, Regression Tree R² ≈ 0.761

| Model | RMSE | R² | MAE |
|---|---|---|---|
| Linear Regression | 1,971.9 | 0.734 | 1,321.0 |
| **Random Forest** | **1,775.2** | **0.785** | **1,171.1** |
| Regression Tree | 1,867.9 | 0.761 | 1,255.2 |

## Files
- `lastone.html` — Full R analysis notebook (rendered from Quarto/R Markdown)

## Tools
R (tidyverse, caret, caretEnsemble, glmnet, xgboost, randomForest, rpart,
rpart.plot, car, skimr, GGally, lubridate)
