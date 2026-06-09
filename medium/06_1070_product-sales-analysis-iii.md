# 🟡 1070 · Product Sales Analysis III

**Difficulty:** Medium | **Topic:** Subquery / JOIN / MIN / Group Filtering  
**LeetCode:** [Problem Link](https://leetcode.com/problems/product-sales-analysis-iii/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Find all sales that occurred in the **first year each product was ever sold**.
For each `product_id`, identify its earliest year in the `Sales` table and return all sales entries for that product in that year.

Return columns: `product_id`, `first_year`, `quantity`, `price`.

---

## 🗂️ Schema
```sql
CREATE TABLE Sales (
  sale_id    INT,
  product_id INT,
  year       INT,
  quantity   INT,
  price      INT
);
-- Primary key: (sale_id, year)

CREATE TABLE Product (
  product_id   INT,
  product_name VARCHAR(255)
);
```

### Sample Input

**Sales**

| sale_id | product_id | year | quantity | price |
|---------|------------|------|----------|-------|
| 1       | 100        | 2008 | 10       | 5000  |
| 2       | 100        | 2009 | 12       | 5000  |
| 7       | 200        | 2011 | 15       | 9000  |

**Product**

| product_id | product_name |
|------------|--------------|
| 100        | Nokia        |
| 200        | Apple        |
| 300        | Samsung      |

### Sample Output

| product_id | first_year | quantity | price |
|------------|------------|----------|-------|
| 100        | 2008       | 10       | 5000  |
| 200        | 2011       | 15       | 9000  |

---

## 💡 Solution
```sql
SELECT s.product_id, s.year AS first_year, s.quantity, s.price
FROM Sales s
JOIN (
    SELECT product_id, MIN(year) AS first_year
    FROM Sales
    GROUP BY product_id
) t
ON s.product_id = t.product_id AND s.year = t.first_year;
```

## 🧠 Approach

1. Build subquery `t` that finds the **earliest year** per product using `MIN(year)` grouped by `product_id`.
2. `JOIN` the original `Sales` table `s` with subquery `t` on two conditions: matching `product_id` **and** `s.year = t.first_year` — this filters the outer table down to only the first-year rows for each product.
3. Select `s.product_id`, `s.year` aliased as `first_year`, `s.quantity`, and `s.price` from the matching rows.
4. If a product had multiple sales entries in its first year, all of them are returned correctly since the join preserves every matching row.

---

## 📌 Concepts Used

`MIN()` · `GROUP BY` · `Subquery` · `JOIN` on multiple conditions · `Aliasing` · `First-year filtering`

---

## 💭 My Takeaway

The classic pattern here — subquery to find the `MIN()` per group, then join back to the original table on both the group key and the aggregate value — is one of the most reusable templates in SQL. It safely handles cases where a product has multiple sales in its first year, unlike a simple `WHERE year = MIN(year)` which would be invalid. Worth memorising this join-back pattern cold.