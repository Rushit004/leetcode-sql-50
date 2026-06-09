## 🟢 584. Find Customer Referee

**Difficulty:** Easy | **Topic:** NULL Handling / Filtering  
**LeetCode:** [Problem Link](https://leetcode.com/problems/find-customer-referee/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Find the names of customers who are **not referred** by the customer with `id = 2`.

Return the result table in **any order**.

---

## 🗂️ Schema

```sql
CREATE TABLE Customer (
    id         INT PRIMARY KEY,
    name       VARCHAR(25),
    referee_id INT
);
```

---

## 📥 Sample Input

**Customer**

| id | name | referee_id |
|----|------|------------|
| 1  | Will | null       |
| 2  | Jane | null       |
| 3  | Alex | 2          |
| 4  | Bill | null       |
| 5  | Zack | 1          |
| 6  | Mark | 2          |

---

## 📤 Sample Output

| name |
|------|
| Will |
| Jane |
| Bill |
| Zack |

---

## 💡 Solution

```sql
SELECT name
FROM Customer
WHERE referee_id != 2 OR referee_id IS NULL;
```

---

## 🔍 Approach

1. Select the `name` column from the `Customer` table.
2. Filter out rows where `referee_id = 2` using `!= 2`.
3. Crucially, also include rows where `referee_id IS NULL` — because in SQL, `NULL != 2` evaluates to `NULL` (unknown), **not** `TRUE`, so those rows would be silently dropped without the extra condition.
4. The `OR referee_id IS NULL` clause explicitly captures all customers with no referee.

---

## 🧠 Concepts Used

`WHERE clause` `NULL Handling` `IS NULL` `Three-Valued Logic` `OR condition` `Filtering`

---

## ✍️ My Takeaway

This problem is a classic **NULL trap**. In SQL, any arithmetic or comparison with `NULL` returns `NULL`, not `TRUE` or `FALSE` — this is called **three-valued logic**. So writing `referee_id != 2` alone quietly drops every row where `referee_id` is `NULL`. Always handle `NULL` explicitly with `IS NULL` or `IS NOT NULL` whenever your filter column can be null.
