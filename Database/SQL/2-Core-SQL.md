# Core SQL (PostgreSQL)

This document contains the **practice questions**, their **correct SQL answers**, and the **expected output** based on the dummy data.

---
## Question 1
**Get all users from Bangalore aged above 25**
### Query
```sql
SELECT id, name, age, city
FROM users
WHERE city = 'Bangalore'
  AND age > 25;
```
### Output

| id  | name  | age | city      |
| --- | ----- | --- | --------- |
| 1   | Alice | 28  | Bangalore |
| 4   | David | 35  | Bangalore |
| 7   | Grace | 29  | Bangalore |

---
## Question 2
**Get users whose age is between 25 and 35 (inclusive)**
### Query
```sql
SELECT id, name, age
FROM users
WHERE age BETWEEN 25 AND 35;
```
### Output

| id  | name  | age |
| --- | ----- | --- |
| 1   | Alice | 28  |
| 2   | Bob   | 35  |
| 4   | David | 35  |
| 7   | Grace | 29  |
| 8   | Helen | 31  |

---
## Question 3
**Get users whose name starts with 'A'**
### Query
```sql
SELECT id, name
FROM users
WHERE name LIKE 'A%';
```
### Output

| id  | name  |
| --- | ----- |
| 1   | Alice |

---
## Question 4
**Sort users by age in descending order (NULLs last)**
### Query
```sql
SELECT id, name, age
FROM users
ORDER BY age DESC NULLS LAST;
```
### Output

| id  | name    | age  |
| --- | ------- | ---- |
| 6   | Frank   | 40   |
| 2   | Bob     | 35   |
| 4   | David   | 35   |
| 8   | Helen   | 31   |
| 7   | Grace   | 29   |
| 1   | Alice   | 28   |
| 3   | Charlie | 22   |
| 5   | Eva     | NULL |

---
## Question 5
**Fetch the top 3 oldest users**
### Query

```sql
SELECT id, name, age
FROM users
WHERE age IS NOT NULL
ORDER BY age DESC
LIMIT 3;
```
### Output

|id|name|age|
|---|---|---|
|6|Frank|40|
|2|Bob|35|
|4|David|35|

---
## Question 6
**Fetch users where email is NULL**
### Query
```sql
SELECT id, name, email
FROM users
WHERE email IS NULL;
```
### Output

| id  | name  | email |
| --- | ----- | ----- |
| 8   | Helen | NULL  |

---
## Question 7
**Case-insensitive search for users from 'delhi'**
### Query (PostgreSQL-specific)

```sql
SELECT id, name, city
FROM users
WHERE city ILIKE 'delhi';
```
### Output

| id  | name | city  |
| --- | ---- | ----- |
| 2   | Bob  | Delhi |
| 5   | Eva  | Delhi |
***
