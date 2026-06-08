
# 🟡 180. Consecutive Numbers

**Difficulty:** Medium | **Topic:** Database / Self-Join  
**LeetCode:** [Problem Link](https://leetcode.com/problems/consecutive-numbers/)

---

## 📋 Problem Statement

Given a table `Logs`, find all numbers that appear **at least three times consecutively**.

Return the result in **any order**.

---

## 🗃️ Schema

```sql
CREATE TABLE Logs (
    id  INT PRIMARY KEY AUTO_INCREMENT,
    num VARCHAR(255)
);
```

---

## 📥 Sample Input

**Logs**

| id | num |
|----|-----|
| 1  | 1   |
| 2  | 1   |
| 3  | 1   |
| 4  | 2   |
| 5  | 1   |
| 6  | 2   |
| 7  | 2   |

---

## 📤 Sample Output

| ConsecutiveNums |
|-----------------|
| 1               |

---

## 💡 Solution

```sql
SELECT DISTINCT l1.num AS ConsecutiveNums
FROM Logs l1
JOIN Logs l2 ON l2.id = l1.id + 1
JOIN Logs l3 ON l3.id = l1.id + 2
WHERE l1.num = l2.num
  AND l2.num = l3.num;
```

---

## 🪜 Approach

1. Self-join `Logs` three times — `l1`, `l2`, and `l3` — representing three consecutive rows.
2. Link them using `id` increments: `l2.id = l1.id + 1` and `l3.id = l1.id + 2`.
3. Filter rows where all three `num` values are equal using the `WHERE` clause.
4. Use `DISTINCT` to remove duplicate entries in case the same number appears consecutively more than three times.

---

## 🧠 Concepts Used

`Self-Join` `DISTINCT` `Consecutive Row Detection` `Primary Key Arithmetic` `Multi-Table JOIN`

---

## ✍️ My Takeaway

This problem taught me a clean trick — using `id + 1` and `id + 2` offsets in self-joins to simulate a sliding window over consecutive rows. The key insight is that if `id` is auto-incremented and gapless, arithmetic on it reliably maps to physical row adjacency. `DISTINCT` is essential here since a run longer than three would otherwise produce duplicate results.
