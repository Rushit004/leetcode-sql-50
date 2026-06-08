# 🟡 1341 · Movie Rating

**Difficulty:** Medium | **Topic:** UNION ALL / GROUP BY / Aggregation  
**LeetCode:** [Problem Link](https://leetcode.com/problems/movie-rating/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Find the name of the user who has rated the greatest number of movies (lexicographically smaller name on tie), and find the movie with the highest average rating in February 2020 (lexicographically smaller title on tie).  
Return both results in a single column.

---

### Schema

```sql
CREATE TABLE Movies (
  movie_id INT,
  title VARCHAR(30)
);

CREATE TABLE Users (
  user_id INT,
  name VARCHAR(30)
);

CREATE TABLE MovieRating (
  movie_id INT,
  user_id INT,
  rating INT,
  created_at DATE
);
```

### Sample Input

**Movies**

| movie_id | title    |
|----------|----------|
| 1        | Avengers |
| 2        | Frozen 2 |
| 3        | Joker    |

**Users**

| user_id | name   |
|---------|--------|
| 1       | Daniel |
| 2       | Monica |
| 3       | Maria  |
| 4       | James  |

**MovieRating**

| movie_id | user_id | rating | created_at |
|----------|---------|--------|------------|
| 1        | 1       | 3      | 2020-01-12 |
| 1        | 2       | 4      | 2020-02-11 |
| 1        | 3       | 2      | 2020-02-12 |
| 1        | 4       | 1      | 2020-01-01 |
| 2        | 1       | 5      | 2020-02-17 |
| 2        | 2       | 2      | 2020-02-01 |
| 2        | 3       | 2      | 2020-03-01 |
| 3        | 1       | 3      | 2020-02-22 |
| 3        | 2       | 4      | 2020-02-25 |

### Sample Output

| results  |
|----------|
| Daniel   |
| Frozen 2 |

---

### Solution

```sql
-- Part 1: User with most ratings
(SELECT u.name AS results
 FROM MovieRating m
 JOIN Users u ON m.user_id = u.user_id
 GROUP BY m.user_id
 ORDER BY COUNT(*) DESC, u.name ASC
 LIMIT 1)

UNION ALL

-- Part 2: Movie with highest avg rating in Feb 2020
(SELECT mo.title AS results
 FROM MovieRating m
 JOIN Movies mo ON m.movie_id = mo.movie_id
 WHERE m.created_at BETWEEN '2020-02-01' AND '2020-02-29'
 GROUP BY m.movie_id
 ORDER BY AVG(m.rating) DESC, mo.title ASC
 LIMIT 1)
```

## 🧠 Approach

1. This problem has **two independent subqueries** combined with `UNION ALL` — each returns exactly one row.
2. **Part 1:** JOIN `MovieRating` with `Users`, group by `user_id`, count ratings per user, sort by count descending then name ascending, `LIMIT 1`.
3. **Part 2:** JOIN `MovieRating` with `Movies`, filter to Feb 2020 using `BETWEEN`, group by `movie_id`, sort by `AVG(rating)` descending then title ascending, `LIMIT 1`.
4. `UNION ALL` (not `UNION`) is used intentionally — no deduplication needed and it's faster.
5. Tie-breaking with `name ASC` / `title ASC` ensures lexicographically smaller value wins.

---

## 📌 Concepts Used

`UNION ALL` · `JOIN` · `GROUP BY` · `AVG()` · `COUNT()` · `ORDER BY` · `LIMIT` · `BETWEEN`

---

## 💭 My Takeaway

Using `UNION ALL` to stitch two completely different queries into one result set felt elegant. The tricky part was remembering the tie-breaker — always sort by name/title ascending as a secondary condition, or you'll fail edge cases.