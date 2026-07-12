# E-Commerce Sales & Customer Analytics Project

**Status:** 🟡 In Progress — Phases 1–3 of 7 complete (Business Understanding, Dataset Understanding, Excel Analysis). SQL, Python, and Power BI phases pending.

An end-to-end data analyst portfolio project analyzing sales, customer behavior, and order performance for a D2C beauty & personal care e-commerce brand operating across 5 countries.

---

## 📌 Project Overview

- **Domain:** E-commerce / D2C Retail (Hair, Skin, Body, Makeup categories)
- **Scale:** 300 customers · 1,000 orders · 2,000 order line items · 50 products · 5 countries · 1 year (2024)
- **Business problem:** ~19.5% of orders are lost to cancellations/returns, and there's no single source of truth for revenue, order health, or customer performance across markets.
- **Tools used so far:** Microsoft Excel (PivotTables, PivotCharts, Slicers, GETPIVOTDATA)
- **Tools planned:** SQL · Python (EDA & segmentation) · Power BI (dashboard)

---

## 🗂️ Repository Structure

```
ecommerce-sales-analytics-project/
├── README.md
├── data/
│   ├── raw/
│   │   ├── customers.csv
│   │   ├── products.csv
│   │   ├── orders.csv
│   │   ├── order_items.csv
│   │   └── sales_cleaned.csv
│   └── data_dictionary.md
├── docs/
│   └── data_quality_notes.md
├── Excel/
│   └── Ecommerce_Analysis.xlsx
├── sql/                    ← planned (Phase 4)
├── python/                 ← planned (Phase 5)
├── powerbi/                ← planned (Phase 8)
└── report/                 ← planned (Phase 10)
```

---

## Phase 1 — Business Understanding

**Company context:** A mid-sized D2C beauty & personal care e-commerce brand selling Hair, Skin, Body, and Makeup products across 5 markets — Spain, Italy, France, Germany, and Morocco.

**Business problem:** Leadership has no single source of truth for sales performance, and doesn't know why ~19.5% of orders never convert to completed sales (cancellations + returns), which customer segments drive repeat revenue, or which markets/categories to prioritize.

**Objectives:**
1. Quantify revenue and order-health trends by month, category, and country.
2. Identify why cancellations/returns happen and whether it's worse in specific markets.
3. Understand which customers are repeat buyers vs. one-time vs. never-converted.
4. Give a clear view of which products/categories perform best.

**Stakeholders:**
| Stakeholder | Primary interest |
|---|---|
| CEO / Founder | Overall revenue growth |
| Marketing Head | Country/customer segment targeting |
| Operations Head | Root cause of cancellations/returns |
| Category Manager | Product performance |

**Core Business KPIs:** Total Revenue, Average Order Value (AOV), Cancellation Rate, Return Rate, Repeat Purchase Rate, Revenue by Category/Country, Customer Lifetime Value.

**Success criteria:** Every KPI in the final dashboard can be explained and defended; at least 3–5 concrete, data-backed recommendations; the story is understandable to a non-technical stakeholder in under 2 minutes.

---

## Phase 2 — Dataset Understanding

**Source files:**
| File | Rows | Grain (what one row means) |
|---|---|---|
| customers.csv | 300 | 1 customer |
| products.csv | 50 | 1 product (SKU) |
| orders.csv | 1,000 | 1 order header (status lives here) |
| order_items.csv | 2,000 | 1 product line within an order |
| sales_cleaned.csv | 1,625 | 1 Completed-order product line, pre-joined with Revenue calculated |

**Fact vs. Dimension:**
- **Facts (measures):** quantity, price, Revenue
- **Dimensions (labels to group by):** country, category, order_date, status, signup_date

**Table relationships:**
- `orders.customer_id → customers.customer_id`
- `order_items.order_id → orders.order_id`
- `order_items.product_id → products.product_id`
- `sales_cleaned.customer_id → customers.customer_id` and `sales_cleaned.product_id → products.product_id` (sales_cleaned is *not* linked directly to orders/order_items, to avoid double-counting Revenue)

