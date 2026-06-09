# 🟢 619 · Biggest Single Number

**Difficulty:** Easy | **Topic:** Subquery / Aggregation / MAX  
**LeetCode:** [Problem Link](https://leetcode.com/problems/biggest-single-number/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Find the **largest single number** in the table. A **single number** is a number that appears **only once** in the table.

If there is no single number, return `null`.

---

## 🗂️ Schema
```sql
CREATE TABLE MyNumbers (
  num INT
);
```

### Sample Input

| num |
|-----|
| 8   |
| 8   |
| 3   |
| 3   |
| 1   |
| 4   |
| 5   |
| 6   |

### Sample Output

| num |
|-----|
| 6   |

---

## 💡 Solution
```sql
SELECT MAX(t.num) AS 'num'
FROM (
    SELECT num, COUNT(num) AS 'cnt'
    FROM MyNumbers
    GROUP BY num
    HAVING cnt = 1
) t
```

## 🧠 Approach

1. The **inner subquery** groups rows by `num` and uses `HAVING cnt = 1` to keep only numbers that appear exactly once — these are the single numbers.
2. The **outer query** wraps the subquery as a derived table `t` and applies `MAX()` to find the largest among all single numbers.
3. If no single number exists, the subquery returns an empty set and `MAX()` of an empty set naturally returns `NULL` — satisfying the null requirement without any extra `IFNULL` or `CASE WHEN`.

---

## 📌 Concepts Used

`Subquery` · `Derived Table` · `GROUP BY` · `HAVING` · `COUNT()` · `MAX()` · `NULL handling`

---

## 💭 My Takeaway

The elegant part of this solution is that `MAX()` on an empty set returns `NULL` automatically — no need for an explicit null guard. The two-layer approach (filter singles in subquery → pick max in outer query) is a clean pattern to internalise: when you need to aggregate on top of an already-aggregated result, a derived table or CTE is almost always the right structure. Trying to do both in one query level would require nested aggregates, which SQL doesn't allow directly.