## 🟢 1683. Invalid Tweets

**Difficulty:** Easy | **Topic:** String Functions / WHERE  
**LeetCode:** [Problem Link](https://leetcode.com/problems/invalid-tweets/description/?envType=study-plan-v2&envId=top-sql-50)

---

## 📋 Problem Statement

Find the `tweet_id` of all **invalid tweets**.

A tweet is considered invalid if the number of characters in the `content` is **strictly greater than 15**.

Return the result table in **any order**.

---

## 🗂️ Schema

```sql
CREATE TABLE Tweets (
    tweet_id  INT PRIMARY KEY,
    content   VARCHAR(50)
);
```

---

## 📥 Sample Input

**Tweets**

| tweet_id | content                          |
|----------|----------------------------------|
| 1        | Vote for Biden                   |
| 2        | Let us make America great again! |

---

## 📤 Sample Output

| tweet_id |
|----------|
| 2        |

---

## 💡 Solution

```sql
SELECT tweet_id
FROM Tweets
WHERE LENGTH(content) > 15;
```

---

## 🔍 Approach

1. Select `tweet_id` from the `Tweets` table.
2. Use the `LENGTH()` function to count the number of characters in the `content` column.
3. Filter rows where the character count is **strictly greater than 15** using `WHERE LENGTH(content) > 15`.
4. All matching rows are invalid tweets and are returned.

---

## 🧠 Concepts Used

`WHERE clause` `LENGTH()` `String Functions` `Filtering` `Comparison Operators`

---

## ✍️ My Takeaway

This problem introduces the `LENGTH()` function in SQL, which is commonly used to measure string size. It's a simple but important tool when working with text data. One thing to note — in MySQL, `LENGTH()` returns the number of **bytes**, while `CHAR_LENGTH()` returns the number of **characters**. For standard ASCII text both give the same result, but for multi-byte characters (like emojis or Unicode), `CHAR_LENGTH()` is the safer choice.