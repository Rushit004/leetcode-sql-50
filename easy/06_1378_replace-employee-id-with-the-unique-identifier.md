# 🟢 1378. Replace Employee ID With The Unique Identifier

**Difficulty:** Easy | **Topic:** JOIN / LEFT JOIN  
**LeetCode:** [Problem Link](https://leetcode.com/problems/replace-employee-id-with-the-unique-identifier/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Find the **unique ID** of each employee. If an employee does not have a unique ID, show `null` instead.

Return the result table in **any order**.

---

## 🗂️ Schema

```sql
CREATE TABLE Employees (
    id    INT PRIMARY KEY,
    name  VARCHAR(20)
);

CREATE TABLE EmployeeUNI (
    id         INT,
    unique_id  INT,
    PRIMARY KEY (id, unique_id)
);
```

---

## 📥 Sample Input

**Employees**

| id | name     |
|----|----------|
| 1  | Alice    |
| 7  | Bob      |
| 11 | Meir     |
| 90 | Winston  |
| 3  | Jonathan |

**EmployeeUNI**

| id | unique_id |
|----|-----------|
| 3  | 1         |
| 11 | 2         |
| 90 | 3         |

---

## 📤 Sample Output

| unique_id | name     |
|-----------|----------|
| null      | Alice    |
| null      | Bob      |
| 2         | Meir     |
| 3         | Winston  |
| 1         | Jonathan |

---

## 💡 Solution

```sql
SELECT unique_id, name
FROM Employees t1
LEFT JOIN EmployeeUNI t2
ON t1.id = t2.id;
```

---

## 🧠 Approach
1. Start with the `Employees` table as the base (left) table to ensure all employees are included.
2. `LEFT JOIN` with `EmployeeUNI` on the matching `id` column.
3. If an employee has a corresponding entry in `EmployeeUNI`, their `unique_id` is returned.
4. If no match is found, SQL automatically fills `unique_id` with `NULL` — no extra handling needed.
5. Select `unique_id` and `name` in the final output.

---

## 📌 Concepts Used
`LEFT JOIN` `JOIN` `NULL` `Multi-table Query` `Table Alias` `Filtering`

---

## 💭 My Takeaway
This problem is a great introduction to `LEFT JOIN`. The key idea is that a `LEFT JOIN` always keeps **all rows from the left table**, even if there's no matching row in the right table — filling unmatched columns with `NULL`. This is perfect for scenarios where some records may not have associated data in another table.
