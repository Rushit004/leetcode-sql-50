
# 🟢 1280 · Students and Examinations

**Difficulty:** Easy | **Topic:** CROSS JOIN / LEFT JOIN / Aggregation  
**LeetCode:** [Problem Link](https://leetcode.com/problems/students-and-examinations/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Find the number of times each student attended each exam.

Return the result table ordered by `student_id` and `subject_name`. Every student must appear for **every subject** — even if they attended **zero** exams for it.

---

## 🗂️ Schema
```sql
CREATE TABLE Students (
  student_id   INT PRIMARY KEY,
  student_name VARCHAR(20)
);

CREATE TABLE Subjects (
  subject_name VARCHAR(20) PRIMARY KEY
);

CREATE TABLE Examinations (
  student_id   INT,
  subject_name VARCHAR(20)
);
```

### Sample Input

**Students** table:

| student_id | student_name |
|------------|--------------|
| 1          | Alice        |
| 2          | Bob          |
| 6          | Alex         |
| 13         | John         |

**Subjects** table:

| subject_name |
|--------------|
| Math         |
| Physics      |
| Programming  |

**Examinations** table:

| student_id | subject_name |
|------------|--------------|
| 1          | Math         |
| 1          | Physics      |
| 1          | Programming  |
| 2          | Math         |
| 1          | Math         |
| 13         | Math         |
| 13         | Programming  |
| 13         | Physics      |
| 2          | Math         |
| 1          | Math         |


### Sample Output

| student_id | student_name | subject_name | attended_exams |
|------------|--------------|--------------|----------------|
| 1          | Alice        | Math         | 3              |
| 1          | Alice        | Physics      | 1              |
| 1          | Alice        | Programming  | 1              |
| 2          | Bob          | Math         | 2              |
| 2          | Bob          | Physics      | 0              |
| 2          | Bob          | Programming  | 0              |
| 6          | Alex         | Math         | 0              |
| 6          | Alex         | Physics      | 0              |
| 6          | Alex         | Programming  | 0              |
| 13         | John         | Math         | 1              |
| 13         | John         | Physics      | 1              |
| 13         | John         | Programming  | 1              |

---

## 💡 Solution
```sql
SELECT t1.student_id, t1.student_name, t2.subject_name, COUNT(t3.subject_name) AS 'attended_exams'
FROM Students t1
CROSS JOIN Subjects t2
LEFT JOIN Examinations t3
  ON t1.student_id = t3.student_id
 AND t2.subject_name = t3.subject_name
GROUP BY t1.student_id, t1.student_name, t2.subject_name
ORDER BY t1.student_id, t2.subject_name
```

## 🧠 Approach

1. `CROSS JOIN` `Students` with `Subjects` to generate every possible student–subject combination, including those with zero attendance.
2. `LEFT JOIN` `Examinations` on **both** `student_id` and `subject_name` to attach actual exam records — unmatched combinations stay in the result as `NULL`.
3. `COUNT(t3.subject_name)` counts only non-NULL matches, so students who never attended a subject naturally get `0`.
4. `GROUP BY` all three non-aggregated columns to collapse multiple exam rows into one count per student–subject pair.
5. `ORDER BY student_id, subject_name` to satisfy the required output order.

---

## 📌 Concepts Used

`CROSS JOIN` · `LEFT JOIN` · `JOIN ON multiple columns` · `COUNT()` · `GROUP BY` · `ORDER BY` · `NULL handling`

---

## 💭 My Takeaway

The key insight here is using `CROSS JOIN` to build the full grid of all student–subject pairs *before* joining exam data — not the other way around. Trying to start from `Examinations` would silently drop students or subjects with zero records. Also a good reminder that `COUNT(column)` ignores NULLs, which is exactly what makes the zero-attendance case work without any `COALESCE` or `IFNULL`.
