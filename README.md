# Capstone_project-Smart-City-Insights-A-Tableau-Based-Urban-Analytics-Dashboard-
My end-to-end journey from raw, messy sales data to a clean Tableau dashboard — built to answer real business questions like top products, top customers, and seasonal sales trends.


# Smart City Insights: A Tableau-Based Urban Analytics Dashboard

## Overview

This capstone project turns a raw, messy e-commerce/retail transactions dataset into an interactive Tableau dashboard that surfaces sales trends, top-performing products and customers, and behavioral patterns across time and geography. The goal was to take the data through a full analytics workflow — cleaning, transforming, calculating KPIs, and finally visualizing — so that a business user could open the dashboard and immediately understand how the business is performing.

The finished dashboard is built in Tableau and organized into six sheets feeding a single combined dashboard view: **Monthly Sales Trend**, **Top 10 Products**, **Top 10 Customers**, **Sales by Weekdays**, **Sales by Countries**, and a **KPI** summary panel.

---

## 1. Data Cleaning

Before any analysis, the raw transaction data was cleaned to remove noise and errors that would otherwise distort the numbers:

| Step | What was done | Why |
|---|---|---|
| Remove cancelled orders | Excluded any invoice number starting with **"C"** | These represent cancellations, not completed sales, and would inflate/distort revenue if left in |
| Remove null Customer IDs | Dropped rows with missing customer identifiers | Can't attribute a sale to a customer for CLV/AOV analysis without an ID |
| Remove duplicates | Deduplicated repeated transaction rows | Prevents double-counting the same sale |
| Remove zero quantity | Filtered out rows where quantity = 0 | A zero-quantity row isn't a real transaction |
| Remove zero unit price | Filtered out rows where unit price = 0 | Free/zero-price rows are usually data errors, not real sales, and would understate average values |
| Fix data types | Corrected column types across the dataset | Ensures accurate calculations downstream |

**Data type corrections applied:**
- `Invoice Date` → converted to proper **Date/Time**
- `Quantity` → converted to **Integer**
- `Unit Price` → converted to **Decimal**

---

## 2. Data Transformations

Once the data was clean, several calculated fields were created to enable the analysis:

1. **Total Sales** = `Quantity × Unit Price`
2. **Order Month & Year** — extracted from Invoice Date for trend analysis
3. **Month-Year** — a combined field used for the monthly time series
4. **Day of Week** — extracted from Invoice Date to analyze weekday sales patterns
5. **Hourly Analysis** — extracted the hour from Invoice Date for time-of-day analysis

---

## 3. Key Performance Indicators (KPIs)

Four core KPIs summarize overall business performance:

- **Total Sales / Average Sales**
- **Average Quantity / Total Quantity**
- **CLV (Customer Lifetime Value)**
- **AOV (Average Order Value)** — calculated as total revenue per customer divided by number of purchases per customer

![KPI Summary](images/04_kpi_summary.jpg)

From the current dataset, the headline numbers are:

| Metric | Value |
|---|---|
| Average Order Value (AOV) | 22 |
| Count of Invoices | 397,640 |
| Total Quantity Sold | 5,166,023 |
| Total Revenue | 8,908,741 |

---

## 4. Dashboard Views

### Monthly Sales Trend
Tracks **Sum of Sales** and **Sum of Quantity** by month (January–December), with trend lines overlaid. Sales climb steadily through the year, peak sharply in September (~1.13M) and November (~1.04M) — likely seasonal/holiday-driven spikes — before dropping off in December.

![Monthly Sales Trend](images/01_monthly_sales_trend.jpg)

### Top 10 Products by Total Sales
A bar chart ranking Stock Codes by total sales value. The top product (Stock Code 22423) alone generates ~142,567 in sales, roughly 40% more than the second-ranked product.

![Top 10 Products](images/02_top10_products.jpg)

### Top 10 Customers by Total Sales
Ranks customers by total sales contribution. The top customer (ID 14646) accounts for 280,206 in sales — well ahead of the rest — which is useful for identifying high-value accounts for retention efforts.

![Top 10 Customers](images/03_top10_customers.jpg)

### Sales by Weekdays
A treemap showing how sales are distributed across the days of the week. Thursday and Tuesday are the strongest sales days (~1.71M each), while Saturday is by far the weakest (~444K) — a pattern that could inform staffing or promotional timing.

![Sales by Weekdays](images/05_sales_by_weekdays.jpg)

### Sales by Countries
A pie chart showing the geographic distribution of sales. The **United Kingdom dominates at 84.65%** of total sales, with the Netherlands (3.31%), Germany (2.65%), and Switzerland (0.65%) making up most of the remainder — highlighting how concentrated the customer base is domestically.

![Sales by Countries](images/06_sales_by_countries.jpg)

### Combined Dashboard
All views are brought together into a single interactive dashboard, allowing filtering and cross-highlighting across sheets (e.g., clicking a country filters the product and customer charts).

![Full Dashboard](images/07_full_dashboard.jpg)

---

## 5. Tools Used

- **Tableau Public / Desktop** — data connection, cleaning (via filters/calculated fields), and dashboard design
- **Excel** — source raw dataset (`data_tableau_cs.xlsx`)

---

## 6. Key Insights

- Sales show clear **seasonality**, with strong peaks around September and November.
- Revenue is **highly concentrated**: a small number of products and customers drive a disproportionate share of total sales.
- The business is **heavily UK-centric**, with over 84% of sales coming from a single country — international markets remain a small share of revenue.
- **Weekday sales significantly outperform weekend sales**, especially Saturday, suggesting the customer base is likely business/wholesale-oriented rather than typical weekend retail shoppers.

---

## 7. How to Explore

1. Open the published Tableau Public workbook-https://public.tableau.com/views/Capstone-ProjectSmartCityInsightsATableauBasedUrbanAnalyticsDashboard/Dashboard1?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link








2. Use the tabs at the bottom (`Monthly sales trend`, `Top 10 products`, `Top 10 customers`, `Sales by Countries`, `Sales by Weekdays`, `KPI`, `Dashboard 1`) to move between individual views and the combined dashboard.
3. Filters (Invoice Exclusion, Quantity > 0, Unit Price > 0, Country) are already applied so all views reflect the cleaned dataset.
