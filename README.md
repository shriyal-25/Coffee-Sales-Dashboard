☕ **Cafe Sales Dashboard — MySQL + Power BI**



> An end-to-end sales analytics project — raw transactional data cleaned and queried in MySQL, imported into Power BI via Power Query Editor, and visualized as an interactive single-page dashboard tracking $699K in revenue across 3 café locations.



<img width="1297" height="739" alt="Screenshot 2026-06-09 215220" src="https://github.com/user-attachments/assets/39fd4642-3633-421c-ab6e-862b5343069e" />




\---

**Overview**



This project analyses transactional sales data from a 3-branch café chain — **Astoria**, **Hell's** **Kitchen**, and **Lower** **Manhattan** — covering **Jan 2023 to Jun 2023**.



The workflow:

1\. MySQL — Data cleaning, type casting, and all business logic queries

2\. Power Query Editor — Data imported from MySQL into Power BI for transformation and modelling

3\. Power BI — Interactive dashboard with KPIs, trend charts, heatmaps, and category breakdowns



\---



📊 **Dashboard Features**



**KPI Cards**

| Metric | Value |

|---|---|

| Total Sales | **$699K** |

| Total Orders | **149,116** |

| Total Qty Sold | **214,470** |



Each card includes a **vs Last Month (LM)** sparkline and month-on-month change indicator — powered by window function queries using `LAG()`.



**Filters \& Slicers**

\- Month-Year button slicer — Jan 2023 to Jun 2023

\- Calendar date picker — Drill down to any specific date



**Sales Trend Over the Period**

\- Daily bar chart across Jan–Jun 2023

\- Bars colored green (above average) / red (below average)

\- Average sales reference line at $3,861/day — derived from the avg sales subquery



**Sales By Store Location**

| Branch | Revenue |

|---|---|

| Hell's Kitchen | $236.51K |

| Astoria | $232.24K |

| Lower Manhattan | $230.06K |



Each bar includes a vs LM comparison indicator.



**Sales By Product Category**

| Category | Revenue |

|---|---|

| Coffee | $269.95K |

| Tea | $196.41K |

| Bakery | $82.32K |

| Drinking Chocolate | $72.42K |

| Coffee Beans | $40.09K |



**Sales By Product Type**

Granular breakdown of individual products — Barista Espresso ($91.41K), Brewed Black Tea ($47.93K), Brewed Chai Tea ($77.08K), Gourmet Brewed Coffee ($70.03K), Hot Chocolate ($72.42K) — each with vs LM indicators.



**Peak Hours Heatmap**

\- Hour × Day-of-Week matrix (Mon–Sun, starting 6 AM)

\- Color intensity shows transaction density — built from the hour-wise and day-wise sales queries

\- Instantly identifies busiest shifts for staffing and inventory decisions



\---



**🗄️ SQL Queries Covered**



**Data Cleaning**

\- Converted `transaction\\\_date` from string → `DATE` using `STR\\\_TO\\\_DATE('%d-%m-%Y')`

\- Converted `transaction\\\_time` from string → `TIME`

\- Renamed malformed column `ï»¿transaction\\\_id` → `transaction\\\_id`



**KPI 1 — Total Sales**

\- Monthly total sales using `SUM(unit\\\_price \\\* transaction\\\_qty)`

\- Month-on-month % change using `LAG()` window function over ordered months



**KPI 2 — Total Orders**

\- Monthly order count using `COUNT(transaction\\\_id)`

\- Month-on-month % change using `LAG()` over ordered months



**KPI 3 — Total Quantity Sold**

\- Monthly quantity using `SUM(transaction\\\_qty)`

\- Month-on-month % change using `LAG()` over ordered months



**Calendar Heatmap**

\- Single-date lookup returning sales, qty sold, and orders formatted as `'K'` strings



**Weekday vs Weekend Sales**

\- `CASE WHEN DAYOFWEEK() IN (1,7)` to split weekend vs weekday revenue



**Sales by Store Location**

\- `GROUP BY store\\\_location` with formatted K-rounded totals



**Daily Sales with Average Line**

\- Subquery calculates per-day totals → outer query takes `AVG()` → drives the $3,861 reference line

\- `CASE WHEN total\\\_sales > avg\\\_sales` labels each day as Above/Below Average



**Sales by Product Category \& Type**

\- `GROUP BY product\\\_category / product\\\_type` ordered by revenue DESC

\- Supports top-10 filter and category-specific drill-down (e.g. Coffee only)



**Peak Hours Heatmap**

\- `HOUR(transaction\\\_time)` for hour-wise sales

\- `DAYOFWEEK()` mapped to day names via `CASE` for day-wise sales

\- Combined to build the Hour × Day matrix in Power BI



\---



**📄 License**



This project is for educational and portfolio purposes.



