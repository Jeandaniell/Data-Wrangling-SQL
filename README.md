# Data-Wrangling-SQL
# SQL Project — WideWorldImporters & SQLPlayground

## Overview

This project contains a series of SQL queries designed to analyze business data consistency, data quality, revenue loss, and customer purchasing behavior across two databases: **WideWorldImporters** and **SQLPlayground**.

---

## Databases

| Database | Used in |
|---|---|
| `WideWorldImporters` | Q1, Q2, Q3 |
| `SQLPlayground` | Q4 |

---

## Questions

### Q1 — Orders vs Invoices Consistency Report

**Database:** `WideWorldImporters`

**Objective:** Audit the consistency between customer orders and their corresponding invoices by comparing quantities and monetary values.

**Output columns:**

| Column | Description |
|---|---|
| `CustomerID` | Unique customer identifier |
| `CustomerName` | Full name of the customer |
| `TotalNBOrders` | Total number of orders placed |
| `TotalNBInvoices` | Number of invoices converted from an order |
| `OrdersTotalValue` | Sum of all order values |
| `InvoicesTotalValue` | Sum of all invoice values |
| `AbsoluteValueDifference` | Absolute difference between `OrdersTotalValue` and `InvoicesTotalValue` |

**Notes:**
- `TotalNBOrders` and `TotalNBInvoices` must be identical by definition, since we only consider orders that were converted into invoices.
- The goal is to detect discrepancies between order values and invoice values (columns c & d).
- The data in `WideWorldImporters` is clean, so all differences should be zero before Q2.

**Sort order:** `AbsoluteValueDifference` DESC, `TotalNBOrders` ASC, `CustomerName` ASC

---

### Q2 — Unit Price Update for a Specific Invoice Line

**Database:** `WideWorldImporters`

**Objective:** For customer `CustomerID = 1060` (`Anand Mudaliyar`), find the first `InvoiceLine` of his first `Invoice` (both identified by their lowest respective IDs), then increase its `UnitPrice` by **20**.

**Validation:** After applying the update, re-running the Q1 query should produce the corrected resultset as described in `Q2-Resultset_Corrected.csv`.

**Alternative (if Q1 was not completed):** Run a selection query returning `CustomerId`, `CustomerName`, and `InvoiceTotal` (sum of all invoice lines for the target invoice). The expected post-update result is available in `Q2-Alternative-Resultset.csv`.

---

### Q3 — Highest Revenue Loss from Unconverted Orders by Customer Category

**Database:** `WideWorldImporters`

**Objective:** Identify the highest monetary loss caused by orders that were **never converted into invoices**, grouped by customer category. For each category, also identify the customer responsible for the highest loss (name and ID).

**Output:** Ordered by highest loss (descending).

**Implementation note:** This query can be written in pure SQL. A T-SQL solution using cursors is also acceptable if the pure SQL approach proves too complex.

---

### Q4 — Customers Who Purchased All Products and More Than 50 Units

**Database:** `SQLPlayground`

**Objective:** Select all data for customers who meet **both** of the following criteria:

1. They have purchased **every product** available in the database.
2. The **total quantity** of all their purchases exceeds **50 units**.

---

## Project Structure

```
/
├── Q1_orders_invoices_consistency.sql
├── Q2_unit_price_update.sql
├── Q3_revenue_loss_by_category.sql
├── Q4_customers_all_products.sql
├── Q2-Resultset_Corrected.csv
├── Q2-Alternative-Resultset.csv
└── README.md
```

---

## Prerequisites

- Microsoft SQL Server with the **WideWorldImporters** sample database restored
- Access to the **SQLPlayground** database
- SQL Server Management Studio (SSMS) or any compatible SQL client

---

## Author

*SQL project — Academic assignment*
