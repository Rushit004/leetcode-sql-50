# 🟢 1141 · User Activity for the Past 30 Days I

**Difficulty:** Easy | **Topic:** Filtering / DATE / Aggregation  
**LeetCode:** [Problem Link](https://leetcode.com/problems/user-activity-for-the-past-30-days-i/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Find the **daily active user count** for a period of **30 days** ending on `2019-07-27` inclusively.

A user was active on a given day if they performed **at least one activity** on that day.

Return the result table in any order.

---

### Schema

```sql
CREATE TABLE Activity (
  user_id       INT,
  session_id    INT,
  activity_date DATE,
  activity_type ENUM('open_session', 'end_session', 'scroll_down', 'send_message')
);
```

### Sample Input

| user_id | session_id | activity_date | activity_type |
|---------|------------|---------------|---------------|
| 1       | 1          | 2019-07-20    | open_session  |
| 1       | 1          | 2019-07-20    | scroll_down   |
| 1       | 1          | 2019-07-20    | end_session   |
| 2       | 4          | 2019-07-20    | open_session  |
| 2       | 4          | 2019-07-21    | send_message  |
| 2       | 4          | 2019-07-21    | end_session   |
| 3       | 2          | 2019-07-21    | open_session  |
| 3       | 2          | 2019-07-21    | end_session   |
| 4       | 3          | 2019-06-25    | open_session  |
| 4       | 3          | 2019-06-25    | end_session   |


### Sample Output

| day        | active_users |
|------------|--------------|
| 2019-07-20 | 2            |
| 2019-07-21 | 2            |

---

### Solution

```sql
SELECT activity_date AS 'day', COUNT(DISTINCT user_id) AS 'active_users'
FROM Activity
WHERE activity_date BETWEEN '2019-06-28' AND '2019-07-27'
AND activity_type IN ('open_session', 'end_session', 'scroll_down', 'send_message')
GROUP BY activity_date
```

## 🧠 Approach

1. `WHERE activity_date BETWEEN '2019-06-28' AND '2019-07-27'` restricts rows to the exact 30-day window ending on the reference date — both bounds are inclusive with `BETWEEN`.
2. The `IN` clause covers all possible `activity_type` values as an explicit safety filter, ensuring only valid activity rows are considered.
3. `GROUP BY activity_date` collapses all activity rows into one row per day.
4. `COUNT(DISTINCT user_id)` counts each user only once per day regardless of how many activities they performed, which correctly reflects "active on that day."
5. Aliasing `activity_date` as `day` matches the expected output column name.

---

## 📌 Concepts Used

`BETWEEN` · `IN` · `COUNT(DISTINCT)` · `GROUP BY` · `WHERE` · `Date Filtering` · `Aliasing`

---

## 💭 My Takeaway

The key detail here is using `COUNT(DISTINCT user_id)` instead of plain `COUNT(*)` — a single user can perform multiple activities in one day, so without `DISTINCT` the count would reflect activity records, not active users. Also worth noting that the `IN` clause covering all ENUM values is technically redundant here since no other values exist, but it's a safe and readable habit when working with ENUM columns. The 30-day window translates to `2019-07-27 - 29 days = 2019-06-28` — always double-check inclusive vs exclusive bounds when hardcoding date ranges.