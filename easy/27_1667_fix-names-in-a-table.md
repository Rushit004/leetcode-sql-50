# 🟢 1667 · Fix Names in a Table

**Difficulty:** Easy | **Topic:** String Functions / CONCAT / UPPER / LOWER  
**LeetCode:** [Problem Link](https://leetcode.com/problems/fix-names-in-a-table/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Fix the names in the `Users` table so that only the **first character is uppercase** and the **rest are lowercase**.
Return the result table ordered by `user_id`.

---

### Schema

```sql
CREATE TABLE Users (
  user_id INT,
  name    VARCHAR(255)
);
```

### Sample Input

| user_id | name  |
|---------|-------|
| 1       | aLice |
| 2       | bOB   |

### Sample Output

| user_id | name  |
|---------|-------|
| 1       | Alice |
| 2       | Bob   |

---

### Solution

```sql
SELECT user_id,
       CONCAT(UPPER(SUBSTRING(name, 1, 1)), LOWER(SUBSTRING(name, 2))) AS 'name'
FROM Users
ORDER BY user_id;
```

## 🧠 Approach

1. Use `SUBSTRING(name, 1, 1)` to extract just the first character of the name.
2. Wrap it with `UPPER()` to force it to uppercase.
3. Use `SUBSTRING(name, 2)` to extract everything from the second character onwards.
4. Wrap it with `LOWER()` to force the remainder to lowercase.
5. `CONCAT()` the two parts back together into the corrected name.
6. `ORDER BY user_id` to return results in ascending order as required.

---

## 📌 Concepts Used

`CONCAT()` · `UPPER()` · `LOWER()` · `SUBSTRING()` · `ORDER BY` · `String manipulation`

---

## 💭 My Takeaway

Clean and straightforward string problem. The trick is splitting the name at index 1 — `SUBSTRING(name, 1, 1)` for the head and `SUBSTRING(name, 2)` for the tail, then applying case functions independently before joining. A good reminder that MySQL string indexing starts at 1, not 0.