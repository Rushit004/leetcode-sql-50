# 🟢 1327 · List the Products Ordered in a Period

**Difficulty:** Easy | **Topic:** JOIN / GROUP BY / HAVING / Date Filtering     
**LeetCode:** [Problem Link](https://leetcode.com/problems/list-the-products-ordered-in-a-period/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Find the `product_name` and total `unit` ordered for products that had **at least 100 units ordered** in **February 2020**.
Return the result table in any order.

---

### Schema

```sql
CREATE TABLE Products (
  product_id       INT,
  product_name     VARCHAR(255),
  product_category VARCHAR(255)
);

CREATE TABLE Orders (
  product_id INT,
  order_date DATE,
  unit       INT
);
```

### Sample Input

**Products**

| product_id | product_name          | product_category |
|------------|-----------------------|------------------|
| 1          | Leetcode Solutions    | Book             |
| 2          | Jewels of Stringology | Book             |
| 3          | HP                    | Laptop           |
| 4          | Lenovo                | Laptop           |
| 5          | Leetcode Kit          | T-shirt          |

**Orders**

| product_id | order_date | unit |
|------------|------------|------|
| 1          | 2020-02-05 | 60   |
| 1          | 2020-02-10 | 70   |
| 2          | 2020-01-18 | 30   |
| 2          | 2020-02-11 | 80   |
| 3          | 2020-02-17 | 2    |
| 3          | 2020-02-24 | 3    |
| 4          | 2020-03-01 | 20   |
| 4          | 2020-03-04 | 30   |
| 4          | 2020-03-04 | 60   |
| 5          | 2020-02-25 | 50   |
| 5          | 2020-02-27 | 50   |
| 5          | 2020-03-01 | 50   |

### Sample Output

| product_name       | unit |
|--------------------|------|
| Leetcode Solutions | 130  |
| Leetcode Kit       | 100  |

---

### Solution

```sql
SELECT t2.product_name, SUM(t1.unit) AS 'unit'
FROM Orders t1
JOIN Products t2
ON t1.product_id = t2.product_id
WHERE t1.order_date >= '2020-02-01' AND t1.order_date < '2020-03-01'
GROUP BY t2.product_name
HAVING SUM(t1.unit) >= 100;
```

## 🧠 Approach

1. `JOIN` the `Orders` table with `Products` on `product_id` to bring in `product_name` alongside each order row.
2. Filter rows to **February 2020 only** using `order_date >= '2020-02-01' AND order_date < '2020-03-01'` — the range approach safely excludes March without any date function overhead.
3. `GROUP BY product_name` to aggregate all February orders per product.
4. Use `SUM(unit)` to get the total units ordered per product in the period.
5. Apply `HAVING SUM(unit) >= 100` to keep only products that crossed the 100-unit threshold.

---

## 📌 Concepts Used

`JOIN` · `WHERE` date range · `GROUP BY` · `SUM()` · `HAVING` · `Aggregate filtering`

---

## 💭 My Takeaway

The key distinction here is using `WHERE` for row-level date filtering **before** aggregation, then `HAVING` for aggregate-level filtering **after** grouping — mixing these up is a classic SQL mistake. Using a date range comparison (`>= '2020-02-01' AND < '2020-03-01'`) instead of `MONTH()` and `YEAR()` functions is also a good habit as it stays index-friendly.