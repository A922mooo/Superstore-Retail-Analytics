# Superstore Retail Analytics

## Business Problem

A multinational retail company needs an automated analytical solution to monitor sales,
profitability, customer behavior, and operational performance across its US Superstore
operations (2016-2019).

## Objectives

- Clean and validate the raw Orders/People/Returns dataset
- Engineer analysis-ready features (margin, shipping duration, order-value tiers, etc.)
- Build a reusable KPI framework with correct grain handling (order vs. line-item vs. customer)
- Produce 12 professional visualizations answering specific business questions
- Generate an automated HTML report and cleaned data exports

## Dataset

`Sample - Superstore 2019.xls` -- 3 sheets: Orders (9,994 rows, 21 columns),
People (4 rows), Returns (800 rows, 296 unique Order IDs).

## Tools & Technologies

Python, Pandas, NumPy, Matplotlib, Seaborn, Jupyter Notebook.

## Methodology

`DataProcessor` (load/audit/clean/validate) -> `FeatureEngineer` (feature creation) ->
`SalesAnalyzer` (KPIs and aggregation) -> `Visualizer` (chart rendering) ->
`ReturnsAnalyzer` (return-rate analysis) -> `ReportGenerator` (export and HTML assembly).

## Data Cleaning

- Postal Code: 11 missing values, converted to a nullable string type, left unimputed
  (no external ZIP source used) and excluded from modeling
- Country/Region: retained for audit transparency (constant, 1 unique value), excluded from modeling
- 8 repeated Order ID + Product ID combinations (16 rows) flagged, not removed -- legitimate repeat line items
- 0 full duplicate rows found

## Feature Engineering

Profit Margin, Shipping Duration, Sales Performance Category (order-level quartiles of
summed Sales per Order ID), Order Year/Month/Quarter/Year-Month, Profitability Category
(Loss/Break-even/Profit), Discount Band (data-driven bins over the observed discount
values), and `is_deep_discount` (Discount >= 0.5).

## KPIs

| KPI | Value |
|---|---|
| Total Sales | $2,297.2k |
| Total Profit | $286.4k |
| Overall Profit Margin | 12.5% |
| Total Orders | 5,009 |
| Total Customers | 793 |
| Average Order Value | $458.61 |
| Average Shipping Duration | 3.96 days |
| Loss-Making Order % | 20.4% |
| Best Performing Category | Technology |
| Worst Performing Sub-Category | Tables |

## Exploratory Data Analysis

12 visualizations (8 core + 4 optional) covering time trends, category/region/segment
performance, sub-category profitability, discount-vs-profit, shipping duration
distribution, correlation analysis, top customers, order-value tier distribution, and
return-rate-by-region.

## Statistical Analysis

Descriptive statistics and a Pearson correlation matrix across Sales, Quantity, Discount,
Profit, Profit Margin, and Shipping Duration. Strongest relationship observed: Discount vs.
Profit Margin (r = -0.86) -- an association, not a proven causal effect.

## Key Findings

- Profit grew 88.6% from 2016 to 2019, outpacing sales growth of 51.4%; overall margin rose from 10.2% to 12.7%.
- Furniture accounts for 32.3% of sales but only 6.4% of profit -- the largest revenue/profit mismatch among the three categories.
- Tables is the largest loss-making sub-category at $-17.7k.
- West leads all regions in profit at $108.4k.
- Central shows lower profit ($39.7k) than South ($46.7k) despite higher sales ($501.2k vs $391.7k).
- Discount shows a strong negative association with Profit Margin (r = -0.86), far stronger than with raw Profit.
- West shows the highest return rate at 11.7%, well above the other three regions.
- Shipping duration follows the implied Ship Mode hierarchy: Same Day is fastest (median 0 days) and Standard Class is slowest (median 5 days).

## Business Recommendations

1. Review discounting policy in Furniture, with particular attention to Tables.
2. Investigate the drivers of West's elevated return rate before it further erodes regional profit.
3. Use Profit Margin, not raw Profit, as the primary metric when evaluating future discounting or pricing changes.

## Project Structure

```
project/
├── data/
│   ├── raw/Sample - Superstore 2019.xls
│   └── processed/cleaned_superstore.csv
├── notebooks/superstore_analysis.ipynb
├── figures/ (12 PNGs)
├── reports/analytical_report.html
├── outputs/cleaned_superstore.csv, kpi_summary.csv
├── README.md
└── requirements.txt
```

## How to Run

1. Install dependencies: `pip install -r requirements.txt`
2. Place the source file at `data/raw/Sample - Superstore 2019.xls`
3. Run `notebooks/superstore_analysis.ipynb` top to bottom
4. Outputs are written to `figures/`, `outputs/`, and `reports/`

## Outputs

- `outputs/cleaned_superstore.csv` -- final feature-engineered, memory-optimized dataset
- `outputs/kpi_summary.csv` -- all computed KPIs
- `figures/*.png` -- 12 visualizations at 150 DPI
- `reports/analytical_report.html` -- offline, self-contained analytical report

## Skills Demonstrated

Data cleaning and validation, reusable OOP pipeline design, feature engineering with
explicit grain discipline (order vs. line-item vs. customer), KPI framework design,
correlation and descriptive statistics, professional data visualization, automated
reporting, exception handling, and memory optimization.
