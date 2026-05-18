# DATA_SPEC.md

## Project: NutriTrack KPI Dashboard
## Format: Spreadsheet (e.g., Google Sheets, Excel)
## Purpose: Track key performance indicators for user acquisition and revenue.

## Sheet Name: KPI_Dashboard

## Column Headers and Data Types:
- Date: Date (YYYY-MM-DD)
- New_Paying_Users: Integer
- Total_Paying_Users: Integer
- Monthly_Recurring_Revenue_MRR: Currency (e.g., $X.XX)
- Churn_Rate: Percentage (e.g., 0.05 for 5%)
- Customer_Acquisition_Cost_CAC: Currency (e.g., $X.XX)
- Lifetime_Value_LTV: Currency (e.g., $X.XX)

## Formula Definitions (Conceptual):
- Total_Paying_Users: Cumulative sum of New_Paying_Users minus churned users.
- Monthly_Recurring_Revenue_MRR: Total_Paying_Users * Average_Subscription_Price (assuming $9/user based on $4500 MRR / 500 users goal).
- Churn_Rate: (Number of churned users in period / Total paying users at start of period) * 100.
- Customer_Acquisition_Cost_CAC: Total marketing/sales spend in period / New_Paying_Users in period.
- Lifetime_Value_LTV: Average Revenue Per User (ARPU) * (1 / Churn_Rate).

## Sample Data (Illustrative):
Date,New_Paying_Users,Total_Paying_Users,Monthly_Recurring_Revenue_MRR,Churn_Rate,Customer_Acquisition_Cost_CAC,Lifetime_Value_LTV
2026-05-01,10,10,$90.00,0.00,50.00,90.00
2026-05-08,15,25,$225.00,0.00,40.00,90.00
2026-05-15,20,45,$405.00,0.00,35.00,90.00
2026-05-22,25,70,$630.00,0.00,30.00,90.00
2026-05-29,30,100,$900.00,0.00,28.00,90.00

## Formatting Guidelines:
- Dates: YYYY-MM-DD
- Currencies: Two decimal places, leading dollar sign.
- Percentages: Two decimal places.
