# E-Commerce Sales & Customer Analytics — Excel & SQL Analysis

**Status:** 🟡 In Progress — Phase 3 (Excel) and Phase 4 (SQL) complete. Python and Power BI phases pending.

This document covers the **Excel** and **SQL** analysis stages of the end-to-end E-Commerce Sales & Customer Analytics project (D2C beauty & personal care brand, 5 countries, 4 categories, 1 year of data). Every KPI below is cross-validated between the two tools — the SQL numbers match the Excel numbers, which is the point of doing both.

---

## 📁 Folder Structure

```
ecommerce-sales-analytics-project/
├── data/
│   └── raw/  (customers.csv, products.csv, orders.csv, order_items.csv, sales_cleaned.csv)
├── Excel/
│   └── Ecommerce_Analysis.xlsx
├── sql/
│   ├── 01_basic_queries.sql
│   ├── 02_aggregations.sql
│   ├── 03_joins.sql
│   ├── 04_case_subqueries_kpis.sql
│   ├── 05_ctes.sql
│   ├── 06_window_functions.sql
│   └── query_notes.md
└── README.md   ← this file
```

---

## Part 1 — Excel Analysis

**Approach:** Built on a native Excel Data Model — PivotTables, PivotCharts, and Slicers connected via Manage Relationships — with all KPIs as live formulas (`SUM`, `COUNTIF`, `GETPIVOTDATA`), not hardcoded snapshots.

**Data Model relationships used:**
```
order_items(order_id)      → orders(order_id)
order_items(product_id)    → products(product_id)
orders(customer_id)        → customers(customer_id)
sales_cleaned(customer_id) → customers(customer_id)
sales_cleaned(product_id)  → products(product_id)
```

**Deliverables** ([`Excel/Ecommerce_Analysis.xlsx`](Excel/Ecommerce_Analysis.xlsx)):
- **KPI Summary** — Total Revenue (₹311,111), AOV (₹447.64), Cancellation Rate (10.3%), Return Rate (9.2%), Repeat Purchase Rate (82%), Never-Ordered Customers (15)
- **Category Wise Revenue** — Revenue by Category × Month
- **Order Count by Country** — Order status split by country, with Slicers
- **Top 10 Customers** — Highest-revenue customers
- **Lost Calculation** — Cancellation/Return rate by country

**Key Findings:**
1. ~19.5% of orders are lost to cancellation + return.
2. France has the highest cancellation rate (11.86%); Germany has the highest return rate (11.31%).
3. Spain shows the strongest order completion performance.
4. Italy is above 10% on both cancellation and return — flagged for investigation.
5. 82% of customers are repeat buyers; 15 customers (5%) have never ordered.

---

## Part 2 — SQL Analysis

**Approach:** All 4 raw tables (`customers`, `products`, `orders`, `order_items`) imported into a relational schema with foreign keys defined exactly as in the Excel Data Model above. `sales_cleaned` was independently rebuilt via SQL joins to confirm it equals `order_items ⋈ orders ⋈ products` filtered to `status = 'Completed'` — this cross-check validates every number that follows.

**Concepts covered:** SELECT / WHERE / ORDER BY, GROUP BY / HAVING, INNER & LEFT JOIN, CASE WHEN, subqueries, CTEs, window functions (RANK, SUM OVER, running totals).

**Query files (30 queries total, easy → advanced):**
| File | Covers |
|---|---|
| `01_basic_queries.sql` | Filtering, sorting, distinct values, row counts |
| `02_aggregations.sql` | GROUP BY, HAVING, order/customer/product-level counts |
| `03_joins.sql` | INNER JOIN across all 4 tables, LEFT JOIN for orphan orders |
| `04_case_subqueries_kpis.sql` | CASE WHEN labeling, Cancellation Rate, AOV, above-average spenders |
| `05_ctes.sql` | WITH-clause queries: repeat customers, MoM growth, high-spend customers |
| `06_window_functions.sql` | RANK, running revenue total, top-1-per-country pattern |

**Key Findings (validated against Excel, plus new insights only SQL/aggregation surfaces):**
1. **Total Revenue, AOV, Cancellation Rate, Return Rate all reconciled exactly** with the Excel KPI Summary — confirming `sales_cleaned` was correctly rebuilt.
2. **Revenue by category:** Hair (₹101,637) > Makeup (₹81,085) > Body (₹76,011) > Skin (₹52,378) — Hair is the leading category.
3. **Revenue by country:** Italy (₹70,719) and Spain (₹69,897) lead; Germany (₹49,355) is the lowest — despite Germany having the highest *return rate* in the Excel analysis, indicating a quality/fit issue rather than a demand issue.
4. **Cancellation rate by category:** Makeup (9.85%) and Hair (9.73%) are highest; Body (8.54%) is lowest — cancellation is not concentrated in one category, it's fairly evenly spread.
5. **Monthly revenue swings meaningfully month-to-month** — biggest jump is October (+32.3% MoM), biggest drop is February (‑24.7% MoM), suggesting a seasonal or promotional pattern worth investigating in Phase 5 (Python).
6. **139 orphan orders confirmed via LEFT JOIN** — same finding as the Excel/data-quality notes, now validated at the query level.

**Data-quality decision (documented once, applies to both Excel and SQL):**
> 139 of 1,000 orders (13.9%) have no matching `order_items` rows. Status distribution among these orders closely matches the overall dataset, indicating a data-completeness gap rather than a status-driven pattern. These orders are **excluded from revenue/product analysis** but **included in order-count and status-based KPIs**.

---

## 📋 Known Data Limitations

- No cost/COGS data — analysis is revenue-based only; margin is out of scope.
- Single calendar year (2024) — monthly trend only, no YoY comparison.
- 139 orphan orders — documented above, consistently excluded from revenue calculations in both tools.

---

## 🔜 Next Steps

- [ ] Phase 5: Python EDA — RFM customer segmentation, outlier detection, correlation analysis
- [ ] Phase 6: Power BI dashboard — 7-page interactive report, star-schema data model
- [ ] Phase 7: Final written business report with prioritized recommendations

---

## 🧑‍💻 About This Project

Fresher Data Analyst portfolio project demonstrating the real-world workflow: Excel → SQL → Python → Power BI → Business Reporting, with every KPI cross-validated between tools before moving to the next phase.

🧑‍💻 **Author:** Saurabh Gopal Chaudhari
📊 **Role:** Aspiring Data Analyst
🔗 **LinkedIn:** https://www.linkedin.com/in/saurabh-chaudhari-ds/
📧 **Focus Areas:** Excel, SQL, Python, Power BI, Data Visualization, Business Analytics
