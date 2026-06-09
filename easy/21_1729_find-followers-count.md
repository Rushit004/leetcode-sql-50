# 🟢 1729 · Find Followers Count

**Difficulty:** Easy | **Topic:** Aggregation / COUNT DISTINCT  
**LeetCode:** [Problem Link](https://leetcode.com/problems/find-followers-count/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Find the **number of followers** for each user.

Return the result table ordered by `user_id` in **ascending order**.

---

## 🗂️ Schema
```sql
CREATE TABLE Followers (
  user_id     INT,
  follower_id INT,
  PRIMARY KEY (user_id, follower_id)
);
```

### Sample Input

| user_id | follower_id |
|---------|-------------|
| 0       | 1           |
| 1       | 0           |
| 2       | 0           |
| 2       | 1           |


### Sample Output

| user_id | followers_count |
|---------|-----------------|
| 0       | 1               |
| 1       | 1               |
| 2       | 2               |

---

## 💡 Solution
```sql
SELECT user_id, COUNT(DISTINCT follower_id) AS 'followers_count'
FROM Followers
GROUP BY user_id
ORDER BY user_id
```

## 🧠 Approach

1. `GROUP BY user_id` to aggregate all follower records belonging to the same user into one group.
2. `COUNT(DISTINCT follower_id)` counts only unique followers per user — since `(user_id, follower_id)` is already a composite primary key, duplicates are impossible here, but using `DISTINCT` is a safe and explicit habit.
3. `ORDER BY user_id` returns the result in ascending order of `user_id` as required.

---

## 📌 Concepts Used

`COUNT(DISTINCT)` · `GROUP BY` · `ORDER BY`

---

## 💭 My Takeaway

Almost identical in structure to problem 2356 — both use `COUNT(DISTINCT)` with `GROUP BY` on a single table. The composite primary key already guarantees no duplicate `(user_id, follower_id)` pairs, so `COUNT(follower_id)` would give the same result here. That said, keeping `DISTINCT` as a habit pays off in tables without such constraints where duplicates can silently inflate counts.