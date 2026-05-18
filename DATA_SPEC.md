# DATA_SPEC.md

## Project: My Business Financial Model
## Format: Excel Workbook (.xlsx)
## Purpose: Validate business model, track KPIs, project P&L and unit economics.

## Sheet: Assumptions
### Columns:
- Parameter (Text)
- Bear Case (Number)
- Base Case (Number)
- Bull Case (Number)
- Unit (Text)
### Sample Data:
- Monthly New Customers, 20, 25, 30, Customers
- Customer Acquisition Cost (CAC), 150, 125, 100, $
- Average Monthly Recurring Revenue (MRR) per Customer (ARPU), 18, 20, 22, $
- Monthly Churn Rate, 0.08, 0.05, 0.03, %
- Variable Cost per Customer, , 2, , $
- Sales & Marketing Spend, , 1500, , $
- Product Development, , 3000, , $
- General & Administrative, , 1000, , $

## Sheet: P&L Projection
### Columns:
- Month (Date)
- New Customers (Number)
- Total Customers (Number)
- Revenue (Currency)
- COGS (Currency)
- Gross Profit (Currency)
- Sales & Marketing (Currency)
- Product Development (Currency)
- General & Administrative (Currency)
- Total Operating Expenses (Currency)
- Net Income (Currency)
### Formula Definitions:
- Total Customers: Previous Month Total Customers * (1 - Churn Rate) + New Customers
- Revenue: Total Customers * ARPU
- COGS: Total Customers * Variable Cost per Customer
- Gross Profit: Revenue - COGS
- Total Operating Expenses: Sales & Marketing + Product Development + General & Administrative
- Net Income: Gross Profit - Total Operating Expenses

## Sheet: Unit Economics
### Columns:
- Metric (Text)
- Value (Number)
- Unit (Text)
### Formula Definitions:
- MRR: Total Customers * ARPU
- ARR: MRR * 12
- CAC: Customer Acquisition Cost (from Assumptions)
- LTV: ARPU * (1 - Variable Cost per Customer / ARPU) / Monthly Churn Rate
- LTV:CAC Ratio: LTV / CAC
- Payback Period: CAC / (ARPU - Variable Cost per Customer)

## Sheet: Sensitivity Analysis
### Columns:
- Scenario (Text)
- Parameter (Text)
- Change (%) (Number)
- Impact on Net Income (Currency)
### Formula Definitions:
- Impact on Net Income: (Net Income with changed parameter - Base Case Net Income)
