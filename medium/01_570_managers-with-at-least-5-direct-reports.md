## 🟡 570. Managers with at Least 5 Direct Reports

**Difficulty:** Medium | **Topic:** Self JOIN / GROUP BY / HAVING   
**LeetCode:** [Problem Link](https://leetcode.com/problems/managers-with-at-least-5-direct-reports/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Find the managers who have **at least 5 direct reports**.

Return the result table in **any order**.

---

## 🗂️ Schema

```sql
CREATE TABLE Employee (
    id        INT PRIMARY KEY,
    name      VARCHAR(255),
    department VARCHAR(255),
    managerId  INT
);
```

---

## 📥 Sample Input

**Employee**

| id  | name  | department | managerId |
|-----|-------|------------|-----------|
| 101 | John  | A          | null      |
| 102 | Dan   | A          | 101       |
| 103 | James | A          | 101       |
| 104 | Amy   | A          | 101       |
| 105 | Anne  | A          | 101       |
| 106 | Ron   | B          | 101       |

---

## 📤 Sample Output

| name |
|------|
| John |

---

## 💡 Solution

```sql
SELECT e1.name
FROM Employee e1
JOIN Employee e2
ON e1.id = e2.managerId
GROUP BY e1.id, e1.name
HAVING COUNT(e2.id) >= 5;
```

---

## 🧠 Approach
1. Perform a **Self JOIN** on the `Employee` table — `e1` represents the manager and `e2` represents the direct reports.
2. Join condition `e1.id = e2.managerId` links each manager to all their direct reports.
3. `GROUP BY e1.id, e1.name` groups all direct reports under their respective manager.
4. Use `HAVING COUNT(e2.id) >= 5` to filter only those managers who have **5 or more** direct reports.
5. Return the `name` of all such qualifying managers.

---

## 📌 Concepts Used
`Self JOIN` `GROUP BY` `HAVING` `COUNT()` `Aggregate Functions` `Table Alias` `Filtering`

---

## 💭 My Takeaway
This problem combines **Self JOIN** with **aggregation** — a very powerful pattern in SQL. The key distinction here is using `HAVING` instead of `WHERE` for filtering on aggregated results. `WHERE` filters rows before grouping, while `HAVING` filters after grouping. Also, grouping by both `e1.id` and `e1.name` is a good practice to avoid ambiguity, especially when names might not be unique across the table.
