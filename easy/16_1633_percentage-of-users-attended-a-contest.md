# 🟢 1633 · Percentage of Users Attended a Contest

**Difficulty:** Easy | **Topic:** Joins / Aggregation / Subquery  
**LeetCode:** [Problem Link](https://leetcode.com/problems/percentage-of-users-attended-a-contest/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Find the **percentage of users registered** in each contest, rounded to **2 decimal places**.

Return the result table ordered by `percentage` in **descending order**. In case of a tie, order by `contest_id` in **ascending order**.

---

### Schema

```sql
CREATE TABLE Users (
  user_id   INT PRIMARY KEY,
  user_name VARCHAR(20)
);

CREATE TABLE Register (
  contest_id INT,
  user_id    INT,
  PRIMARY KEY (contest_id, user_id)
);
```

### Sample Input

**Users** table:

| user_id | user_name |
|---------|-----------|
| 6       | Alice     |
| 2       | Bob       |
| 7       | Alex      |

**Register** table:

| contest_id | user_id |
|------------|---------|
| 215        | 6       |
| 209        | 2       |
| 208        | 6       |
| 210        | 6       |
| 208        | 2       |
| 209        | 7       |
| 209        | 6       |
| 215        | 7       |
| 208        | 7       |
| 210        | 2       |
| 207        | 2       |
| 210        | 7       |


### Sample Output

| contest_id | percentage |
|------------|------------|
| 208        | 100.0      |
| 209        | 100.0      |
| 210        | 100.0      |
| 215        | 66.67      |
| 207        | 33.33      |

---

### Solution

```sql
SELECT t1.contest_id, ROUND((COUNT(t1.user_id) / (SELECT COUNT(*) FROM Users)) * 100, 2) AS 'percentage'
FROM Register t1
JOIN Users t2
  ON t1.user_id = t2.user_id
GROUP BY t1.contest_id
ORDER BY percentage DESC, t1.contest_id
```

## 🧠 Approach

1. `JOIN` `Register` with `Users` on `user_id` to ensure only valid registered users are counted.
2. `GROUP BY contest_id` to aggregate registrations per contest.
3. Compute `percentage` as `COUNT(user_id) / total_users * 100`, where total users comes from a **scalar subquery** `(SELECT COUNT(*) FROM Users)` — it runs once and returns a fixed denominator for all groups.
4. `ROUND(..., 2)` formats the result to 2 decimal places.
5. `ORDER BY percentage DESC, contest_id ASC` satisfies the tie-breaking rule — higher percentage first, then lower `contest_id` on a tie.

---

## 📌 Concepts Used

`JOIN` · `COUNT()` · `ROUND()` · `GROUP BY` · `ORDER BY` · `Scalar Subquery` · `Percentage Calculation`

---

## 💭 My Takeaway

The scalar subquery `(SELECT COUNT(*) FROM Users)` is the neat trick here — it computes the total user count just once and reuses it as a constant denominator across every group, avoiding a separate CTE or variable. Also a good reminder that `ORDER BY` can chain multiple columns with different sort directions, which is essential whenever a tie-breaking rule is specified in the problem.