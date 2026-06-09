## 🟢 1148. Article Views I

**Difficulty:** Easy | **Topic:** Filtering / WHERE  
**LeetCode:** [Problem Link](https://leetcode.com/problems/article-views-i/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Find all the authors that viewed **at least one** of their own articles.

Return the result table sorted by `id` in **ascending order**.

---

## 🗂️ Schema

```sql
CREATE TABLE Views (
    article_id  INT,
    author_id   INT,
    viewer_id   INT,
    view_date   DATE
);
```

---

## 📥 Sample Input

**Views**

| article_id | author_id | viewer_id | view_date  |
|------------|-----------|-----------|------------|
| 1          | 3         | 5         | 2019-08-01 |
| 1          | 3         | 6         | 2019-08-02 |
| 2          | 7         | 7         | 2019-08-01 |
| 2          | 7         | 6         | 2019-08-02 |
| 4          | 7         | 1         | 2019-07-22 |
| 3          | 4         | 4         | 2019-07-21 |
| 3          | 4         | 4         | 2019-07-21 |

---

## 📤 Sample Output

| id |
|----|
| 4  |
| 7  |

---

## 💡 Solution

```sql
SELECT DISTINCT author_id AS 'id'
FROM Views
WHERE author_id = viewer_id
ORDER BY id;
```

---

## 🔍 Approach

1. Select `author_id` from the `Views` table and alias it as `id`.
2. Apply a `WHERE` filter to only keep rows where `author_id = viewer_id` — meaning the author viewed their own article.
3. Use `DISTINCT` to eliminate duplicate author entries (same author may have viewed their own articles multiple times).
4. Sort the final result in ascending order using `ORDER BY id`.

---

## 🧠 Concepts Used

`WHERE clause` `DISTINCT` `Column Alias` `Self-reference Filter` `ORDER BY` `Filtering`

---

## ✍️ My Takeaway

This problem teaches a neat trick — comparing two columns of the same table to detect a self-referencing condition. The `DISTINCT` keyword is essential here because the same author could appear multiple times if they viewed their own articles on different dates. Without it, the result would have duplicates.
