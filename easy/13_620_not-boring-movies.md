# 🟢 620 · Not Boring Movies

**Difficulty:** Easy | **Topic:** Filtering / WHERE  
**LeetCode:** [Problem Link](https://leetcode.com/problems/not-boring-movies/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Find all movies with an **odd-numbered ID** and a description that is **not** `'boring'`.

Return the result table ordered by `rating` in **descending order**.

---

### Schema

```sql
CREATE TABLE Cinema (
  id          INT PRIMARY KEY,
  movie       VARCHAR(255),
  description VARCHAR(255),
  rating      FLOAT
);
```

### Sample Input

| id | movie      | description | rating |
|----|------------|-------------|--------|
| 1  | War        | great 3D    | 8.9    |
| 2  | Science    | fiction     | 8.5    |
| 3  | irish      | boring      | 6.2    |
| 4  | Ice song   | Fantacy     | 8.6    |
| 5  | House card | Interesting | 9.1    |


### Sample Output

| id | movie      | description | rating |
|----|------------|-------------|--------|
| 5  | House card | Interesting | 9.1    |
| 1  | War        | great 3D    | 8.9    |

---

### Solution

```sql
SELECT *
FROM Cinema
WHERE id % 2 = 1 AND description NOT LIKE 'boring'
ORDER BY rating DESC
```

## 🧠 Approach

1. Use `id % 2 = 1` to filter only odd-numbered IDs using the modulo operator.
2. Use `description NOT LIKE 'boring'` to exclude rows where description is exactly `'boring'`.
3. `ORDER BY rating DESC` to return the highest rated movies first.

---

## 📌 Concepts Used

`WHERE` · `Modulo %` · `NOT LIKE` · `ORDER BY DESC` · `SELECT *`

---

## 💭 My Takeaway

Straightforward filtering problem but worth noting that `NOT LIKE 'boring'` without wildcards behaves the same as `!= 'boring'` — `LIKE` is only different when `%` or `_` wildcards are involved. Using `%` for odd-check is a clean and reusable trick that shows up often in SQL filtering problems.