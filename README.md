# Sales & Customer Analytics Dashboard
### End-to-End Tableau Project | Retail Superstore Dataset (2020–2023)

---

## Overview

An end-to-end business intelligence project analyzing **$2.3M in retail sales** across 4 years, 49 states, and 3 product categories. Built two interactive Tableau dashboards — Sales Performance and Customer Analysis — designed for executive and operational decision-making.

The project follows a structured BI development lifecycle: requirements analysis → data modeling → KPI development → dashboard build → interactivity and filtering.

---

## Business Problem

Retail stakeholders had no centralized view of performance across product categories, geographies, and customer segments. Key gaps:

- No visibility into **which sub-categories were generating losses** despite high sales volume (e.g., Tables: $206K revenue, $−17.7K profit)
- No way to compare **year-over-year trends** for Sales vs. Profit simultaneously
- **Discount strategy was unmeasured** — discounted orders were running at −2.9% margin vs. 29.5% for non-discounted orders
- Geographic performance was opaque — West vs. Central regions had a 2.7x profit gap on comparable revenue

---

## Dataset

| Table | Rows | Description |
|---|---|---|
| Orders | 9,994 | Fact table — sales transactions 2020–2023 |
| Customers | 793 | Customer master |
| Products | 1,862 | Product catalog with Category and Sub-Category |
| Location | 632 | Postal code → City → State → Region mapping |

**Data Model:** Star schema. Orders is the central fact table, joined to Customers (Customer ID), Products (Product ID), and Location (Postal Code).

**Date Range:** January 2020 – December 2023  
**Geographic Coverage:** 49 US states, 531 cities, 4 regions

---

## Key Metrics (Real, Computed from Source Data)

| Metric | Value |
|---|---|
| Total Sales (4-year) | $2,297,201 |
| Total Profit | $286,397 |
| Overall Profit Margin | 12.5% |
| Total Orders | 5,009 |
| Total Customers | 793 |
| Total Quantity Sold | 37,873 units |
| YoY Sales Growth (2022→2023) | +20.4% |
| YoY Profit Growth (2022→2023) | +14.2% |

**Category Breakdown:**

| Category | Sales | Profit | Margin |
|---|---|---|---|
| Technology | $836,154 | $145,455 | 17.4% |
| Furniture | $742,000 | $18,451 | 2.5% |
| Office Supplies | $719,047 | $122,491 | 17.0% |

**Regional Performance:**

| Region | Sales | Profit |
|---|---|---|
| West | $725,458 | $108,418 |
| East | $669,852 | $89,278 |
| Central | $501,240 | $39,706 |
| South | $400,651 | $48,994 |

**Discount Impact:**
- Discounted orders (5,196 rows): **−2.9% margin**
- Non-discounted orders (4,798 rows): **+29.5% margin**

---

## Dashboards Built

### 1. Sales Performance Dashboard

**Purpose:** Track top-line sales, profit, and quantity trends for management reporting.

**Components:**
- 3 KPI tiles: Total Sales, Total Profit, Total Quantity — each with YoY % change indicator and sparkline
- **Sales & Profit by Sub-Category** (horizontal bar chart) — dual-axis showing both metrics side-by-side, with loss-making sub-categories highlighted in orange
- **Trends Over Time** (dual-line chart) — monthly Sales and Profit on a shared time axis for 2020–2023

**Key Insight Surfaced:** Furniture's Tables sub-category generated $206K in sales but lost $17.7K in profit — driven by excessive discounting. Flagged for pricing strategy review.

---

### 2. Customer Dashboard

**Purpose:** Analyze customer distribution, purchase behavior, and segment-level contribution.

**Components:**
- Customer count, average sales per customer, average orders per customer KPIs
- Customer distribution by segment (Consumer, Corporate, Home Office)
- Top customers by revenue with profitability overlay

**Key Insight Surfaced:** Consumer segment drives 52% of order volume but Home Office customers have the highest average order value, suggesting upsell potential in that segment.

