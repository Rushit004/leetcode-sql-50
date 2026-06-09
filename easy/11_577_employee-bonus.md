# 🟢 577. Employee Bonus

**Difficulty:** Easy | **Topic:** LEFT JOIN / NULL Handling  
**LeetCode:** [Problem Link](https://leetcode.com/problems/employee-bonus/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Find the `name` and `bonus` of each employee whose bonus is **less than 1000** or has **no bonus** at all.

Return the result table in **any order**.

---

## 🗂️ Schema

```sql
CREATE TABLE Employee (
    empId     INT PRIMARY KEY,
    name      VARCHAR(255),
    supervisor INT,
    salary    INT
);

CREATE TABLE Bonus (
    empId  INT PRIMARY KEY,
    bonus  INT
);
```

---

## 📥 Sample Input

**Employee**

| empId | name   | supervisor | salary |
|-------|--------|------------|--------|
| 3     | Brad   | null       | 4000   |
| 1     | John   | 3          | 1000   |
| 2     | Dan    | 3          | 2000   |
| 4     | Thomas | 3          | 4000   |

**Bonus**

| empId | bonus |
|-------|-------|
| 2     | 500   |
| 4     | 2000  |

---

## 📤 Sample Output

| name | bonus |
|------|-------|
| Brad | null  |
| John | null  |
| Dan  | 500   |

---

## 💡 Solution

```sql
SELECT name, bonus
FROM Employee t1
LEFT JOIN Bonus t2
ON t1.empId = t2.empId
WHERE bonus < 1000 OR bonus IS NULL;
```

---

## 🧠 Approach
1. Start with the `Employee` table as the base (left) table to ensure all employees are included.
2. `LEFT JOIN` with the `Bonus` table on matching `empId` — employees with no bonus entry will have `NULL` in the `bonus` column.
3. Apply a `WHERE` filter with two conditions joined by `OR`.
4. First condition keeps employees with `bonus < 1000`.
5. Second condition `bonus IS NULL` explicitly captures employees who have no bonus entry at all — since `NULL < 1000` evaluates to `NULL` (not `TRUE`), these rows would be lost without this extra check.

---

## 📌 Concepts Used
`LEFT JOIN` `NULL Handling` `IS NULL` `WHERE clause` `OR condition` `Multi-table Query` `Table Alias`

---

## 💭 My Takeaway
This problem is a great combination of two important SQL concepts — `LEFT JOIN` and `NULL` handling. The `LEFT JOIN` ensures employees without any bonus record still appear in the result. The `OR bonus IS NULL` part is critical because SQL's three-valued logic means `NULL < 1000` is `NULL`, not `TRUE`, so those rows would silently disappear without that extra condition. Always pair `LEFT JOIN` with explicit `NULL` checks in your `WHERE` clause.
