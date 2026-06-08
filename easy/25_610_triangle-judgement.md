# 🟢 610 · Triangle Judgement

**Difficulty:** Easy | **Topic:** CASE WHEN / Conditional Logic  
**LeetCode:** [Problem Link](https://leetcode.com/problems/triangle-judgement/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

For each row in the `Triangle` table, determine whether the three line segments with lengths `x`, `y`, and `z` can form a **valid triangle**.

A valid triangle must satisfy the **triangle inequality** — the sum of any two sides must be strictly greater than the third side.

Return the result table in any order.

---

### Schema

```sql
CREATE TABLE Triangle (
  x INT,
  y INT,
  z INT,
  PRIMARY KEY (x, y, z)
);
```

### Sample Input

| x  | y  | z  |
|----|----|----|
| 13 | 15 | 30 |
| 10 | 20 | 15 |

### Sample Output

| x  | y  | z  | triangle |
|----|----|----|----------|
| 13 | 15 | 30 | No       |
| 10 | 20 | 15 | Yes      |

---

### Solution

```sql
SELECT x, y, z,
CASE
    WHEN x + y > z AND x + z > y AND z + y > x THEN 'Yes'
    ELSE 'No'
END AS 'triangle'
FROM Triangle
```

## 🧠 Approach

1. For every row, apply the **triangle inequality theorem** — all three conditions must hold simultaneously: `x + y > z`, `x + z > y`, and `y + z > x`.
2. Chain all three checks with `AND` inside a `CASE WHEN` — if all pass, label the row `'Yes'`, otherwise `'No'`.
3. No `GROUP BY`, `JOIN`, or subquery is needed — this is a pure row-level transformation using `CASE WHEN` directly in the `SELECT`.

---

## 📌 Concepts Used

`CASE WHEN` · `AND` · `Conditional Logic` · `Row-level Transformation`

---

## 💭 My Takeaway

Clean one-level problem that's really testing whether you know the triangle inequality theorem more than SQL itself. The SQL part is just translating three math conditions into a `CASE WHEN` block — straightforward once the geometry clicks. Worth remembering that `CASE WHEN` in `SELECT` is not just for aggregation scenarios; it's equally powerful for row-by-row conditional labelling without any grouping at all.