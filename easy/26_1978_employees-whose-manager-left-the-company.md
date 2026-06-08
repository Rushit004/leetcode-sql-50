# 🟢 1978 · Employees Whose Manager Left the Company

**Difficulty:** Easy | **Topic:** Subqueries / Filtering  
**LeetCode:** [Problem Link](https://leetcode.com/problems/employees-whose-manager-left-the-company/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Find the IDs of employees whose salary is strictly less than $30,000 and whose manager has left the company (i.e., their `manager_id` does not appear in the `employee_id` column).  
Return the result ordered by `employee_id`.

---

### Schema

```sql
CREATE TABLE Employees (
  employee_id INT,
  name VARCHAR(20),
  manager_id INT,
  salary INT
);
```

### Sample Input

| employee_id | name      | manager_id | salary |
|-------------|-----------|------------|--------|
| 3           | Mila      | 9          | 60301  |
| 12          | Antonella | NULL       | 31000  |
| 13          | Emery     | NULL       | 67084  |
| 1           | Kalel     | 11         | 21241  |
| 9           | Mikaela   | NULL       | 50937  |
| 11          | Joziah    | 6          | 28485  |

### Sample Output

| employee_id |
|-------------|
| 11          |

---

### Solution

```sql
SELECT employee_id
FROM Employees 
WHERE salary < 30000
AND manager_id NOT IN (SELECT employee_id FROM Employees)
ORDER BY employee_id;
```

## 🧠 Approach

1. Filter employees with `salary < 30000` — only underpaid employees qualify.
2. The tricky part: we need employees whose **manager no longer exists** in the table.
3. Use a subquery to get all current `employee_id`s, then check if `manager_id` is `NOT IN` that list.
4. Employees with `NULL` manager_id are excluded naturally — they have no manager to begin with.
5. `ORDER BY employee_id` for clean sorted output.

---

## 📌 Concepts Used

`WHERE` · `Subquery` · `NOT IN` · `ORDER BY` · `NULL handling`

---

## 💭 My Takeaway

The `NOT IN` with a subquery is clean here, but I have to remember it silently drops NULLs — if `manager_id` is NULL, the row won't match anyway, which actually works in our favor for this problem.