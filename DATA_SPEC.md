# DATA_SPEC.md

## Project: My Business Financial Model
## Format: Spreadsheet (e.g., Google Sheets, Excel)
## Purpose: Define key financial KPIs, quantify risks, and provide framework for business model validation.

## Sheet: Assumptions

### Description
This sheet will contain all the input variables and assumptions used in the financial model.

### Column Headers
- **Parameter**: String (e.g., "Customer Acquisition Cost", "Average Selling Price")
- **Value**: Number (e.g., 50, 100)
- **Unit**: String (e.g., "$", "units", "%")
- **Scenario (Bear)**: Number (e.g., 40, 80)
- **Scenario (Base)**: Number (e.g., 50, 100)
- **Scenario (Bull)**: Number (e.g., 60, 120)
- **Notes**: String (e.g., "Cost to acquire one new customer", "Price per unit sold")

### Sample Data
| Parameter                 | Value | Unit | Scenario (Bear) | Scenario (Base) | Scenario (Bull) | Notes                               |
|---------------------------|-------|------|-----------------|-----------------|-----------------|-------------------------------------|
| Customer Acquisition Cost | 50    | $    | 60              | 50              | 40              | Cost to acquire one new customer    |
| Average Selling Price     | 100   | $    | 90              | 100             | 110             | Price per unit sold                 |
| Cost of Goods Sold (COGS) | 30    | $    | 35              | 30              | 25              | Direct cost per unit sold           |
| Monthly Customers Acquired| 100   | units| 80              | 100             | 120             | New customers per month             |
| Churn Rate                | 5     | %    | 7               | 5               | 3               | Percentage of customers lost monthly|
| Operating Expenses        | 2000  | $    | 2200            | 2000            | 1800            | Fixed monthly expenses              |

## Sheet: Unit Economics

### Description
Calculates the profitability of a single unit or customer.

### Column Headers
- **Metric**: String (e.g., "Revenue per Unit", "COGS per Unit", "Gross Profit per Unit")
- **Value (Base)**: Number
- **Value (Bear)**: Number
- **Value (Bull)**: Number

### Formula Definitions (Logic)
- **Revenue per Unit**: `Assumptions!Average Selling Price`
- **COGS per Unit**: `Assumptions!Cost of Goods Sold (COGS)`
- **Gross Profit per Unit**: `Revenue per Unit - COGS per Unit`
- **Customer Lifetime Value (CLTV)**: `(Average Selling Price - COGS) * (1 / Churn Rate)` (simplified)
- **Payback Period**: `Customer Acquisition Cost / Gross Profit per Unit` (simplified)

## Sheet: P&L (Monthly)

### Description
Monthly Profit & Loss statement, projecting revenue, costs, and profit over time.

### Column Headers
- **Month**: Date (e.g., "2026-05", "2026-06")
- **Scenario**: String (e.g., "Bear", "Base", "Bull")
- **Customers (Start of Month)**: Number
- **New Customers**: Number (from Assumptions)
- **Churned Customers**: Number
- **Customers (End of Month)**: Number
- **Total Revenue**: Number
- **Total COGS**: Number
- **Gross Profit**: Number
- **Operating Expenses**: Number (from Assumptions)
- **Net Profit/Loss**: Number

### Formula Definitions (Logic)
- **Customers (Start of Month)**: Previous month's `Customers (End of Month)`
- **New Customers**: `Assumptions!Monthly Customers Acquired` (adjusted for scenario)
- **Churned Customers**: `Customers (Start of Month) * Assumptions!Churn Rate` (adjusted for scenario)
- **Customers (End of Month)**: `Customers (Start of Month) + New Customers - Churned Customers`
- **Total Revenue**: `Customers (End of Month) * Assumptions!Average Selling Price` (adjusted for scenario)
- **Total COGS**: `Customers (End of Month) * Assumptions!Cost of Goods Sold (COGS)` (adjusted for scenario)
- **Gross Profit**: `Total Revenue - Total COGS`
- **Operating Expenses**: `Assumptions!Operating Expenses` (adjusted for scenario)
- **Net Profit/Loss**: `Gross Profit - Operating Expenses`

## Sheet: KPIs

### Description
Key Performance Indicators derived from the financial model, tracked monthly or quarterly.

### Column Headers
- **KPI**: String (e.g., "Monthly Recurring Revenue", "Customer Acquisition Cost", "Gross Margin %")
- **Month 1 Value**: Number
- **Month 2 Value**: Number
- **Month 3 Value**: Number
- **Trend**: String (e.g., "Increasing", "Stable", "Decreasing")

### Formula Definitions (Logic)
- **Monthly Recurring Revenue (MRR)**: From `P&L (Monthly)!Total Revenue`
- **Customer Acquisition Cost (CAC)**: From `Assumptions!Customer Acquisition Cost`
- **Gross Margin %**: `(P&L (Monthly)!Gross Profit / P&L (Monthly)!Total Revenue) * 100`
- **Net Profit Margin %**: `(P&L (Monthly)!Net Profit/Loss / P&L (Monthly)!Total Revenue) * 100`
- **Customer Lifetime Value (CLTV)**: From `Unit Economics!Customer Lifetime Value`
- **CLTV:CAC Ratio**: `CLTV / CAC`
