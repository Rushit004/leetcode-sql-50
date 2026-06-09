# 🔴 185 · Department Top Three Salaries

**Difficulty:** Hard | **Topic:** Window Functions / DENSE_RANK / JOIN
**LeetCode:** [Problem Link](https://leetcode.com/problems/department-top-three-salaries/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

A high earner in a department is an employee who has a salary in the **top three unique salaries** for that department.

Write a query to find all employees who are high earners in each department.
Return the result table in any order.

---

### Schema

```sql
CREATE TABLE Employee (
  id           INT,
  name         VARCHAR(255),
  salary       INT,
  departmentId INT
);

CREATE TABLE Department (
  id   INT,
  name VARCHAR(255)
);
```

### Sample Input

**Employee**

| id | name  | salary | departmentId |
|----|-------|--------|--------------|
| 1  | Joe   | 85000  | 1            |
| 2  | Henry | 80000  | 2            |
| 3  | Sam   | 60000  | 2            |
| 4  | Max   | 90000  | 1            |
| 5  | Janet | 69000  | 1            |
| 6  | Randy | 85000  | 1            |
| 7  | Will  | 70000  | 1            |

**Department**

| id | name  |
|----|-------|
| 1  | IT    |
| 2  | Sales |

### Sample Output

| Department | Employee | Salary |
|------------|----------|--------|
| IT         | Max      | 90000  |
| IT         | Joe      | 85000  |
| IT         | Randy    | 85000  |
| IT         | Will     | 70000  |
| Sales      | Henry    | 80000  |
| Sales      | Sam      | 60000  |

---

### Solution

```sql
SELECT t.name AS 'Department', t.Employee AS 'Employee', t.salary AS 'Salary'
FROM (
    SELECT t2.name, t1.name AS 'Employee', salary,
    DENSE_RANK() OVER (PARTITION BY departmentId ORDER BY salary DESC) AS 'rank'
    FROM Employee t1
    JOIN Department t2
    ON t1.departmentId = t2.id
) t
WHERE t.rank < 4;
```

## 🧠 Approach

1. `JOIN` the `Employee` table with the `Department` table on `departmentId = id` to bring department names alongside each employee's salary.
2. Apply `DENSE_RANK()` as a window function, partitioned by `departmentId` and ordered by `salary DESC` — this assigns rank 1 to the highest salary within each department, with no gaps for ties.
3. Wrap the ranked result in a subquery aliased as `t`.
4. Filter with `WHERE t.rank < 4` to retain only employees holding rank 1, 2, or 3 within their department — employees with the same salary share the same rank, so all ties are naturally included.

---

## 📌 Concepts Used

`DENSE_RANK()` · `OVER()` · `PARTITION BY` · `ORDER BY DESC` · `JOIN` · `Subquery` · `WHERE filter on window rank`

---

## 💭 My Takeaway

`DENSE_RANK()` is the key choice here over `RANK()` or `ROW_NUMBER()` — it assigns the same rank to duplicate salaries with no gaps, which is exactly what "top three unique salaries" demands. Using `rank < 4` instead of `rank <= 3` is a clean equivalent that reads well. A great problem for cementing the PARTITION BY mental model.