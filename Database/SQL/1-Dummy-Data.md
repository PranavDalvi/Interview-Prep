### 1️⃣ Create Database (optional)
`CREATE DATABASE interview_sql;`
Connect to it:
`\c interview_sql`

---
### 2️⃣ Create `users` table
`CREATE TABLE users (   id SERIAL PRIMARY KEY,   name TEXT NOT NULL,   email TEXT UNIQUE,   age INT,   city TEXT,   created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP );`

---
### 3️⃣ Insert data into `users`
`INSERT INTO users (name, email, age, city) VALUES ('Alice', 'alice@gmail.com', 28, 'Bangalore'), ('Bob', 'bob@gmail.com', 35, 'Delhi'), ('Charlie', 'charlie@gmail.com', 22, 'Mumbai'), ('David', 'david@gmail.com', 35, 'Bangalore'), ('Eva', 'eva@gmail.com', NULL, 'Delhi'), ('Frank', 'frank@gmail.com', 40, 'Mumbai'), ('Grace', 'grace@gmail.com', 29, 'Bangalore'), ('Helen', NULL, 31, 'Chennai');`

---
### 4️⃣ Create `orders` table (for later JOIN days)
`CREATE TABLE orders (   id SERIAL PRIMARY KEY,   user_id INT REFERENCES users(id),   amount NUMERIC(10,2),   status TEXT,   created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP );`

---
### 5️⃣ Insert data into `orders`
`INSERT INTO orders (user_id, amount, status) VALUES (1, 250.50, 'completed'), (1, 120.00, 'completed'), (2, 300.00, 'pending'), (3, 150.00, 'completed'), (5, 500.00, 'cancelled'), (7, 700.00, 'completed');`