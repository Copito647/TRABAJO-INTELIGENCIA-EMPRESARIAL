# TRABAJO-INTELIGENCIA-EMPRESARIAL
Credit Risk Scoring Project
Final project for Corporate Intelligent — UFV Madrid, May 2025.
The goal was to build a credit scoring system that predicts whether a bank customer will default within the next two years, and wrap it in something a non-technical person can actually use.

What's inside
├── notebook/Untitled10.ipynb       # full analysis (run in Google Colab)
├── data/give_me_some_credit.xlsx   # Kaggle dataset
├── dashboard/credit_risk_app.html  # standalone dashboard, no server needed
├── report/                         # written report (PDF)
└── charts/                         # Plotly visualisations

How to run
Dashboard — just open credit_risk_app.html in any browser.
Notebook — upload to Google Colab and run all cells, or locally:
bashpip install pandas numpy scikit-learn xgboost shap plotly openpyxl
jupyter notebook notebook/Untitled10.ipynb
Requires Python 3.9+.

Approach

Data: Give Me Some Credit (Kaggle) — 150k customers, 10 features, binary default target (6.7% positive rate)
ETL: missing value imputation, winsorisation at 99th percentile, feature engineering (TotalLatePayments, IncomePerDependent)
Clustering: K-Means (K=4) to find natural risk profiles — done blind, without the target variable
Models: Logistic Regression, Random Forest, Gradient Boosting — best AUC 0.867 with GB
Threshold: optimised to 0.09 using a 10:1 FN/FP cost matrix — recall goes from 19% to 70%
Explainability: SHAP values for individual predictions + global feature importance + fairness check by age group

Customers are segmented into four bands (Low / Medium / High / Very High) with a recommended APR and loan limit for each.

Dataset
Give Me Some Credit — publicly available on Kaggle. US historical data, so results shouldn't be used in production without retraining on local data.
