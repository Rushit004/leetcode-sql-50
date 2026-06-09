# 🟢 1075 · Project Employees I

**Difficulty:** Easy | **Topic:** Joins / Aggregation  
**LeetCode:** [Problem Link](https://leetcode.com/problems/project-employees-i/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Find the **average experience years** of all employees for each project, rounded to **2 decimal places**.

Return the result table in any order.

---

## 🗂️ Schema
```sql
CREATE TABLE Project (
  project_id  INT,
  employee_id INT,
  PRIMARY KEY (project_id, employee_id)
);

CREATE TABLE Employee (
  employee_id      INT PRIMARY KEY,
  name             VARCHAR(10),
  experience_years INT
);
```

### Sample Input

**Project** table:

| project_id | employee_id |
|------------|-------------|
| 1          | 1           |
| 1          | 2           |
| 1          | 3           |
| 2          | 1           |
| 2          | 4           |

**Employee** table:

| employee_id | name   | experience_years |
|-------------|--------|------------------|
| 1           | Khaled | 3                |
| 2           | Ali    | 2                |
| 3           | John   | 1                |
| 4           | Doe    | 2                |


### Sample Output

| project_id | average_years |
|------------|---------------|
| 1          | 2.00          |
| 2          | 2.50          |

---

## 💡 Solution
```sql
SELECT project_id, ROUND(AVG(t2.experience_years), 2) AS 'average_years'
FROM Project t1
JOIN Employee t2
  ON t1.employee_id = t2.employee_id
GROUP BY project_id
```

## 🧠 Approach

1. `JOIN` `Project` with `Employee` on `employee_id` to bring each employee's `experience_years` alongside their project.
2. `GROUP BY project_id` to aggregate all employees belonging to the same project into one row.
3. Apply `AVG(experience_years)` to compute the mean experience across all employees in that project.
4. Wrap with `ROUND(..., 2)` to format the result to 2 decimal places as required.

---

## 📌 Concepts Used

`JOIN` · `AVG()` · `ROUND()` · `GROUP BY`

---

## 💭 My Takeaway

Clean and minimal problem — a good drill for the `JOIN` → `GROUP BY` → aggregate pattern that appears constantly in SQL. The only thing to watch is that `AVG()` already handles the division internally, so no manual `SUM() / COUNT()` is needed. `ROUND(..., 2)` on top keeps the output tidy.