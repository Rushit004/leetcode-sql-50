# 🟡 176 · Second Highest Salary

**Difficulty:** Medium | **Topic:** Subquery / LIMIT & OFFSET / NULL Handling
**LeetCode:** [Problem Link](https://leetcode.com/problems/second-highest-salary/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Find the second highest **distinct** salary from the `Employee` table.
If there is no second highest salary, return `null`.

---

### Schema

```sql
CREATE TABLE Employee (
  id     INT,
  salary INT
);
```

### Sample Input

| id | salary |
|----|--------|
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |

### Sample Output

| SecondHighestSalary |
|---------------------|
| 200                 |

---

### Solution

```sql
SELECT
    (
        SELECT DISTINCT salary
        FROM Employee
        ORDER BY salary DESC
        LIMIT 1 OFFSET 1
    ) AS SecondHighestSalary;
```

## 🧠 Approach

1. Use `DISTINCT` to collapse duplicate salary values so identical amounts don't count as separate ranks.
2. Sort the distinct salaries in descending order with `ORDER BY salary DESC` — highest salary comes first.
3. Use `LIMIT 1 OFFSET 1` to skip the top result and pick exactly the second one.
4. Wrap the whole thing in a scalar subquery aliased as `SecondHighestSalary` — if the subquery returns no rows (only one distinct salary exists), MySQL automatically returns `NULL`.

---

## 📌 Concepts Used

`Scalar Subquery` · `DISTINCT` · `ORDER BY DESC` · `LIMIT` · `OFFSET` · `NULL handling`

---

## 💭 My Takeaway

The scalar subquery wrapper is the elegant trick here — it silently returns `NULL` when no second salary exists, avoiding the need for `IFNULL` or `COALESCE`. Using `DISTINCT` before ordering is critical; without it, duplicate top salaries would be treated as separate ranks and give wrong results.