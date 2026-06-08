# 🟢 2356 · Number of Unique Subjects Taught by Each Teacher

**Difficulty:** Easy | **Topic:** Aggregation / COUNT DISTINCT  
**LeetCode:** [Problem Link](https://leetcode.com/problems/number-of-unique-subjects-taught-by-each-teacher/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Find the number of **unique subjects** each teacher teaches in the university.

Return the result table in any order.

---

### Schema

```sql
CREATE TABLE Teacher (
  teacher_id INT,
  subject_id INT,
  dept_id    INT,
  PRIMARY KEY (subject_id, dept_id)
);
```

### Sample Input

| teacher_id | subject_id | dept_id |
|------------|------------|---------|
| 1          | 2          | 3       |
| 1          | 2          | 4       |
| 1          | 3          | 3       |
| 2          | 1          | 1       |
| 2          | 2          | 1       |
| 2          | 3          | 1       |
| 2          | 4          | 1       |


### Sample Output

| teacher_id | cnt |
|------------|-----|
| 1          | 2   |
| 2          | 4   |

---

### Solution

```sql
SELECT teacher_id, COUNT(DISTINCT subject_id) AS 'cnt'
FROM Teacher
GROUP BY teacher_id
```

## 🧠 Approach

1. `GROUP BY teacher_id` to process each teacher's records as a single group.
2. `COUNT(DISTINCT subject_id)` counts only unique subject IDs per teacher — the same subject taught in multiple departments is counted just once.
3. No `JOIN` or filtering needed since the single table holds all required information.

---

## 📌 Concepts Used

`COUNT(DISTINCT)` · `GROUP BY`

---

## 💭 My Takeaway

As minimal as SQL problems get, but it highlights a crucial distinction — `COUNT(subject_id)` vs `COUNT(DISTINCT subject_id)`. Here a teacher can teach the same subject across multiple departments, so without `DISTINCT` the count would be inflated. Whenever a problem says "unique" or "different", `DISTINCT` inside the aggregate is almost always the right instinct.