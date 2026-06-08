## 🟡 1934. Confirmation Rate

**Difficulty:** Medium | **Topic:** LEFT JOIN / Aggregate Functions / IFNULL  
**LeetCode:** [Problem Link](https://leetcode.com/problems/confirmation-rate/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Find the **confirmation rate** of each user.

The confirmation rate of a user is the number of `confirmed` messages divided by the total number of requested confirmation messages. If a user did not request any confirmation messages, their confirmation rate is **0**. Round the result to **2 decimal places**.

Return the result table in **any order**.

---

## 🗂️ Schema

```sql
CREATE TABLE Signups (
    user_id    INT PRIMARY KEY,
    time_stamp DATETIME
);

CREATE TABLE Confirmations (
    user_id    INT,
    time_stamp DATETIME,
    action     ENUM('confirmed', 'timeout'),
    PRIMARY KEY (user_id, time_stamp)
);
```

---

## 📥 Sample Input

**Signups**

| user_id | time_stamp          |
|---------|---------------------|
| 3       | 2020-03-21 10:16:13 |
| 7       | 2020-01-04 13:57:59 |
| 2       | 2020-07-29 23:09:44 |
| 6       | 2020-12-09 10:39:37 |

**Confirmations**

| user_id | time_stamp          | action    |
|---------|---------------------|-----------|
| 3       | 2021-01-06 03:30:46 | timeout   |
| 3       | 2021-07-14 14:00:00 | timeout   |
| 7       | 2021-06-12 11:57:29 | confirmed |
| 7       | 2021-06-13 12:58:28 | confirmed |
| 7       | 2021-06-14 13:59:27 | confirmed |
| 2       | 2021-01-22 00:00:00 | confirmed |
| 2       | 2021-02-28 23:59:59 | timeout   |

---

## 📤 Sample Output

| user_id | confirmation_rate |
|---------|-------------------|
| 6       | 0.00              |
| 3       | 0.00              |
| 7       | 1.00              |
| 2       | 0.50              |

---

## 💡 Solution

```sql
SELECT 
    s.user_id,
    ROUND(
        IFNULL(SUM(c.action = 'confirmed') / COUNT(c.action), 0),
        2
    ) AS confirmation_rate
FROM Signups s
LEFT JOIN Confirmations c
ON s.user_id = c.user_id
GROUP BY s.user_id;
```

---

## 🔍 Approach

1. Start with the `Signups` table as the base (left) table to ensure every user is included, even those with no confirmation requests.
2. `LEFT JOIN` with the `Confirmations` table on `user_id` — users with no confirmations will have `NULL` for all `Confirmations` columns.
3. `GROUP BY s.user_id` to aggregate all confirmation records per user.
4. Use `SUM(c.action = 'confirmed')` to count confirmed messages — in MySQL, a boolean expression evaluates to `1` (true) or `0` (false), so summing it gives the total confirmed count.
5. Divide by `COUNT(c.action)` to get the confirmation ratio — `COUNT` ignores `NULL`, so users with no records get `NULL` from the division.
6. Wrap with `IFNULL(..., 0)` to replace `NULL` with `0` for users who never requested a confirmation.
7. Finally, `ROUND(..., 2)` formats the result to 2 decimal places.

---

## 🧠 Concepts Used

`LEFT JOIN` `GROUP BY` `SUM()` `COUNT()` `ROUND()` `IFNULL()` `Boolean Expression in Aggregation` `NULL Handling` `Aggregate Functions`

---

## ✍️ My Takeaway

This problem introduces a very elegant MySQL trick — using a **boolean expression inside `SUM()`** to conditionally count rows matching a condition, instead of using `CASE WHEN`. The combination of `IFNULL` with `LEFT JOIN` is also a key pattern here — since users with no confirmations produce `NULL` from the division, `IFNULL` cleanly handles it. This pattern of `SUM(condition) / COUNT(column)` is a reusable template for computing rates in SQL.