**Assumptions:** Single currency throughout; "Completed" is the only revenue-recognized status; one price per product per line item.

**Limitations:** No cost/margin data; single calendar year (no YoY); no marketing-channel data; 139 orders have no matching line items (see Data Quality Notes below).

Full column-level definitions are in [`Data/Data_dictionary.md/data_dictionary.md`](Data/Data_dictionary.md/data_dictionary.md).

---

## Phase 3 — Excel Analysis

**Approach:** Built entirely on native Excel features — PivotTables connected to a shared Data Model (via Manage Relationships), PivotCharts, and Slicers — with all KPIs as live formulas (`SUM`, `COUNTIF`, `GETPIVOTDATA`), not hardcoded snapshots, so every number recalculates if the source data changes.

**Data Model relationships used:**
```
order_items(order_id)   → orders(order_id)
order_items(product_id) → products(product_id)
orders(customer_id)     → customers(customer_id)
sales_cleaned(customer_id) → customers(customer_id)
sales_cleaned(product_id)  → products(product_id)
```

**Deliverables (see [`Excel/Ecommerce_Analysis.xlsx`](Excel/Ecommerce_Analysis.xlsx)):**

- **KPI Summary** — Total Revenue (₹311,111), AOV (₹447.64), Cancellation Rate (10.3%), Return Rate (9.2%), Total Order Lost (19.5%), Repeat Purchase Rate (82%), Never-Ordered Customers (15)
- **Category Wise Revenue** — Revenue by Category × Month (PivotTable + line chart)
- **Order Count By Country** — Order status split by country (PivotTable + stacked chart, with Slicers)
- **Top 10 Customers** — Highest-revenue customers (PivotTable + bar chart)
- **Lost Calculation** — Cancellation/Return rate by country, built on a live PivotTable with `GETPIVOTDATA` formulas

### Key Findings
1. Approximately 19.5% of orders were lost due to cancellations and returns.
2. France has the highest cancellation rate (11.86%).
3. Germany has the highest return rate (11.31%).
4. Spain demonstrates the strongest order completion performance.
5. Italy shows both cancellation and return rates above 10%, requiring further investigation.
6. 82% of customers are repeat buyers; 15 customers (5%) have never placed an order.

---

## 📋 Known Data Limitations (documented, not hidden)

- **No cost/COGS data** — analysis is revenue-based only; profit/margin is out of scope.
- **139 of 1,000 orders have no matching line items** (13.9%) — a documented data-completeness gap, not a status-driven pattern (see `docs/data_quality_notes.md`). These orders are excluded from revenue analysis but included in order-count/status KPIs.
- **Single calendar year (2024)** — no year-over-year comparison possible, only monthly trend within the year.

---

## 🔜 Next Steps

- [ ] Phase 4: Rebuild core KPIs in SQL (joins, CTEs, window functions) to validate at scale
- [ ] Phase 5: Python EDA — RFM customer segmentation, outlier detection, correlation analysis
- [ ] Phase 6: Power BI dashboard — 7-page interactive report with star-schema data model
- [ ] Phase 7: Final written business report with prioritized recommendations

---

## 🧑‍💻 About This Project

Built as a fresher Data Analyst portfolio project to demonstrate the real-world analyst workflow: Excel → SQL → Python → Power BI → Business Reporting. Each phase's numbers are cross-validated against the previous phase before moving forward.

---

🧑‍💻 **Author:** Saurabh Gopal Chaudhari
📊 **Role:** Aspiring Data Analyst
🔗 **LinkedIn:** https://www.linkedin.com/in/saurabh-chaudhari-ds/
📧 **Focus Areas:** Excel, SQL, Python, Power BI, Data Visualization, Business Analytics
