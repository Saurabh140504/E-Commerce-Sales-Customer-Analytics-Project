# Data Dictionary

This file explains what every column in every file actually means — in plain words, so anyone opening this repo (including a recruiter with no data background) can understand the data immediately.

---

## 1. customers.csv (300 rows)
**In simple words:** One row = one customer.

| Column | Meaning |
|---|---|
| customer_id | A unique number given to each customer (like an ID card number) |
| country | Which country the customer lives in (Spain, Italy, France, Germany, or Morocco) |
| signup_date | The date this customer created an account |

---

## 2. products.csv (50 rows)
**In simple words:** One row = one product the store sells.

| Column | Meaning |
|---|---|
| product_id | A unique number given to each product |
| product_name | The name of the product |
| category | What type of product it is: Hair, Skin, Body, or Makeup |

---

## 3. orders.csv (1,000 rows)
**In simple words:** One row = one order (like one receipt). This table tells you WHO ordered, WHEN, and WHAT HAPPENED to that order — but not WHAT they bought (that's in order_items).

| Column | Meaning |
|---|---|
| order_id | A unique number given to each order |
| customer_id | Which customer placed this order (matches customer_id in customers.csv) |
| order_date | The date the order was placed |
| status | What happened to the order: Completed, Cancelled, or Returned |

---

## 4. order_items.csv (2,000 rows)
**In simple words:** One row = one product inside one order. If someone orders 3 different products in a single order, that creates 3 rows here — all sharing the same order_id.

| Column | Meaning |
|---|---|
| order_id | Which order this product belongs to (matches order_id in orders.csv) |
| product_id | Which product was bought (matches product_id in products.csv) |
| quantity | How many units of that product were bought |
| price | Price of ONE unit of that product |

---

## 5. sales_cleaned.csv (1,625 rows)
**In simple words:** This is a ready-made "shortcut" file — someone already combined order_items + orders + products for you, but **only kept the orders that were actually Completed** (Cancelled/Returned orders are left out). It also already calculated Revenue for you.

| Column | Meaning |
|---|---|
| order_id, product_id, quantity, price | Same meaning as in order_items.csv |
| Revenue | quantity × price — how much money this line item made |
| customer_id | Which customer this order belongs to |
| order_date | Date the order was placed |
| status | Always says "Completed" in this file |
| year, month | The year and month pulled out from order_date, for easy grouping |

**Important thing to know:** This file does **NOT** include `category` or `country` directly — those live in products.csv and customers.csv. To see revenue by category or country, you need to connect this file to those two using `product_id` and `customer_id`.

---

## How the 5 files connect to each other (the relationships)

Think of it like this — each arrow means "look this ID up in that other table":

```
order_items → orders        (using order_id)
order_items → products      (using product_id)
orders → customers           (using customer_id)
sales_cleaned → customers    (using customer_id)
sales_cleaned → products     (using product_id)
```

**Simple way to remember it:** Facts you can count or add up (quantity, price, Revenue) live in order_items/sales_cleaned. Labels you use to group things (country, category, status) live in the other 3 files, and you connect them using the ID columns above.
