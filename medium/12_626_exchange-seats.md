# 🟡 626 · Exchange Seats

**Difficulty:** Medium | **Topic:** CASE / Conditional Logic    
**LeetCode:** [Problem Link](https://leetcode.com/problems/exchange-seats/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Swap the seat id of every two consecutive students. If the number of students is odd, the id of the last student is not swapped.  
Return the result table ordered by `id` in ascending order.

---

### Schema

```sql
CREATE TABLE Seat (
  id INT,
  student VARCHAR(255)
);
```

### Sample Input

| id | student |
|----|---------|
| 1  | Abbot   |
| 2  | Doris   |
| 3  | Emerson |
| 4  | Green   |
| 5  | Jeames  |

### Sample Output

| id | student |
|----|---------|
| 1  | Doris   |
| 2  | Abbot   |
| 3  | Green   |
| 4  | Emerson |
| 5  | Jeames  |

---

### Solution

```sql
SELECT 
    CASE
        WHEN id % 2 = 1 AND id + 1 <= (SELECT MAX(id) FROM Seat)
            THEN id + 1         
        WHEN id % 2 = 0
            THEN id - 1         
        ELSE id                 
    END AS id,
    student
FROM Seat
ORDER BY id;
```

## 🧠 Approach

1. For every **odd** `id`, swap it with the next one (`id + 1`) — but only if that next seat actually exists (checked via `MAX(id)`).
2. For every **even** `id`, swap it with the previous one (`id - 1`) — this always exists since even ids start at 2.
3. If the last student has an odd `id` (total count is odd), the `ELSE id` clause keeps them in place.
4. `ORDER BY id` on the new computed id gives the final sorted result.

---

## 📌 Concepts Used

`CASE WHEN` · `Modulo (%)` · `Subquery` · `MAX()` · `ORDER BY`

---

## 💭 My Takeaway

The key insight is handling the edge case — an odd last row. Using `MAX(id)` inside the CASE condition is a neat trick to detect whether a next seat exists without a JOIN.