# 🟡 1204. Last Person to Fit in the Bus

**Difficulty:** Medium | **Topic:** Database / Window Functions    
**LeetCode:** [Problem Link](https://leetcode.com/problems/last-person-to-fit-in-the-bus/)

---

## 📋 Problem Statement

Given a table `Queue`, a bus has a weight limit of `1000` kg. People board the bus in the order of their `turn`. Find the `person_name` of the **last person** who can board without exceeding the weight limit.

The test cases guarantee that the first person in the queue does not exceed the weight limit.

---

## 🗂️ Schema
```sql
CREATE TABLE Queue (
    person_id   INT,
    person_name VARCHAR(30),
    weight      INT,
    turn        INT
);
```

---

## 📥 Sample Input

**Queue**

| person_id | person_name | weight | turn |
|-----------|-------------|--------|------|
| 5         | Alice       | 250    | 1    |
| 4         | Bob         | 175    | 5    |
| 3         | Alex        | 350    | 2    |
| 6         | John Cena   | 400    | 3    |
| 1         | Winston     | 500    | 6    |
| 2         | Marie       | 200    | 4    |

---

## 📤 Sample Output

| person_name |
|-------------|
| John Cena   |

---

## 💡 Solution

```sql
SELECT person_name FROM
(SELECT *,
SUM(weight) OVER(ORDER BY turn 
                ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS 'cum_weight'
FROM Queue
) t
WHERE t.cum_weight <= 1000 
ORDER BY turn DESC LIMIT 1;
```

---

## 🧠 Approach
1. Use `SUM(weight) OVER(ORDER BY turn ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)` to compute a **running cumulative weight** for each person in boarding order.
2. Wrap the window function in a subquery to make `cum_weight` available for filtering.
3. Filter rows where `cum_weight <= 1000` — keeping only people who can board within the weight limit.
4. Order the remaining rows by `turn DESC` and use `LIMIT 1` to get the **last valid person** in the boarding sequence.

---

## 📌 Concepts Used
`Window Functions` `SUM() OVER()` `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` `Subquery` `ORDER BY` `LIMIT`

---

## 💭 My Takeaway
This problem is a perfect use case for a running total window function. Instead of self-joining or using correlated subqueries, `SUM() OVER()` elegantly computes cumulative weight in boarding order in a single pass. The key trick is filtering after the window function via a subquery, then picking the last valid row with `ORDER BY turn DESC LIMIT 1`.