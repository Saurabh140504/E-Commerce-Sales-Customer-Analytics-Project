# E-Commerce Sales & Customer Analytics

**Status:** 🟡 In Progress — Excel (Phase 3), SQL (Phase 4), and Python (Phase 5) completed. Power BI Dashboard and Business Report are currently in progress.

This project demonstrates an end-to-end Data Analyst workflow using a simulated D2C Beauty & Personal Care e-commerce business operating across **5 countries**, **4 product categories**, and **one year (2024)** of sales data.

The project follows a real-world analytics workflow:

**Excel → SQL → Python → Power BI → Business Report**

Each phase validates the previous one to ensure business metrics remain consistent across all tools.

---

# 📁 Project Structure

```
ecommerce-sales-analytics-project/
│
├── data/
│   └── raw/
│       ├── customers.csv
│       ├── products.csv
│       ├── orders.csv
│       ├── order_items.csv
│       └── sales_cleaned.csv
│
├── Excel/
│   └── Ecommerce_Analysis.xlsx
│
├── SQL/
│   ├── ECommerce  Analyses  using SQL
│
├── Python/
│   ├── ecommerce_analysis.py
│   
│
├── PowerBI/
│   └── (In Progress)
│
└── README.md
```

---

# 📊 Project Overview

Business Problem:

The management team wanted a single source of truth to understand business performance across different countries, product categories, and customers.

The project focuses on:

- Sales Performance
- Customer Behaviour
- Product Performance
- Country Performance
- Order Status Analysis
- Revenue Trends
- Customer Segmentation

---

# Phase 3 — Excel Analysis

## Objective

Build an interactive business dashboard using Excel and validate key business KPIs.

---

## Excel Features

- Data Model
- Relationships
- Pivot Tables
- Pivot Charts
- KPI Dashboard
- Slicers
- Interactive Reports

---

## Data Model

```
Customers
      ▲
      │
Orders
      ▲
      │
Order_Items
      │
      ▼
Products
```

---

## KPI Dashboard

| KPI | Value |
|------|------:|
| Total Revenue | ₹311,111 |
| Average Order Value | ₹447.64 |
| Cancellation Rate | 10.3% |
| Return Rate | 9.2% |
| Repeat Purchase Rate | 82% |
| Customers Never Ordered | 15 |

---

## Excel Insights

- Hair category generated the highest revenue.
- Italy generated the highest overall revenue.
- France recorded the highest cancellation rate.
- Germany recorded the highest return rate.
- Around 19.5% of orders were lost because of cancellations and returns.
- Most customers were repeat buyers.

---

# Phase 4 — SQL Analysis

## Objective

Validate Excel KPIs using SQL and perform advanced business analysis.

---

## SQL Concepts Covered

- SELECT
- WHERE
- ORDER BY
- DISTINCT
- Aggregate Functions
- GROUP BY
- HAVING
- INNER JOIN
- LEFT JOIN
- CASE WHEN
- Subqueries
- CTEs
- Window Functions

---

## SQL Analysis

- Revenue Analysis
- Customer Analysis
- Product Analysis
- Category Analysis
- Country Analysis
- Monthly Revenue
- Customer Spending
- Repeat Customers
- Revenue Ranking
- Running Total
- Month-over-Month Growth
- Cancellation Analysis
- Return Analysis

---

## SQL Insights

- Revenue calculated in SQL exactly matched Excel.
- Hair generated the highest revenue among all categories.
- Italy and Spain contributed the highest sales.
- Germany generated the lowest revenue.
- 139 orphan orders were identified and excluded from revenue analysis.
- Monthly revenue showed noticeable seasonal fluctuations.

---

# Phase 5 — Python Analysis

## Objective

Perform Exploratory Data Analysis (EDA), validate the SQL dataset, analyze customer behaviour, and generate business insights before building the Power BI dashboard.

---

## Python Libraries

- Pandas
- NumPy
- Matplotlib
- Seaborn
- SQLAlchemy

---

## Python Workflow

