# 🟡 602. Friend Requests II: Who Has the Most Friends

**Difficulty:** Medium | **Topic:** UNION ALL / GROUP BY    
**LeetCode:** [View Problem](https://leetcode.com/problems/friend-requests-ii-who-has-the-most-friends/)

---

## 📋 Problem Statement

The `RequestAccepted` table holds the friend request data for all accepted requests.

Write a solution to find the person who has the most friends and the total number of friends they have.

The test cases are generated such that only one person has the most friends.

---

## 🗃️ Schema

```sql
CREATE TABLE RequestAccepted (
    requester_id INT NOT NULL,
    accepter_id  INT NOT NULL,
    accept_date  DATE,
    PRIMARY KEY (requester_id, accepter_id)
);
```

---

## 📥 Sample Input

**RequestAccepted** table:

| requester_id | accepter_id | accept_date |
|:---:|:---:|:---:|
| 1 | 2 | 2016/06/03 |
| 1 | 3 | 2016/06/08 |
| 2 | 3 | 2016/06/08 |
| 3 | 4 | 2016/06/09 |

---

## 📤 Sample Output

| id | num |
|:---:|:---:|
| 3 | 3 |

---

## ✅ Solution

```sql
SELECT id, COUNT(*) AS num
FROM (
    SELECT requester_id AS id FROM RequestAccepted
    UNION ALL
    SELECT accepter_id FROM RequestAccepted
) t
GROUP BY id
ORDER BY num DESC
LIMIT 1;
```

---

## 🧠 Approach

1. A friendship is **bidirectional** — both the requester and accepter gain a friend when a request is accepted.
2. Use `UNION ALL` to combine all `requester_id` and `accepter_id` values into a single `id` column, keeping duplicates so every friendship is counted.
3. `GROUP BY id` and `COUNT(*)` gives the total number of friends for each person.
4. `ORDER BY num DESC` sorts from most to fewest friends.
5. `LIMIT 1` returns only the person with the highest count.

---

## 🏷️ Concepts Used

`UNION ALL` `Subquery` `GROUP BY` `COUNT` `ORDER BY` `LIMIT`

---

## 💡 My Takeaway

The key insight here is treating a friendship as two separate appearances — once as the requester, once as the accepter. Using `UNION ALL` instead of `UNION` is critical because we need to preserve duplicates; dropping them with `UNION` would give wrong counts. Stacking both columns into one and then grouping is a clean pattern I'll reuse whenever a relationship is symmetric.