# Global Mart Sales Performance Analysis Report

> **A 5-page interactive Power BI report that dissects the sales, profitability, product mix, regional distribution, and customer behaviour of a fictional global retail company — "Global Mart" — giving decision-makers a single source of truth for performance insights.**

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [File Details](#2-file-details)
3. [Data Sources & Model](#3-data-sources--model)
4. [Report Pages — What Each One Tells You](#4-report-pages--what-each-one-tells-you)
   - [Page 1 — Sales Overview](#page-1--sales-overview)
   - [Page 2 — Product Analysis Dashboard](#page-2--product-analysis-dashboard)
   - [Page 3 — Regional Analysis](#page-3--regional-analysis)
   - [Page 4 — Customer Analysis](#page-4--customer-analysis)
   - [Page 5 — Executive Analysis](#page-5--executive-analysis)
5. [Measures & Calculated Fields](#5-measures--calculated-fields)
6. [Filters & Slicers](#6-filters--slicers)
7. [Custom Visuals Used](#7-custom-visuals-used)
8. [Key Insights Embedded in the Report](#8-key-insights-embedded-in-the-report)
9. [Recommendations (from the Executive Page)](#9-recommendations-from-the-executive-page)
10. [How to Open & Use the Report](#10-how-to-open--use-the-report)

---

## 1. Project Overview

**Global Mart Sales Performance Analysis** is a business intelligence project built in Microsoft Power BI. It was created to answer one central question:

> *How is Global Mart performing commercially — and where should leadership focus their energy to grow revenue, protect margins, and fix weak spots?*

The report is structured as a progressive narrative:

- It starts broad (**Sales Overview** — the big numbers),
- drills into products (**Product Analysis** — what sells and what doesn't),
- maps geography (**Regional Analysis** — where the money comes from),
- examines order-level behaviour (**Customer Analysis** — how customers buy),
- and ends with a strategic synthesis (**Executive Analysis** — patterns, comparisons, and recommendations).

Each page is self-contained but cross-filters with the others, so a selection on one visual ripples across the entire report.

---

## 2. File Details

| Property | Value |
|---|---|
| **File name** | `global_mart_sales_performance_analysis_report.pbix` |
| **File size** | ~4.4 MB |
| **Tool** | Microsoft Power BI Desktop |
| **Theme** | Tidal (built-in Power BI theme) |
| **Report pages** | 5 |
| **Custom visuals** | 6 (including flow map, tile map, icon array, change chart) |
| **Primary data table** | `GlobalMart_Sales_Data` |
| **Supporting table** | `Date` (calendar / date dimension) |

---

## 3. Data Sources & Model

The report is built on two core tables:

### `GlobalMart_Sales_Data` — The Fact Table
This is the transaction-level sales table. Each row represents a line item on an order. Key columns include:

| Column | Description |
|---|---|
| `Order ID` | Unique identifier for each order |
| `Order Date` | Date the order was placed |
| `Product Name` | Name of the individual product |
| `Category` | High-level product grouping (e.g. Technology, Furniture, Office Supplies) |
| `Sub-Category` | Finer product grouping within a Category |
| `Region` | Sales region (e.g. West, East, Central, South) |
| `State` | US state of the customer |
| `Discount` | Discount fraction applied to the order line |
| `Sales` | Revenue generated on the line item |
| `Profit` | Profit earned on the line item |
| `Quantity` | Units ordered |

### `Date` — The Calendar Dimension
A standard date table linked to `Order Date`, enabling time intelligence. Columns used in the report:

| Column | Description |
|---|---|
| `Day` | Day of month |
| `Month` | Month name / number |
| `Quarter` | Q1–Q4 |
| `Year` | Calendar year |

The two tables are related on `Order Date` → `Date[Date]`, enabling all time-based filtering and the year-over-year comparison measure (`SamePeriodLastYear`).

---

## 4. Report Pages — What Each One Tells You

---

### Page 1 — Sales Overview

**Purpose:** Give every user — from analyst to executive — an immediate pulse check on the business.

**What you see:**
- A **KPI card strip** at the top showing the five most important headline numbers:
  - Total Sales
  - Total Profit
  - Profit Margin %
  - Average Discount per Order
  - Average Sales per Order
- An **area chart** showing Total Sales by Day — useful for spotting intra-month peaks and troughs
- A second **area chart** filtered to a specific period for closer examination of daily sales patterns
- A **line chart** tracking Total Profit by Quarter — showing how profitability ebbs and flows through the year
- A **scatter chart** titled *"Sum of Discount and Total Profit by Sub-Category and Category"* — this is one of the most diagnostic visuals in the report. Each bubble is a sub-category; size represents discount given; position shows whether that discount translated into profit or ate into it
- A **Sales by Region** card — a single-number callout for the selected region
- A **month slicer** (custom calendar visual) for drilling into specific months

**Slicers on this page:** Year, Quarter, Region

**The question this page answers:** *"Are we growing, are we profitable, and is our discounting strategy working?"*

---

### Page 2 — Product Analysis Dashboard

**Purpose:** Understand the product portfolio — which products drive volume, which drive profit, and which are dragging performance.

**What you see:**
- A **horizontal bar chart** — Sub-Categories ranked by Total Orders (volume leaders)
- A **pie chart** — Sales split by Category (Technology vs Furniture vs Office Supplies share of revenue)
- A **line chart** titled *"Sales Trend by Product Over Time"* — tracks how individual product sales move across the order date axis, useful for spotting growth or decline
- A **bar chart** — Top products by Total Profit (the most *valuable* products, not just the most sold)
- A **treemap** — Sub-Categories coloured and sized by Average Discount — reveals where discounting is heaviest
- A **bar chart** — Top products by Total Sales (most *revenue-generating* products)
- **Two callout cards** showing the best-performing Product Name and Sub-Category for the current filter context
- **Two alert cards** for:
  - **Slow Moving Product Sales** — highlights products not shifting inventory
  - **Late Shipments** — flags fulfilment problems

**Slicers on this page:** Year, Quarter, Region, Sub-Category

**The question this page answers:** *"What are we selling, what's making money, and what's sitting on shelves?"*

---

### Page 3 — Regional Analysis

**Purpose:** Map commercial performance geographically to understand where sales are concentrated, where discounts are being given away, and how regions compare.

**What you see:**
- A **clustered bar chart** titled *"Sales as per Region"* — shows Total Sales and Total Profit side-by-side for each region, making margin differences immediately obvious
- A **clustered bar chart** — Average Discount by Region — reveals which regions are being discounted most aggressively
- A **custom map visual** (MapBySquillion) — plots Total Sales by State across the US, with region colouring — the most geographic view in the entire report
- A **donut chart** — Share of total discount spend by Region — answers the question: which region gets the most discount?
- Slicers for **Region**, **State**, and **Product Name** allow drilling all the way to a specific product in a specific state

**Slicers on this page:** Year, Quarter, Region, State, Product Name

**The question this page answers:** *"Which regions are our growth engines, which are discount-dependent, and which states are underperforming?"*

---

### Page 4 — Customer Analysis

**Purpose:** Examine buying patterns at the order and product level — connecting customer behaviour to sales and profitability outcomes.

**What you see:**
- The **KPI card strip** (same five headline metrics as Page 1, but now filtered by the customer-level slicers on this page)
- A **line chart** titled *"Sales Trend over Time"* — Total Sales plotted against Order Date, showing the full sales trajectory
- A **pie chart** titled *"Product Category Sales Distribution"* — uses a `Sales Contribution by Category %` measure to show each category's share as a proportion, not an absolute
- A **bar chart** titled *"Best Selling Products"* — the top products by Total Sales for the current filter context
- A **scatter chart** titled *"Discount vs Profitability Impact"* — plots Discount (x-axis) against Profit (y-axis) at the order level, making visible the negative correlation between deep discounting and profitability
- A **transaction table** with columns: Order ID, Order Date, Total Sales, Total Quantity — allows row-level inspection of specific orders

**Slicers on this page:** Region, Quarter, Year, Order ID (search by specific order)

**The question this page answers:** *"How do customers buy, which products do they buy most, and are discounts winning business or destroying margin?"*

---

### Page 5 — Executive Analysis

**Purpose:** Synthesise everything into strategic-level insight for senior decision-makers. This page goes beyond what happened to explain *why* it happened and *what to do about it*.

**What you see:**
- A **decomposition tree** — breaks down Total Sales hierarchically by Region → Category → Sub-Category → State, allowing executives to trace exactly which combination of factors is driving or dragging total revenue
- A **line chart** titled *"Sales Trend – Last 3 Months of the Year"* — plots `SamePeriodLastYear` (a time-intelligence measure) to compare current Q4 performance against the same period last year
- A **KPI card strip** (Total Profit, Total Sales, Avg Discount per Order)
- A second **KPI card strip** with operational metrics: Total Orders, Total Products, Total Quantity, Profit Margin%
- A **clustered bar chart** titled *"Most Profitable Category"* — ranks categories by Total Profit
- A **clustered bar chart** titled *"Discounts by Region"* — shows discount volume by region, feeding into the strategic recommendations
- A **parameter slicer** — allows dynamic switching of the analysis dimension (linked to a `Parameter` table for what-if or field-switching scenarios)
- An **Insights text panel** (embedded directly on the canvas) summarising the four most important findings from the data

**Slicers on this page:** Year, Quarter, Region, Category, State

**The question this page answers:** *"What is the one-page story of our business, and what should we prioritise next quarter?"*

---

## 5. Measures & Calculated Fields

All measures live in the `GlobalMart_Sales_Data` table. The following are referenced across the report:

| Measure | What it calculates |
|---|---|
| `Total Sales` | Sum of all sales revenue |
| `Total Profit` | Sum of all profit |
| `Total Quantity` | Sum of all units sold |
| `Total Orders` | Count of distinct orders |
| `Total Products` | Count of distinct products |
| `Profit Margin%` | Total Profit ÷ Total Sales, expressed as a percentage |
| `Avg Discount per Order` | Average discount value per order |
| `Average Discount` | Average discount rate across transactions |
| `Avg Sales per Order` | Total Sales ÷ Total Orders |
| `Sales by Region` | Total Sales filtered to the selected region |
| `Sales Contribution by Category %` | Each category's share of total sales as a percentage |
| `SamePeriodLastYear` | Sales for the equivalent period in the prior year (time-intelligence) |
| `Slow Moving Product Sales` | Sales value of products below a defined velocity threshold |
| `Late Shipments` | Count or value of orders that shipped after the expected date |

---

## 6. Filters & Slicers

Every page includes a consistent slicer set so users can always drill by the same dimensions. The full slicer inventory across the report:

| Slicer | Dimension | Pages |
|---|---|---|
| **YEAR** | `Date.Year` | All 5 pages |
| **QUARTER** | `Date.Quarter` | All 5 pages |
| **Month** (custom calendar visual) | `Date.Month` | All 5 pages |
| **REGION** | `GlobalMart_Sales_Data.Region` | Pages 1, 2, 3, 4, 5 |
| **SUB-CATEGORY** | `GlobalMart_Sales_Data.Sub-Category` | Page 2 |
| **STATE** | `GlobalMart_Sales_Data.State` | Page 3 |
| **PRODUCT NAME** | `GlobalMart_Sales_Data.Product Name` | Page 3 |
| **ORDER ID** | `GlobalMart_Sales_Data.Order ID` | Page 4 |
| **CATEGORY** | `GlobalMart_Sales_Data.Category` | Page 5 |
| **Parameter** | `Parameter.Parameter` | Page 5 |

---

## 7. Custom Visuals Used

The report uses six custom (marketplace) visuals beyond Power BI's standard library:

| Visual | What it does in this report |
|---|---|
| **Calendar / Month Slicer** (PBI_CV_16948668) | Appears on all five pages — a visual calendar picker for intuitive month-level filtering |
| **Change Chart** | Visualises period-over-period change with clear directional indicators |
| **Icon Array Chart** (Office Solution) | Displays part-to-whole comparisons using icon grids rather than pie slices |
| **Flow Map** | Geographic flow visualisation for showing movement or volume between locations |
| **tMap** | A tile / cartogram map where each region is represented as an equal-area tile |
| **MapBySquillion** | The filled US state map on Page 3 — plots Total Sales by state with region colouring |

---

## 8. Key Insights Embedded in the Report

The Executive Analysis page (Page 5) contains a hand-written Insights panel directly on the canvas. These findings were drawn from the data by the analyst:

1. **Sales peak in December, then drop sharply** — the business is heavily seasonal, with Q4 carrying outsized revenue weight. Q1–Q3 are comparatively flat.

2. **The West region has the highest sales but not the highest profit** — the West is the top revenue region, but aggressive discounting is compressing its margins relative to other regions.

3. **Office Supplies dominate in volume, but Technology yields higher profits** — Office Supplies drive the most orders and units, but the Technology category is far more margin-rich per transaction.

4. **Discounts averaging nearly 24% are reducing profit potential** — the average discount rate across the business is close to 24%, which the scatter charts on Pages 1 and 4 show is correlated with lower — and sometimes negative — profit outcomes.

---

## 9. Recommendations (from the Executive Page)

The report embeds four strategic recommendations derived directly from the data:

1. **Optimise discounting in the West and East regions** — these are the highest-discount regions; bringing average discounts down by even a few percentage points could meaningfully recover margin without sacrificing volume.

2. **Push high-margin products like Technology into underperforming regions** — Technology is profitable but may be under-penetrated in Central and South regions; targeted campaigns could improve margin mix.

3. **Balance inventory and promotions for Office Supplies to reduce slow movers** — the Slow Moving Product Sales metric on Page 2 flags that some Office Supplies lines are not turning; a rationalisation or promotional push could free up working capital.

4. **Design campaigns to boost Q1–Q3 sales and reduce seasonal dependency** — with December doing the heavy lifting, mid-year demand generation (promotions, seasonal campaigns, bundling) would smooth revenue and reduce forecast risk.

---

## 10. How to Open & Use the Report

### Requirements
- **Microsoft Power BI Desktop** — free download at [powerbi.microsoft.com](https://powerbi.microsoft.com)
- The data is embedded in the `.pbix` file — no external database connection is required

### Opening the file
1. Launch Power BI Desktop
2. Go to **File → Open report → Browse**
3. Select `global_mart_sales_performance_analysis_report.pbix`
4. The report will open on Page 1 (Sales Overview)

### Navigating the report
- Use the **page tabs** at the bottom to move between the five pages
- Use the **slicers** on each page (Year, Quarter, Month, Region) to filter all visuals simultaneously
- **Click any bar, slice, or data point** on a chart to cross-filter all other visuals on the same page
- Use the **decomposition tree** on Page 5 to interactively drill into sales drivers

### Refreshing data
The data is embedded and static. To update the report with new data, the source data table (`GlobalMart_Sales_Data`) would need to be replaced or appended via **Home → Transform Data** in Power BI Desktop.

---

*Report authored by Doreen Wathimu. Built with Microsoft Power BI Desktop using the Tidal theme.*
