# 🟢 1789 · Primary Department for Each Employee

**Difficulty:** Easy | **Topic:** UNION / Filtering / GROUP BY  
**LeetCode:** [Problem Link](https://leetcode.com/problems/primary-department-for-each-employee/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Find the **primary department** for each employee.

Employees can belong to multiple departments. When an employee belongs to only **one** department, their `primary_flag` will be `'N'`, but that department is still considered their primary. When an employee belongs to multiple departments, their primary department has `primary_flag = 'Y'`.

Return the result table in any order.

---

### Schema

```sql
CREATE TABLE Employee (
  employee_id   INT,
  department_id INT,
  primary_flag  ENUM('Y', 'N'),
  PRIMARY KEY (employee_id, department_id)
);
```

### Sample Input

| employee_id | department_id | primary_flag |
|-------------|---------------|--------------|
| 1           | 1             | N            |
| 2           | 1             | Y            |
| 2           | 2             | N            |
| 3           | 3             | N            |
| 4           | 2             | N            |
| 4           | 3             | Y            |
| 4           | 4             | N            |


### Sample Output

| employee_id | department_id |
|-------------|---------------|
| 1           | 1             |
| 2           | 1             |
| 3           | 3             |
| 4           | 3             |

---

### Solution

```sql
SELECT employee_id, department_id
FROM Employee
WHERE primary_flag = 'Y'

UNION

SELECT employee_id, department_id
FROM Employee
GROUP BY employee_id
HAVING COUNT(*) = 1;
```

## 🧠 Approach

1. The problem has two distinct cases that need to be handled separately and merged — a natural fit for `UNION`.
2. **First branch** — `WHERE primary_flag = 'Y'` picks the explicitly marked primary department for employees who belong to multiple departments.
3. **Second branch** — `GROUP BY employee_id` with `HAVING COUNT(*) = 1` isolates employees who belong to exactly one department; since they have no choice, that single department is their primary regardless of the `'N'` flag.
4. `UNION` (not `UNION ALL`) merges both result sets and removes any duplicates, though in practice no row can satisfy both conditions simultaneously.

---

## 📌 Concepts Used

`UNION` · `WHERE` · `GROUP BY` · `HAVING` · `COUNT()` · `ENUM filtering` · `Set Operations`

---

## 💭 My Takeaway

The key insight is recognising that the problem splits into two logically separate cases — multi-department employees (use the `'Y'` flag) and single-department employees (flag is always `'N'`, but they still have a primary). Trying to solve both cases in one `WHERE` or one `GROUP BY` gets messy fast; `UNION` keeps each case clean and readable. A good reminder that set operations like `UNION` are not just for combining different tables — they're equally useful for handling multiple logical conditions on the same table.