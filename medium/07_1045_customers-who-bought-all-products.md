# 🟡 1045 · Customers Who Bought All Products

**Difficulty:** Medium | **Topic:** GROUP BY / HAVING / Scalar Subquery / COUNT DISTINCT   
**LeetCode:** [Problem Link](https://leetcode.com/problems/customers-who-bought-all-products/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Find all `customer_id`s from the `Customer` table that have bought **every product** listed in the `Product` table.
Return the result table in any order.

---

### Schema

```sql
CREATE TABLE Customer (
  customer_id INT,
  product_key INT
);
-- May contain duplicate rows. customer_id is NOT NULL.
-- product_key is a foreign key referencing Product.

CREATE TABLE Product (
  product_key INT PRIMARY KEY
);
```

### Sample Input

**Customer**

| customer_id | product_key |
|-------------|-------------|
| 1           | 5           |
| 2           | 6           |
| 3           | 5           |
| 3           | 6           |
| 1           | 6           |

**Product**

| product_key |
|-------------|
| 5           |
| 6           |

### Sample Output

| customer_id |
|-------------|
| 1           |
| 3           |

---

### Solution

```sql
SELECT customer_id
FROM Customer
GROUP BY customer_id
HAVING COUNT(DISTINCT product_key) = (SELECT COUNT(*) FROM Product);
```

## 🧠 Approach

1. `GROUP BY customer_id` to bucket all purchase rows per customer.
2. Use `COUNT(DISTINCT product_key)` to count how many unique products each customer has bought — `DISTINCT` handles duplicate purchase rows in the `Customer` table.
3. Use a scalar subquery `(SELECT COUNT(*) FROM Product)` to get the total number of products that exist in the catalogue.
4. The `HAVING` clause compares the two counts — only customers whose distinct purchase count **equals** the total product count have bought every product.

---

## 📌 Concepts Used

`GROUP BY` · `HAVING` · `COUNT(DISTINCT)` · `Scalar subquery` · `COUNT(*)` · `Set equality via counting`

---

## 💭 My Takeaway

This is a textbook "relational division" problem — finding rows that satisfy a condition for every member of another set. The clean SQL trick is to sidestep actual set intersection by comparing counts: if a customer's distinct product count equals the total product count, they must have bought all of them. Simple, efficient, and far more readable than a correlated NOT EXISTS approach.