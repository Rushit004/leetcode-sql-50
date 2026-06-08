# 🟡 1193 · Monthly Transactions I

**Difficulty:** Medium | **Topic:** Aggregation / CASE WHEN / GROUP BY  
**LeetCode:** [Problem Link](https://leetcode.com/problems/monthly-transactions-i/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

For each **month** and **country**, find the number of transactions and their total amount, as well as the number of **approved** transactions and their total amount.

Return the result table in any order.

---

### Schema

```sql
CREATE TABLE Transactions (
  id         INT PRIMARY KEY,
  country    VARCHAR(4),
  state      ENUM('approved', 'declined'),
  amount     INT,
  trans_date DATE
);
```

### Sample Input

| id  | country | state    | amount | trans_date |
|-----|---------|----------|--------|------------|
| 121 | US      | approved | 1000   | 2018-12-18 |
| 122 | US      | declined | 2000   | 2018-12-19 |
| 123 | US      | approved | 2000   | 2019-01-01 |
| 124 | DE      | approved | 2000   | 2019-01-07 |


### Sample Output

| month   | country | trans_count | approved_count | trans_total_amount | approved_total_amount |
|---------|---------|-------------|----------------|--------------------|-----------------------|
| 2018-12 | US      | 2           | 1              | 3000               | 1000                  |
| 2019-01 | US      | 1           | 1              | 2000               | 2000                  |
| 2019-01 | DE      | 1           | 1              | 2000               | 2000                  |

---

### Solution

```sql
SELECT
    DATE_FORMAT(trans_date, '%Y-%m') AS month,
    country,
    COUNT(*) AS trans_count,
    SUM(CASE WHEN state = 'approved' THEN 1 ELSE 0 END) AS approved_count,
    SUM(amount) AS trans_total_amount,
    SUM(CASE WHEN state = 'approved' THEN amount ELSE 0 END) AS approved_total_amount
FROM Transactions
GROUP BY month, country
ORDER BY month, country;
```

## 🧠 Approach

1. Use `DATE_FORMAT(trans_date, '%Y-%m')` to extract the year-month string from the date, grouping all transactions within the same calendar month together.
2. `GROUP BY month, country` creates one row per unique month–country combination.
3. `COUNT(*)` gives the total number of transactions regardless of state.
4. `SUM(CASE WHEN state = 'approved' THEN 1 ELSE 0 END)` conditionally counts only approved transactions by treating each approved row as `1` and declined as `0`.
5. `SUM(amount)` sums all transaction amounts unconditionally for `trans_total_amount`.
6. `SUM(CASE WHEN state = 'approved' THEN amount ELSE 0 END)` sums only the amounts of approved transactions for `approved_total_amount`.

---

## 📌 Concepts Used

`DATE_FORMAT()` · `GROUP BY` · `COUNT()` · `SUM()` · `CASE WHEN` · `Conditional Aggregation` · `ENUM filtering`

---

## 💭 My Takeaway

This problem is a great introduction to **conditional aggregation** — the pattern of wrapping `CASE WHEN` inside `SUM()` to selectively count or total rows that match a condition, all within a single pass over the table. Far cleaner than writing multiple subqueries. `DATE_FORMAT('%Y-%m')` is also a go-to tool whenever a problem asks to group by month, and it's worth memorising that alias for use directly in `GROUP BY`.