# 🟢 1581. Customer Who Visited but Did Not Make Any Transactions

**Difficulty:** Easy | **Topic:** LEFT JOIN / NULL Handling / GROUP BY  
**LeetCode:** [Problem Link](https://leetcode.com/problems/customer-who-visited-but-did-not-make-any-transactions/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Find the `customer_id` and the number of times they visited the mall **without making any transactions**.

Return the result table in **any order**.

---

## 🗂️ Schema

```sql
CREATE TABLE Visits (
    visit_id    INT PRIMARY KEY,
    customer_id INT
);

CREATE TABLE Transactions (
    transaction_id INT PRIMARY KEY,
    visit_id       INT,
    amount         INT
);
```

---

## 📥 Sample Input

**Visits**

| visit_id | customer_id |
|----------|-------------|
| 1        | 23          |
| 2        | 9           |
| 4        | 30          |
| 5        | 54          |
| 6        | 96          |
| 7        | 54          |
| 8        | 54          |

**Transactions**

| transaction_id | visit_id | amount |
|----------------|----------|--------|
| 2              | 5        | 310    |
| 3              | 5        | 300    |
| 9              | 5        | 200    |
| 12             | 1        | 910    |
| 13             | 2        | 970    |

---

## 📤 Sample Output

| customer_id | count_no_trans |
|-------------|----------------|
| 54          | 2              |
| 30          | 1              |
| 96          | 1              |

---

## 💡 Solution

```sql
SELECT customer_id, COUNT(t1.visit_id) AS 'count_no_trans'
FROM Visits t1
LEFT JOIN Transactions t2
ON t1.visit_id = t2.visit_id
WHERE t2.visit_id IS NULL
GROUP BY customer_id;
```

---

## 🔍 Approach

1. Start with the `Visits` table as the base (left) table to keep all visit records.
2. `LEFT JOIN` with the `Transactions` table on `visit_id` — visits with no matching transaction will have `NULL` in all `Transactions` columns.
3. Use `WHERE t2.visit_id IS NULL` to filter only those visits that had **no transaction** at all.
4. `GROUP BY customer_id` to group all no-transaction visits per customer.
5. Use `COUNT(t1.visit_id)` to count how many such visits each customer made.

---

## 🧠 Concepts Used

`LEFT JOIN` `NULL Handling` `IS NULL` `GROUP BY` `COUNT()` `WHERE clause` `Aggregate Functions` `Table Alias`

---

## ✍️ My Takeaway

This problem teaches a classic **anti-join** pattern in SQL — using `LEFT JOIN` + `WHERE right_table.column IS NULL` to find rows in the left table that have **no match** in the right table. This is a cleaner and often more efficient alternative to using `NOT IN` or `NOT EXISTS`. Whenever the question asks "find records that don't have a corresponding entry somewhere", this pattern should be the first thing that comes to mind.
