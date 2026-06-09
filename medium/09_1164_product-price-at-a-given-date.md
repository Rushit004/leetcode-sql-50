# 🟡 1164. Product Price at a Given Date

**Difficulty:** Medium | **Topic:** Database / Subquery / UNION   
**LeetCode:** [Problem Link](https://leetcode.com/problems/product-price-at-a-given-date/)

---

## 📋 Problem Statement

Given a table `Products`, find the price of each product on `2019-08-16`. Assume the initial price of all products before any change is `10`.

Return the result in **any order**.

---

## 🗂️ Schema
```sql
CREATE TABLE Products (
    product_id  INT,
    new_price   INT,
    change_date DATE
);
```

---

## 📥 Sample Input

**Products**

| product_id | new_price | change_date |
|------------|-----------|-------------|
| 1          | 20        | 2019-08-14  |
| 2          | 50        | 2019-08-14  |
| 1          | 30        | 2019-08-15  |
| 1          | 35        | 2019-08-16  |
| 2          | 65        | 2019-08-17  |
| 3          | 20        | 2019-08-18  |

---

## 📤 Sample Output

| product_id | price |
|------------|-------|
| 1          | 35    |
| 2          | 50    |
| 3          | 10    |

---

## 💡 Solution

```sql
SELECT 
    product_id,
    new_price AS price
FROM Products
WHERE (product_id, change_date) IN (
    SELECT product_id, MAX(change_date)
    FROM Products
    WHERE change_date <= '2019-08-16'
    GROUP BY product_id
)

UNION

SELECT 
    product_id,
    10 AS price
FROM Products
WHERE product_id NOT IN (
    SELECT product_id
    FROM Products
    WHERE change_date <= '2019-08-16'
)
GROUP BY product_id;
```

---

## 🧠 Approach
1. In the first `SELECT`, use a subquery to find the **most recent `change_date` on or before `2019-08-16`** for each product using `MAX(change_date)` grouped by `product_id`.
2. Match `(product_id, change_date)` as a composite key with `IN` to retrieve the corresponding `new_price` — the product's effective price on that date.
3. In the second `SELECT`, identify products with **no price change on or before `2019-08-16`** using `NOT IN` on the same date filter.
4. Assign a default price of `10` to those products as per the problem constraint.
5. `UNION` both results to produce the complete list of all products with their prices on `2019-08-16`.

---

## 📌 Concepts Used
`UNION` `Subquery` `MAX()` `GROUP BY` `Composite Key Filtering` `NOT IN` `Date Comparison`

---

## 💭 My Takeaway
This problem is a great exercise in handling two separate cases — products that *have* a price record before the target date, and those that *don't*. Using a composite `(product_id, change_date)` pair inside `IN` cleanly pinpoints the latest price per product. `UNION` neatly stitches both cases into one final result.