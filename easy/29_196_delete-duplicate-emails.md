# 🟢 196 · Delete Duplicate Emails

**Difficulty:** Easy | **Topic:** DELETE / Self Join     
**LeetCode:** [Problem Link](https://leetcode.com/problems/delete-duplicate-emails/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Delete all duplicate emails from the `Person` table, keeping only the row with the **smallest `id`** for each unique email.
Write a `DELETE` statement — not a `SELECT`.
The final order of the table does not matter.

---

### Schema

```sql
CREATE TABLE Person (
  id    INT,
  email VARCHAR(255)
);
```

### Sample Input

| id | email            |
|----|------------------|
| 1  | john@example.com |
| 2  | bob@example.com  |
| 3  | john@example.com |

### Sample Output

| id | email            |
|----|------------------|
| 1  | john@example.com |
| 2  | bob@example.com  |

---

### Solution

```sql
DELETE p1
FROM Person p1
JOIN Person p2
ON p1.email = p2.email
AND p1.id > p2.id;
```

## 🧠 Approach

1. Self-join the `Person` table as `p1` and `p2` on matching `email` values — this pairs every duplicate row with all other rows sharing the same email.
2. Add the condition `p1.id > p2.id` so that within each duplicate pair, only the row with the **larger** id is targeted — the row with the smaller id is always safe.
3. The `DELETE p1` targets only the `p1` alias, so only the higher-id duplicates are removed while the smallest-id row for each email survives.

---

## 📌 Concepts Used

`DELETE` · `Self Join` · `JOIN ON` · `Alias` · `Deduplication` · `Row comparison`

---

## 💭 My Takeaway

This is one of the rare SQL problems requiring `DELETE` instead of `SELECT`, which makes it memorable. The self-join trick is elegant — by joining the table to itself on equal email and strictly greater id, you automatically isolate every redundant duplicate in a single pass. No subquery needed.