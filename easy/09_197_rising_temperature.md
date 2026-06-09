## 🟢 197. Rising Temperature

**Difficulty:** Easy | **Topic:** Self JOIN / Date Functions  
**LeetCode:** [Problem Link](https://leetcode.com/problems/rising-temperature/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Find all dates' `id` where the temperature is **higher** than the previous day's temperature.

Return the result table in **any order**.

---

## 🗂️ Schema

```sql
CREATE TABLE Weather (
    id           INT PRIMARY KEY,
    recordDate   DATE,
    temperature  INT
);
```

---

## 📥 Sample Input

**Weather**

| id | recordDate | temperature |
|----|------------|-------------|
| 1  | 2015-01-01 | 10          |
| 2  | 2015-01-02 | 25          |
| 3  | 2015-01-03 | 20          |
| 4  | 2015-01-04 | 30          |

---

## 📤 Sample Output

| id |
|----|
| 2  |
| 4  |

---

## 💡 Solution

```sql
SELECT w1.id
FROM Weather w1
JOIN Weather w2
ON DATEDIFF(w1.recordDate, w2.recordDate) = 1
WHERE w1.temperature > w2.temperature;
```

---

## 🔍 Approach

1. Perform a **Self JOIN** on the `Weather` table, treating `w1` as the current day and `w2` as the previous day.
2. Use `DATEDIFF(w1.recordDate, w2.recordDate) = 1` to match each row with its immediate previous day's row.
3. Apply a `WHERE` filter to only keep rows where the current day's temperature (`w1.temperature`) is greater than the previous day's temperature (`w2.temperature`).
4. Return the `id` of all such matching rows.

---

## 🧠 Concepts Used

`Self JOIN` `DATEDIFF()` `Date Functions` `JOIN` `Table Alias` `Filtering` `WHERE clause`

---

## ✍️ My Takeaway

This problem introduces the concept of a **Self JOIN** — joining a table with itself using two aliases to compare rows within the same table. The `DATEDIFF()` function is key here as it calculates the difference in days between two dates, ensuring we only compare truly consecutive days. Using `= 1` instead of just `>` is important to avoid false matches between non-adjacent dates.