---

## Dashboard Features

- **Cross-dashboard navigation** — buttons switch between Sales and Customer dashboards seamlessly
- **Dynamic filters** — Category, Sub-Category, Region, City; all charts update on filter selection
- **Chart-as-filter interactivity** — clicking a sub-category on the bar chart filters the trend lines in real-time
- **Formatted tooltips** — contextual detail on hover (Sales, Profit, Margin %, YoY delta)
- **Fit Entire View** — dashboard scales to any screen without scroll

---

## Technical Implementation

**Tool:** Tableau Desktop  
**Data Connection:** CSV flat files (local extract)  
**Data Model:** Manually built star schema with 4 joins in Tableau's data source layer  

**Calculated Fields Built:**

```
// Year-over-Year Sales
(SUM([Sales]) - LOOKUP(SUM([Sales]), -1)) / ABS(LOOKUP(SUM([Sales]), -1))

// Profit Margin %
SUM([Profit]) / SUM([Sales])

// KPI Color Flag (positive/negative)
IF SUM([Profit]) < 0 THEN "Loss" ELSE "Profit" END
```

**Container Structure (Dashboard Layout):**
```
Vertical Container (Main)
├── Horizontal Container — Title + Navigation Buttons
├── Horizontal Container — KPI Tiles (3x BAN sheets)
└── Horizontal Container — Charts
    ├── Bar Chart (Sub-Category Performance)
    └── Vertical Container
        ├── Line Chart (Sales Trend)
        └── Line Chart (Profit Trend)
```

**Formatting Decisions:**
- Removed all grid lines and borders from chart sheets
- Axis labels cleaned — no redundant titles
- Color palette: Orange (#E8613C) for losses/negative delta, Blue (#4E79A7) for positive, Neutral grey for baseline
- Font: consistent sizing hierarchy (Title 16pt Bold → KPI value 24pt → labels 10pt)

---

## Project Workflow (4-Step Process)

```
Step 1: Analyse Requirements
  └── Defined user stories for sales managers and executives
  └── Selected chart types: BAN tiles, dual bar, dual-line, pie
  └── Drew mockups (hand-drawn → container wireframe)

Step 2: Build Data Source
  └── Connected 4 CSV files
  └── Built star schema joins
  └── Validated data types, renamed fields for clarity
  └── Verified row counts and date range integrity

Step 3: Build Charts
  └── Created calculated fields (YoY, Margin %, color flags)
  └── Built and formatted each chart sheet independently
  └── Applied consistent color coding and tooltip formatting

Step 4: Build Dashboard
  └── Built container structure (Vertical → Horizontal nesting)
  └── Dragged sheets into containers
  └── Added filter actions and navigation buttons
  └── Distributed objects evenly, applied padding
  └── Final QA: filter behavior, cross-sheet interaction, responsiveness
```

---

## Files

```
├── Sales___Customer_Dashboards.twbx   # Packaged Tableau workbook (includes data)
├── Customers.csv                       # Customer master data
├── Products.csv                        # Product catalog
├── Orders.csv                          # Transaction fact table
├── Location.csv                        # Geographic dimension
└── README.md                           # This file
```

---

## How to Open

1. Download `Sales___Customer_Dashboards.twbx`
2. Open with Tableau Desktop (version 2021.1+) or Tableau Public (free)
3. The workbook is self-contained — all data is packaged inside the `.twbx` file
4. Navigate between dashboards using the buttons in the top-right header

---

## Skills Demonstrated

`Tableau` `Star Schema Data Modeling` `Dashboard Design` `KPI Development` `Calculated Fields` `Table Calculations (YoY)` `Dashboard Actions & Filters` `Data Storytelling` `Container Layout` `Business Intelligence`

---

## Author

**Piyush Panthi**  
B.Tech AI Engineering | MITS Gwalior  
[LinkedIn](#) | [GitHub](#)
