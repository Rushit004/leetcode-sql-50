# 🟢 1757 · Recyclable and Low Fat Products

**Difficulty:** Easy | **Topic:** Filtering / WHERE  
**LeetCode:** [Problem Link](https://leetcode.com/problems/recyclable-and-low-fat-products/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Find the ids of products that are both low fat and recyclable.
Return the result table in any order.

---

### Schema

```sql
CREATE TABLE Products (
  product_id INT,
  low_fats ENUM('Y','N'),
  recyclable ENUM('Y','N')
);
```

### Sample Input

| product_id | low_fats | recyclable |
|------------|----------|------------|
| 0          | Y        | N          |
| 1          | Y        | Y          |
| 2          | N        | Y          |
| 3          | Y        | Y          |
| 4          | N        | N          |



### Sample Output

| product_id |
|------------|
| 1          |
| 3          |

---

### Solution

```sql
SELECT product_id
FROM Products
WHERE low_fats = 'Y' AND recyclable = 'Y';
```

## 🧠 Approach

1. Need rows satisfying two conditions at once.
2. Both columns are `ENUM('Y','N')` → string equality works directly.
3. Chain conditions with `AND` in `WHERE`. No JOIN or subquery needed.

---

## 📌 Concepts Used

`WHERE` · `AND` · `ENUM comparison` · `SELECT`

---

## 💭 My Takeaway

Simple problem but a good reminder that ENUM columns compare with
string literals. Solid warm-up for the series.
