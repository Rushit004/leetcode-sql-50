# 🟡 550 · Game Play Analysis IV

**Difficulty:** Medium | **Topic:** Subquery / JOIN / DATE_ADD / Aggregation  
**LeetCode:** [Problem Link](https://leetcode.com/problems/game-play-analysis-iv/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Report the **fraction of players** that logged in again on the **day immediately after** their first login day, rounded to 2 decimal places.

Divide the number of players who logged in the day after their first login by the **total number of distinct players**.

---

## 🗂️ Schema
```sql
CREATE TABLE Activity (
  player_id    INT,
  device_id    INT,
  event_date   DATE,
  games_played INT
);
-- Primary key: (player_id, event_date)
```

### Sample Input

| player_id | device_id | event_date | games_played |
|-----------|-----------|------------|--------------|
| 1         | 2         | 2016-03-01 | 5            |
| 1         | 2         | 2016-03-02 | 6            |
| 2         | 3         | 2017-06-25 | 1            |
| 3         | 1         | 2016-03-02 | 0            |
| 3         | 4         | 2018-07-03 | 5            |

### Sample Output

| fraction |
|----------|
| 0.33     |

---

## 💡 Solution
```sql
SELECT
    ROUND(
        COUNT(DISTINCT a.player_id) /
        (SELECT COUNT(DISTINCT player_id) FROM Activity),
    2) AS fraction
FROM Activity a
JOIN (
    SELECT player_id, MIN(event_date) AS first_login
    FROM Activity
    GROUP BY player_id
) b
ON a.player_id = b.player_id
AND a.event_date = DATE_ADD(b.first_login, INTERVAL 1 DAY);
```

## 🧠 Approach

1. Build a subquery `b` that finds the **first login date** per player using `MIN(event_date)` grouped by `player_id`.
2. `JOIN` the original `Activity` table `a` with subquery `b` on two conditions: matching `player_id` **and** `event_date = DATE_ADD(first_login, INTERVAL 1 DAY)` — this only keeps rows where a player logged in exactly the day after their first login.
3. `COUNT(DISTINCT a.player_id)` counts how many players satisfied the day-after condition.
4. Divide by the total distinct player count from a scalar subquery on the full table.
5. Wrap in `ROUND(..., 2)` to get the result to 2 decimal places.

---

## 📌 Concepts Used

`MIN()` · `GROUP BY` · `JOIN` · `DATE_ADD()` · `INTERVAL 1 DAY` · `COUNT(DISTINCT)` · `Scalar subquery` · `ROUND()`

---

## 💭 My Takeaway

The key insight is using `DATE_ADD(first_login, INTERVAL 1 DAY)` as a JOIN condition instead of a WHERE filter — this elegantly matches only the exact next-day row for each player. The scalar subquery in the denominator ensures the total player count is always the full dataset, regardless of how many matched. A strong exercise in multi-condition joins and date arithmetic.