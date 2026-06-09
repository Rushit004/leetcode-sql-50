# 🟡 1907. Count Salary Categories

**Difficulty:** Medium | **Topic:** Database / UNION ALL / LEFT JOIN   
**LeetCode:** [Problem Link](https://leetcode.com/problems/count-salary-categories/)

---

## 📋 Problem Statement

Given a table `Accounts`, categorize each account's income into one of three salary buckets and count the number of accounts in each category.

- **Low Salary** — income strictly less than `20000`
- **Average Salary** — income between `20000` and `50000` (inclusive)
- **High Salary** — income strictly greater than `50000`

Return all three categories even if some have **zero accounts**.

---

## 🗃️ Schema

```sql
CREATE TABLE Accounts (
    account_id INT PRIMARY KEY,
    income     INT
);
```

---

## 📥 Sample Input

**Accounts**

| account_id | income |
|------------|--------|
| 3          | 108939 |
| 2          | 12747  |
| 8          | 87709  |
| 6          | 91796  |

---

## 📤 Sample Output

| category       | accounts_count |
|----------------|----------------|
| Low Salary     | 1              |
| Average Salary | 0              |
| High Salary    | 3              |

---

## 💡 Solution

```sql
SELECT c.category,
       COUNT(a.account_id) AS accounts_count
FROM (
    SELECT 'Low Salary' AS category
    UNION ALL
    SELECT 'Average Salary'
    UNION ALL
    SELECT 'High Salary'
) c
LEFT JOIN Accounts a
ON (
    (a.income < 20000 AND c.category = 'Low Salary') OR
    (a.income BETWEEN 20000 AND 50000 AND c.category = 'Average Salary') OR
    (a.income > 50000 AND c.category = 'High Salary')
)
GROUP BY c.category;
```

---

## 🪜 Approach

1. Build a derived table `c` using `UNION ALL` to hardcode all three category labels — this guarantees every category appears in the output even with zero matches.
2. `LEFT JOIN` the `Accounts` table onto `c` using a multi-condition `ON` clause that maps each income range to its corresponding category label.
3. Use `COUNT(a.account_id)` instead of `COUNT(*)` so that unmatched rows from the left side (zero-account categories) are correctly counted as `0`.
4. `GROUP BY c.category` to aggregate the count per bucket.

---

## 🧠 Concepts Used

`UNION ALL` `LEFT JOIN` `COUNT()` `GROUP BY` `BETWEEN` `Derived Table` `Conditional JOIN`

---

## ✍️ My Takeaway

The main challenge here is ensuring zero-count categories still appear in the result. Using a hardcoded category table with `UNION ALL` as the left side of a `LEFT JOIN` is an elegant pattern for this — it acts as a guaranteed row anchor. Using `COUNT(a.account_id)` instead of `COUNT(*)` is a subtle but critical detail to correctly return `0` instead of `1` for unmatched categories.