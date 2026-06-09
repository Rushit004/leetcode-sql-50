
# 🟢 1661 · Average Time of Process per Machine

**Difficulty:** Easy | **Topic:** Joins / Aggregation  
**LeetCode:** [Problem Link](https://leetcode.com/problems/average-time-of-process-per-machine/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

There is a factory website that has several machines each running the same number of processes. Find the **average time** each machine takes to complete a process.

The time to complete a process is the `end` timestamp minus the `start` timestamp. The average time is calculated by the total time to complete every process on the machine divided by the number of processes that were run.

Return the result table with `machine_id` and `processing_time` rounded to **3 decimal places**, in any order.

---

## 🗂️ Schema
```sql
CREATE TABLE Activity (
  machine_id    INT,
  process_id    INT,
  activity_type ENUM('start', 'end'),
  timestamp     FLOAT,
  PRIMARY KEY (machine_id, process_id, activity_type)
);
```

### Sample Input

| machine_id | process_id | activity_type | timestamp |
|------------|------------|---------------|-----------|
| 0          | 0          | start         | 0.712     |
| 0          | 0          | end           | 1.520     |
| 0          | 1          | start         | 3.140     |
| 0          | 1          | end           | 4.120     |
| 1          | 0          | start         | 0.550     |
| 1          | 0          | end           | 1.550     |
| 1          | 1          | start         | 0.430     |
| 1          | 1          | end           | 1.420     |
| 2          | 0          | start         | 4.100     |
| 2          | 0          | end           | 4.512     |
| 2          | 1          | start         | 2.500     |
| 2          | 1          | end           | 5.000     |


### Sample Output

| machine_id | processing_time |
|------------|-----------------|
| 0          | 0.894           |
| 1          | 0.995           |
| 2          | 1.456           |

---

## 💡 Solution
```sql
SELECT t1.machine_id, ROUND(AVG(t2.timestamp - t1.timestamp), 3) AS 'processing_time'
FROM Activity t1
JOIN Activity t2
  ON t1.machine_id = t2.machine_id
 AND t1.process_id = t2.process_id
WHERE t1.activity_type = 'start'
  AND t2.activity_type = 'end'
GROUP BY t1.machine_id
```

## 🧠 Approach

1. The same table holds both `start` and `end` events — a self-join is the cleanest way to pair them.
2. Join `Activity` to itself on **both** `machine_id` and `process_id` so each start row aligns with its exact end row.
3. Filter `t1` to `'start'` and `t2` to `'end'` in the `WHERE` clause to isolate the correct pairs.
4. Compute duration per process as `t2.timestamp - t1.timestamp` and pass it to `AVG()`.
5. `GROUP BY machine_id` to get one average per machine, then `ROUND(..., 3)` for the required precision.

---

## 📌 Concepts Used

`Self-Join` · `JOIN ON multiple columns` · `AVG()` · `ROUND()` · `GROUP BY` · `WHERE` · `ENUM filtering`

---

## 💭 My Takeaway

Classic self-join pattern — when one table stores two roles of the same event (start vs end), joining it to itself on a shared composite key is the go-to move. The trick is pairing on **both** `machine_id` and `process_id` together; joining on just one would produce wrong cross-process pairs. Good problem to internalize before tackling more complex event-log queries.
