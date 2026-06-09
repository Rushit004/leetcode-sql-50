# 🟢 1527 · Patients With a Condition

**Difficulty:** Easy | **Topic:** String Matching / LIKE Pattern
**LeetCode:** [Problem Link](https://leetcode.com/problems/patients-with-a-condition/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Find the `patient_id`, `patient_name`, and `conditions` of patients who have **Type I Diabetes**.
Type I Diabetes always starts with the prefix `DIAB1`.
The `conditions` column contains 0 or more codes separated by spaces.
Return the result table in any order.

---

### Schema

```sql
CREATE TABLE Patients (
  patient_id   INT,
  patient_name VARCHAR(255),
  conditions   VARCHAR(255)
);
```

### Sample Input

| patient_id | patient_name | conditions   |
|------------|--------------|--------------|
| 1          | Daniel       | YFEV COUGH   |
| 2          | Alice        |              |
| 3          | Bob          | DIAB100 MYOP |
| 4          | George       | ACNE DIAB100 |
| 5          | Alain        | DIAB201      |

### Sample Output

| patient_id | patient_name | conditions   |
|------------|--------------|--------------|
| 3          | Bob          | DIAB100 MYOP |
| 4          | George       | ACNE DIAB100 |

---

### Solution

```sql
SELECT patient_id, patient_name, conditions
FROM Patients
WHERE conditions LIKE 'DIAB1%'
   OR conditions LIKE '% DIAB1%';
```

## 🧠 Approach

1. The `conditions` field is a space-separated list of condition codes — `DIAB1` can appear as the **first** code or **any subsequent** code.
2. Use `LIKE 'DIAB1%'` to catch cases where `DIAB1` is the very first (or only) code in the string — no leading space.
3. Use `LIKE '% DIAB1%'` to catch cases where `DIAB1` appears after at least one other code — preceded by a space.
4. Combine both patterns with `OR` to cover all valid positions in the string.

---

## 📌 Concepts Used

`LIKE` · `%` wildcard · `OR` · `Pattern matching` · `Space-delimited string search`

---

## 💭 My Takeaway

The subtle trap here is that `LIKE '%DIAB1%'` alone would incorrectly match codes like `XDIAB1` where `DIAB1` appears mid-word. By explicitly anchoring the pattern to either the start of the string or a space boundary (`'% DIAB1%'`), we ensure only valid word-boundary matches are returned. A neat introduction to positional pattern matching in SQL.