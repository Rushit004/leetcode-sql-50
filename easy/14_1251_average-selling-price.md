# 🟢 1251 · Average Selling Price

**Difficulty:** Easy | **Topic:** Joins / Aggregation / CASE WHEN  
**LeetCode:** [Problem Link](https://leetcode.com/problems/average-selling-price/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Find the **average selling price** for each product.

`average_price` should be **rounded to 2 decimal places**. If a product does not have any sold units, its average selling price is `0`.

Return the result table in any order.

---

### Schema

```sql
CREATE TABLE Prices (
  product_id  INT,
  start_date  DATE,
  end_date    DATE,
  price       INT,
  PRIMARY KEY (product_id, start_date, end_date)
);

CREATE TABLE UnitsSold (
  product_id    INT,
  purchase_date DATE,
  units         INT
);
```

### Sample Input

**Prices** table:

| product_id | start_date | end_date   | price |
|------------|------------|------------|-------|
| 1          | 2019-02-17 | 2019-02-28 | 5     |
| 1          | 2019-03-01 | 2019-03-22 | 20    |
| 2          | 2019-02-01 | 2019-02-20 | 15    |
| 2          | 2019-02-21 | 2019-03-31 | 30    |

**UnitsSold** table:

| product_id | purchase_date | units |
|------------|---------------|-------|
| 1          | 2019-02-25    | 100   |
| 1          | 2019-03-01    | 15    |
| 2          | 2019-02-10    | 200   |
| 2          | 2019-03-22    | 30    |


### Sample Output

| product_id | average_price |
|------------|---------------|
| 1          | 6.96          |
| 2          | 16.96         |

---

### Solution

```sql
SELECT 
    p.product_id,
    ROUND(
        CASE 
            WHEN SUM(u.units) = 0 OR SUM(u.units) IS NULL THEN 0
            ELSE SUM(u.units * p.price) / SUM(u.units)
        END,
        2
    ) AS average_price
FROM Prices p
LEFT JOIN UnitsSold u
    ON p.product_id = u.product_id
    AND u.purchase_date BETWEEN p.start_date AND p.end_date
GROUP BY p.product_id;
```

## 🧠 Approach

1. `LEFT JOIN` `UnitsSold` onto `Prices` so products with zero sales are still included in the result.
2. The join condition uses `BETWEEN p.start_date AND p.end_date` to match each sale to the correct price tier active on that `purchase_date`.
3. Compute weighted average as `SUM(units * price) / SUM(units)` — this correctly accounts for different prices across different date ranges.
4. Wrap in a `CASE WHEN` to handle products with no sales (`SUM(units) IS NULL` or `0`), returning `0` instead of a division error.
5. `ROUND(..., 2)` formats the result to 2 decimal places as required.

---

## 📌 Concepts Used

`LEFT JOIN` · `BETWEEN` · `CASE WHEN` · `SUM()` · `ROUND()` · `GROUP BY` · `Weighted Average` · `NULL handling`

---

## 💭 My Takeaway

The real challenge here is the **date-range join** — each sale must match the price that was active on its purchase date, not just any price for that product. Using `BETWEEN` directly inside the `ON` clause is an elegant way to handle this without subqueries. The `CASE WHEN` guard for zero units is also a good habit to build — silent division-by-zero bugs are easy to miss in aggregation queries.