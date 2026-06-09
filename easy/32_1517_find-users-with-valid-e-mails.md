# 🟢 1517 · Find Users With Valid E-Mails

**Difficulty:** Easy | **Topic:** Regex / REGEXP / Pattern Validation
**LeetCode:** [Problem Link](https://leetcode.com/problems/find-users-with-valid-e-mails/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Find all users with **valid emails**. A valid email must satisfy:
- The **prefix** may contain letters (upper or lower case), digits, `_`, `.`, and/or `-`.
- The **prefix must start with a letter**.
- The **domain** must be exactly `@leetcode.com` (case-sensitive).

Return the result table in any order.

---

### Schema

```sql
CREATE TABLE Users (
  user_id INT,
  name    VARCHAR(255),
  mail    VARCHAR(255)
);
```

### Sample Input

| user_id | name      | mail                    |
|---------|-----------|-------------------------|
| 1       | Winston   | winston@leetcode.com    |
| 2       | Jonathan  | jonathanisgreat         |
| 3       | Annabelle | bella-@leetcode.com     |
| 4       | Sally     | sally.come@leetcode.com |
| 5       | Marwan    | quarz#2020@leetcode.com |
| 6       | David     | david69@gmail.com       |
| 7       | Shapiro   | .shapo@leetcode.com     |

### Sample Output

| user_id | name      | mail                    |
|---------|-----------|-------------------------|
| 1       | Winston   | winston@leetcode.com    |
| 3       | Annabelle | bella-@leetcode.com     |
| 4       | Sally     | sally.come@leetcode.com |

---

### Solution

```sql
SELECT *
FROM Users
WHERE
    mail REGEXP '^[a-zA-Z][a-zA-Z0-9_.-]*@leetcode\\.com$'
    AND mail LIKE BINARY '%@leetcode.com';
```

## 🧠 Approach

1. Use `REGEXP '^[a-zA-Z][a-zA-Z0-9_.-]*@leetcode\\.com$'` to validate the full structure:
   - `^[a-zA-Z]` — prefix must begin with a letter.
   - `[a-zA-Z0-9_.-]*` — the rest of the prefix allows letters, digits, `_`, `.`, `-`.
   - `@leetcode\\.com$` — domain must end with exactly `@leetcode.com` (the `\\.` escapes the literal dot).
2. Add `LIKE BINARY '%@leetcode.com'` as a **case-sensitive guard** — MySQL's `REGEXP` is case-insensitive by default, so without this, `@LeetCode.COM` would incorrectly pass. `LIKE BINARY` enforces lowercase domain matching.

---

## 📌 Concepts Used

`REGEXP` · `^` anchor · `$` anchor · `[a-zA-Z0-9_.-]` character class · `\\.` dot escape · `LIKE BINARY` · `Case-sensitive matching`

---

## 💭 My Takeaway

The tricky part of this problem is MySQL's case-insensitive `REGEXP` — the regex alone won't reject `@LeetCode.COM`. Pairing it with `LIKE BINARY` is an elegant workaround to enforce domain case sensitivity without switching the full query to a binary collation. A great problem for understanding regex anchoring and MySQL's collation behaviour.