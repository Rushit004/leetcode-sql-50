# 🟢 596 · Classes More Than 5 Students

**Difficulty:** Easy | **Topic:** Aggregation / HAVING  
**LeetCode:** [Problem Link](https://leetcode.com/problems/classes-more-than-5-students/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Find all classes that have **at least 5 students**.

Return the result table in any order.

---

## 🗂️ Schema
```sql
CREATE TABLE Courses (
  student VARCHAR(255),
  class   VARCHAR(255),
  PRIMARY KEY (student, class)
);
```

### Sample Input

| student | class    |
|---------|----------|
| A       | Math     |
| B       | English  |
| C       | Math     |
| D       | Biology  |
| E       | Math     |
| F       | Computer |
| G       | Math     |
| H       | Math     |
| I       | Math     |


### Sample Output

| class |
|-------|
| Math  |

---

## 💡 Solution
```sql
SELECT class
FROM Courses
GROUP BY class
HAVING COUNT(student) > 4
```

## 🧠 Approach

1. `GROUP BY class` collapses all rows into one group per class.
2. `HAVING COUNT(student) > 4` filters out any class with fewer than 5 students — `HAVING` is used here instead of `WHERE` because the filter applies to an aggregated value, not an individual row.
3. Since the table has a `PRIMARY KEY (student, class)`, duplicate student–class pairs are impossible, so `COUNT(student)` is inherently distinct.

---

## 📌 Concepts Used

`GROUP BY` · `HAVING` · `COUNT()` · `Aggregation Filtering`

---

## 💭 My Takeaway

Short problem but it nails the `WHERE` vs `HAVING` distinction — `WHERE` filters rows before grouping, `HAVING` filters groups after aggregation. Trying to write `WHERE COUNT(student) > 4` would throw an error. Also worth noting that `COUNT(student) > 4` means 5 or more, so no `>= 5` is needed — just make sure the inequality is right when the problem says "at least".