### Step 1

Connected Python directly with the MySQL database.

### Step 2

Imported the four relational tables.

- Customers
- Products
- Orders
- Order Items

### Step 3

Performed data quality checks.

- Missing Values
- Duplicate Records
- Data Types
- Unique Values
- Summary Statistics

### Step 4

Merged all tables into a single analytical dataset.

Created the Revenue column.

Filtered completed orders for revenue analysis.

### Step 5

Validated table relationships.

Checked missing customers, products, and orders.

### Step 6

Performed Exploratory Data Analysis.

- Revenue Distribution
- Country Performance
- Category Performance
- Monthly Revenue
- Cancellation Analysis
- Return Analysis
- Correlation Analysis

### Step 7

Performed Outlier Detection using the IQR method.

### Step 8

Calculated Correlation Matrix.

### Step 9

Performed RFM Customer Segmentation.

---

# Python Insights

## Dataset Quality

- 300 Customers
- 50 Products
- 1,000 Orders
- 2,000 Order Items

The dataset contains:

- No Missing Values
- No Duplicate Records
- Valid Table Relationships

A total of **139 orphan orders** were identified and excluded from revenue calculations.

---

## Revenue Analysis

- Revenue from completed orders: **₹311,111**
- Italy generated the highest revenue.
- Spain ranked second in revenue.
- Germany generated the lowest revenue.
- Revenue remained balanced across all product categories.

---

## Customer Behaviour

Customer Segments:

| Segment | Customers |
|----------|----------:|
| Loyal | 122 |
| One Time | 71 |
| Champions | 44 |
| Never Converted | 33 |
| At Risk | 30 |

Repeat Purchase Rate:

**65.33%**

---

## Cancellation & Returns

- France recorded the highest cancellation percentage.
- Germany recorded the highest return percentage.
- Makeup products had the highest cancellation rate.

---

## Outlier Analysis

- Total Outliers: **16**
- Average Order Value (With Outliers): **₹191.45**
- Average Order Value (Without Outliers): **₹187.60**

Only a small difference was observed, indicating that extreme orders have minimal impact on overall business performance.

---

## Correlation Analysis

| Variables | Correlation |
|------------|------------:|
| Quantity vs Revenue | 0.64 |
| Price vs Revenue | 0.68 |

Revenue is positively influenced by both product quantity and selling price.

---

## Business Recommendations

- Focus marketing campaigns on Italy and Spain.
- Investigate cancellation reasons in France.
- Improve product quality or logistics in Germany to reduce returns.
- Re-engage the 33 inactive customers with promotional campaigns.
- Increase customer retention efforts to convert one-time buyers into loyal customers.

---

# 📋 Data Limitations

- Revenue-based analysis only.
- No Cost or Profit information.
- Single-year dataset (2024).
- No demographic information.
- No shipping or payment details.
- 139 orphan orders were excluded from revenue calculations.

---

# 🚀 Next Phase

## Phase 6 — Power BI Dashboard *(In Progress)*

Planned dashboards:

- Executive Dashboard
- Revenue Dashboard
- Customer Dashboard
- Product Dashboard
- Country Dashboard
- RFM Dashboard

---

## Phase 7 — Business Report *(In Progress)*

The final report will include:

- Executive Summary
- KPI Summary
- Revenue Insights
- Customer Insights
- Product Insights
- Country Performance
- Business Recommendations

---

# 🧑‍💻 About This Project

This project demonstrates a complete end-to-end Data Analyst workflow, beginning with raw transactional data and progressing through Excel, SQL, Python, and Power BI before delivering business recommendations.

The objective is to showcase practical data analysis skills commonly used in real-world business environments.

---
🧑‍💻 **Author:** Saurabh Gopal Chaudhari
📊 **Role:** Aspiring Data Analyst
🔗 **LinkedIn:** https://www.linkedin.com/in/saurabh-chaudhari-ds/
📧 **Focus Areas:** Excel, SQL, Python, Power BI, Data Visualization, Business Analytics
