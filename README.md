# BI 360 – AtliQ Hardware Power BI Dashboard

## Business Problem

AtliQ Hardware grew rapidly worldwide, but its Latin America stores lost heavily because decisions rested on a random survey.  
Excel-based analysis could no longer support a global business or give leaders one trusted view.  
Rival Dell, with a large analytics team, made daily decisions from data, widening the gap.  
At its annual strategy meeting, AtliQ chose to adopt analytics for transparent, accurate decisions.  
BI 360 delivers this: one Power BI report for Finance, Sales, Marketing, Supply Chain and Executive teams.

---

An end-to-end business intelligence report built in Power BI for **AtliQ Hardware**, covering Finance, Sales, Marketing, Supply Chain and Executive views from a single semantic model (FY2018 – FY2025).

---

## Table of Contents

- [Business Problem](#business-problem)
- [Project Overview](#project-overview)
  - [Business Objective](#business-objective)
  - [Key Insights and Business Value](#key-insights-and-business-value)
  - [Tools and Technologies](#tools-and-technologies)
- [Report Pages](#report-pages)
  - [Executive](#1-executive)
  - [Finance](#2-finance)
  - [Sales](#3-sales)
  - [Marketing](#4-marketing)
  - [Supply Chain](#5-supply-chain)
- [Data Model](#data-model)
- [Forecast Accuracy](#forecast-accuracy-net-error-vs-abs-error)
- [FY2025 Highlights (Estimated)](#fy2025-highlights-estimated)
- [Getting Started](#repository-structure)
  - [Repository Structure](#repository-structure)
  - [How to Use](#how-to-use)

---

## Project Overview

| Item | Detail |
|---|---|
| Tool | Microsoft Power BI Desktop |
| Domain | Consumer hardware (PC, Peripherals & Accessories, Networking & Storage) |
| Period | FY2018 – FY2025 (FY2025 is estimated) |
| Model size | 37 tables, 110 measures |
| Grain | Date × Product × Customer |
| Dimensions | Customer, Product, Market, Date, Fiscal Year |
| Currency | Formatted in ₹ (measure names use "$") |

> **Note:** FY2025 figures are estimates, not final actuals, so FY2025 results and year-over-year comparisons with FY2024 are indicative.

**Business goal:** give each function a focused view of performance while keeping one consistent set of KPIs from gross sales to net profit and forecast quality.

---

## Business Objective

Give leadership and each function (Finance, Sales, Marketing, Supply Chain) one consistent view of performance, from gross sales to net profit and forecast quality, so they can find where profit is leaking and where planning is failing.

## Key Insights and Business Value

### 1. Growth is strong, but it is not turning into profit
- **Insight:** Net sales reached ₹19.4B (+61% YoY, about 3% above target) and GM is on target at 36.4%. Net profit is still -20.7%, because operating expenses (₹11.1B) exceed gross margin (₹7.05B) and deductions take about ₹19.5B from gross sales.
- **Business value:** The priority shifts from chasing revenue to controlling deductions and ads & promotions spend.

### 2. Profitability depends heavily on channel, customer and segment mix
- **Insight:** Retailers bring about 70% of sales but run at -26% net profit. Direct has the best GM (41.3%) and Distributors are nearest to break-even (-2.7%). Every segment is loss-making at net level, and AtliQ holds about 5.1% market share.
- **Business value:** Shows where to renegotiate terms, protect high-margin accounts and focus investment.

### 3. Forecasting has improved, but hidden errors still put margin at risk
- **Insight:** Accuracy rose from 68.1% (FY23) to an estimated 91.4% (FY25). Net Error is only +1.0M units, but ABS Error is 37.2M units, because over- and under-forecasts cancel out. LATAM is weakest at 69.4%.
- **Business value:** Fewer stock-outs and less excess inventory, with about ₹0.3B of margin at risk (an upper-bound estimate). Net Error shows direction (EI/OOS) and ABS Error shows the true size of the miss.

---

## Tools and Technologies

| Tool | How it was used |
|---|---|
| **MySQL (SQL)** | Source database for the customer, product, market, sales, forecast, cost and deduction tables |
| **Microsoft Excel** | Source files for market share and sales, gross margin and net profit targets |
| **Power Query (M)** | Data cleaning and transformation: merging tables, unpivoting, type changes and standardizing names |
| **Power BI Desktop** | Data modeling, relationships, report pages and visuals |
| **DAX** | Calculated measures for sales, margin, profit, year-over-year comparisons, market share and forecast accuracy |
| **Git and GitHub** | Version control and project documentation |

---

## Report Pages

> Page summaries are derived from the model's measures, parameter tables and FY2025 data (estimated).

### 1. Executive
Headline KPIs with year-over-year and target comparisons (Net Sales, GM %, Net Profit %), plus a **Division vs Channel** switch.
- Net sales grew 61% to ₹19.4B, about 3% above target.
- Operating expenses grew faster than sales (71%), so net profit fell to -₹4.0B (-20.7%).
- All divisions and channels lost profit margin; Retailers (70% of sales) lose the most.

### 2. Finance
P&L view with selectable rows and columns (current year, last year, change, targets, benchmarks).
- Gross Sales ₹38.8B → Net Sales ₹19.4B after pre- and post-invoice deductions
- COGS ₹12.3B (manufacturing ₹11.7B, freight ₹0.55B)
- Operating expenses ₹11.1B (ads & promotions ₹6.8B, other ₹4.2B)

### 3. Sales
Customer and product performance with top-5 country and product rankings and GM target status flags.
- Retailers contribute about 70% of net sales
- Direct channel has the highest GM (41.3%)
- Top customers: Amazon, AtliQ Exclusive, Atliq e Store, Sage, Leader

### 4. Marketing
Market share and segment/market performance (GM % vs Net Profit %) with switchable views.
- AtliQ market share about 5.1% (FY25, est.)
- Largest segments: Notebook, Peripherals, Desktop, Accessories
- Regions: APAC > NA > EU > LATAM

### 5. Supply Chain
Forecast vs actual sales quantity with accuracy, net error, absolute error, tolerance limits and EI/OOS risk.
- Forecast accuracy about 91.4% in FY25 (est.) vs 68.1% in FY23
- Weakest region: LATAM (69.4%)

---

## Data Model

**Fact tables**
- `fact_actuals_estimates` – quantities, sales, deductions, costs, margin
- `fact_forecast_monthly` – forecast quantity by date, product, customer

**Dimensions**
- `dim_customer`, `dim_product`, `dim_market`, `dim_date`, `fiscal_year`

**Cost and assumption tables**
- `manufacturing_cost`, `freight_cost`, `post_invoice_deductions`, `operational expense`

**Targets and benchmarks**
- `NsGmTarget`, `marketshare`

**Supporting tables**
- `Report Measures` (109 measures), `Tolerance Limit`, P&L row/column helpers, parameter tables for field switching (Sales, Marketing, Executive), `LastSalesMonth`, `Refresh Date`

---

## Forecast Accuracy: Net Error vs ABS Error

- **Net Error:** Forecast quantity minus actual sales quantity.
- **ABS Error:** The size of that gap in units, with the sign removed, added up at date and product level.
- **ABS Error %:** ABS Error as a share of forecast quantity.
- **Forecast Accuracy %:** 100% minus ABS Error %.
- **Risk flag:** EI (excess inventory) when Net Error is positive, OOS (out of stock) when it is negative.

| KPI | What it tells you |
|---|---|
| **Net Error** | Direction of the miss. Positive = over-forecast (EI), negative = under-forecast (OOS). |
| **ABS Error** | Magnitude of the miss in units, with the sign removed (at date × product level). |
| **Forecast Accuracy %** | `1 − ABS Error %`. Rises exactly as ABS Error % falls. |

**Key point:** Net Error can be near zero while ABS Error is large, because over- and under-forecasts cancel out. Even at high accuracy (for example 94%), a business can still face both out-of-stock and excess-inventory situations.

| FY | Forecast (M) | Actual (M) | Net Error (M) | ABS Error (M) | Accuracy |
|---|---|---|---|---|---|
| 2022 | 86.8 | 106.0 | -19.2 | 26.0 | 70.1% |
| 2023 | 193.3 | 172.5 | +20.8 | 61.6 | 68.1% |
| 2024 | 275.0 | 276.0 | -0.9 | 25.1 | 90.9% |
| 2025 (est.) | 432.6 | 431.6 | +1.0 | 37.2 | 91.4% |

---

## FY2025 Highlights (Estimated)

- Net Sales ₹19.37B (+61% YoY), Gross Margin 36.4%
- Net Profit -₹4.01B (-20.7%), driven by operating expenses (₹11.1B) exceeding gross margin (₹7.05B)
- Forecast accuracy 91.4%, ABS Error 37.2M units, Net Error +1.0M units
- Accuracy by region: EU 91.7%, APAC 87.0%, NA 83.8%, LATAM 69.4%
- ABS Error units rose about 48% YoY while ABS Error % fell, because forecast volume grew about 57%

---

## Repository Structure

```
Chapter_15_Power_BI_Dashboard/
├── BI 360 New.pbix        # Power BI report
├── README.md              # This file
└── docs/
    └── screenshots/       # Add page screenshots here
```

---

## How to Use

1. Clone the repository.
2. Open `BI 360 New.pbix` in **Power BI Desktop**.
3. To refresh the report with your own data, update the source paths under **Transform data → Data source settings** (the original source files are not provided).
4. Use slicers and parameter selectors on each page to switch views.

---

## Author

@galibmulani
Aspiring Data Analyst
Linkedin: https://www.linkedin.com/in/galib-mulani-5005aa184/
