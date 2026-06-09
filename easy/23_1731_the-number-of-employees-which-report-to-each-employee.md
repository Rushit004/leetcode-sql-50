# 🟢 1731 · The Number of Employees Which Report to Each Employee

**Difficulty:** Easy | **Topic:** Self Join / Aggregation  
**LeetCode:** [Problem Link](https://leetcode.com/problems/the-number-of-employees-which-report-to-each-employee/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Find the managers — employees who have at least one direct report — and for each report:

- The number of employees that **directly report** to them (`reports_count`)
- The **average age** of those direct reports, rounded to the nearest integer (`average_age`)

Return the result table ordered by `employee_id` in **ascending order**.

---

## 🗂️ Schema
```sql
CREATE TABLE Employees (
  employee_id INT PRIMARY KEY,
  name        VARCHAR(20),
  reports_to  INT,
  age         INT
);
```

### Sample Input

| employee_id | name    | reports_to | age |
|-------------|---------|------------|-----|
| 9           | Hercy   | null       | 43  |
| 6           | Alice   | 9          | 41  |
| 4           | Bob     | 9          | 36  |
| 2           | Winston | null       | 37  |


### Sample Output

| employee_id | name  | reports_count | average_age |
|-------------|-------|---------------|-------------|
| 9           | Hercy | 2             | 39          |

---

## 💡 Solution
```sql
SELECT t1.employee_id, t1.name, COUNT(*) AS 'reports_count', ROUND(AVG(t2.age)) AS 'average_age'
FROM Employees t1
CROSS JOIN Employees t2
WHERE t1.employee_id = t2.reports_to
GROUP BY t1.employee_id
ORDER BY employee_id
```

## 🧠 Approach

1. **Self-join** the `Employees` table as `t1` (managers) and `t2` (subordinates) using a `CROSS JOIN` — this produces every possible employee pair combination.
2. The `WHERE t1.employee_id = t2.reports_to` condition then filters the cartesian product down to only valid manager–subordinate pairs, effectively making it an inner join on the reporting relationship.
3. `COUNT(*)` counts how many employees report directly to each manager.
4. `AVG(t2.age)` computes the average age of the direct reports, and `ROUND()` with no second argument rounds to the nearest whole integer.
5. `GROUP BY t1.employee_id` collapses all subordinate rows per manager into a single summary row.
6. `ORDER BY employee_id` returns the result in ascending order as required.

---

## 📌 Concepts Used

`Self Join` · `CROSS JOIN` · `WHERE` · `COUNT()` · `AVG()` · `ROUND()` · `GROUP BY` · `ORDER BY`

---

## 💭 My Takeaway

Using `CROSS JOIN` + `WHERE` here is functionally identical to a regular `JOIN ... ON` — both produce the same result, just written differently. The more interesting observation is that only employees who appear in `t2.reports_to` end up in the output, meaning managers with zero reports are automatically excluded — which is exactly what the problem wants. A good reminder that self-joins are the go-to tool whenever a table encodes a hierarchical relationship within itself.