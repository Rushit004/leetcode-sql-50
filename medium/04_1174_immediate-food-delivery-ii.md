# 🟡 1174 · Immediate Food Delivery ii

**Difficulty:** Medium | **Topic:** Filtering / Subquery / Aggregation  
**LeetCode:** [Problem Link](https://leetcode.com/problems/delivery-company-statistics-ii/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Find the percentage of **immediate orders** among the **first orders** of all customers, rounded to **2 decimal places**.

An order is **immediate** if the `order_date` matches the `customer_pref_delivery_date`. The **first order** of a customer is the one with the earliest `order_date`.

---

### Schema

```sql
CREATE TABLE Delivery (
  delivery_id                 INT PRIMARY KEY,
  customer_id                 INT,
  order_date                  DATE,
  customer_pref_delivery_date DATE
);
```

### Sample Input

| delivery_id | customer_id | order_date | customer_pref_delivery_date |
|-------------|-------------|------------|-----------------------------|
| 1           | 1           | 2019-08-01 | 2019-08-02                  |
| 2           | 2           | 2019-08-02 | 2019-08-02                  |
| 3           | 1           | 2019-08-11 | 2019-08-12                  |
| 4           | 3           | 2019-08-24 | 2019-08-24                  |
| 5           | 3           | 2019-08-21 | 2019-08-22                  |
| 6           | 2           | 2019-08-11 | 2019-08-13                  |
| 7           | 4           | 2019-08-09 | 2019-08-09                  |


### Sample Output

| immediate_percentage |
|----------------------|
| 50.00                |

---

### Solution

```sql
SELECT ROUND(SUM(order_date = customer_pref_delivery_date) * 100 / COUNT(*), 2) AS 'immediate_percentage'
FROM Delivery
WHERE (customer_id, order_date) IN (
    SELECT customer_id, MIN(order_date)
    FROM Delivery
    GROUP BY customer_id
);
```

## 🧠 Approach

1. The subquery `SELECT customer_id, MIN(order_date) FROM Delivery GROUP BY customer_id` identifies the **earliest order date** per customer — i.e. each customer's first order.
2. The `WHERE (customer_id, order_date) IN (...)` **row-value filter** keeps only the first order row for each customer, discarding all subsequent orders.
3. On the filtered set, `SUM(order_date = customer_pref_delivery_date)` exploits MySQL's boolean-to-integer coercion — the equality check returns `1` when immediate and `0` otherwise, so `SUM()` effectively counts immediate orders.
4. Dividing by `COUNT(*)` (total first orders) and multiplying by `100` gives the percentage.
5. `ROUND(..., 2)` formats the result to 2 decimal places.

---

## 📌 Concepts Used

`WHERE IN` · `Row-value Subquery` · `MIN()` · `GROUP BY` · `SUM()` · `COUNT()` · `ROUND()` · `Boolean Coercion` · `Conditional Aggregation`

---

## 💭 My Takeaway

Two things stand out here. First, the **row-value `IN` clause** — `WHERE (customer_id, order_date) IN (subquery)` — is a compact and readable way to filter on composite keys without needing a `JOIN`. Second, `SUM(condition)` as a shorthand for conditional counting is a neat MySQL trick; the boolean expression evaluates to `1` or `0` directly, saving a full `CASE WHEN` block. Both patterns are worth keeping in the toolkit for future problems.