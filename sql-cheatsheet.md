---
id: 16
date: 2025-06-27T00:00:00Z
title: SQL Cheatsheet
author: Jeremy Novak
summary: Cheatsheet for SQL commands and queries
slug: sql-cheatsheet
tags:
  - sql
  - database
  - mysql
  - postgresql
  - sqlite
published: true
---

# SQL Cheatsheet

---

## Database Connection

### MySQL
```bash
mysql -u username -p
mysql -u username -p -h hostname database_name
```

### PostgreSQL
```bash
psql -U username -d database_name
psql -U username -h hostname -d database_name
```

### SQLite
```bash
sqlite3 database.db
```

---

## Database Operations

- Show databases
```sql
-- MySQL
SHOW DATABASES;

-- PostgreSQL
\l

-- SQLite
.databases
```

- Create database
```sql
CREATE DATABASE database_name;
```

- Use database
```sql
-- MySQL
USE database_name;

-- PostgreSQL
\c database_name

-- SQLite
.open database_name.db
```

- Drop database
```sql
DROP DATABASE database_name;
```

---

## Table Operations

- Show tables
```sql
-- MySQL
SHOW TABLES;

-- PostgreSQL
\dt

-- SQLite
.tables
```

- Create table
```sql
CREATE TABLE table_name (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(255) UNIQUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

- Describe table structure
```sql
-- MySQL
DESCRIBE table_name;
SHOW COLUMNS FROM table_name;

-- PostgreSQL
\d table_name

-- SQLite
.schema table_name
```

- Drop table
```sql
DROP TABLE table_name;
```

- Alter table
```sql
-- Add column
ALTER TABLE table_name ADD COLUMN column_name datatype;

-- Drop column
ALTER TABLE table_name DROP COLUMN column_name;

-- Modify column
ALTER TABLE table_name MODIFY COLUMN column_name new_datatype;

-- Rename table
ALTER TABLE old_name RENAME TO new_name;
```

---

## Data Types

### Common Data Types
| Type | Description | Example |
|------|-------------|---------|
| `INT` | Integer | `123` |
| `VARCHAR(n)` | Variable-length string | `'Hello World'` |
| `TEXT` | Long text | `'Long text content'` |
| `DECIMAL(p,s)` | Fixed-point decimal | `123.45` |
| `DATE` | Date | `'2025-06-27'` |
| `DATETIME` | Date and time | `'2025-06-27 10:30:00'` |
| `BOOLEAN` | True/false | `TRUE`, `FALSE` |
| `BLOB` | Binary data | Binary content |

---

## CRUD Operations

### INSERT
```sql
-- Insert single record
INSERT INTO users (name, email) VALUES ('John Doe', 'john@example.com');

-- Insert multiple records
INSERT INTO users (name, email) VALUES 
    ('Jane Smith', 'jane@example.com'),
    ('Bob Wilson', 'bob@example.com');

-- Insert from another table
INSERT INTO users_backup SELECT * FROM users;
```

### SELECT
```sql
-- Basic select
SELECT * FROM users;
SELECT name, email FROM users;

-- With conditions
SELECT * FROM users WHERE age > 18;
SELECT * FROM users WHERE name LIKE 'John%';
SELECT * FROM users WHERE email IS NOT NULL;

-- With ordering
SELECT * FROM users ORDER BY name ASC;
SELECT * FROM users ORDER BY created_at DESC;

-- With limit
SELECT * FROM users LIMIT 10;
SELECT * FROM users LIMIT 10 OFFSET 20;

-- Distinct values
SELECT DISTINCT city FROM users;
```

### UPDATE
```sql
-- Update single record
UPDATE users SET email = 'newemail@example.com' WHERE id = 1;

-- Update multiple records
UPDATE users SET active = TRUE WHERE created_at > '2025-01-01';

-- Update with joins
UPDATE users u 
JOIN orders o ON u.id = o.user_id 
SET u.total_orders = u.total_orders + 1 
WHERE o.created_at > '2025-06-01';
```

### DELETE
```sql
-- Delete specific records
DELETE FROM users WHERE id = 1;
DELETE FROM users WHERE active = FALSE;

-- Delete all records (keep table structure)
DELETE FROM users;

-- Truncate table (faster, resets auto-increment)
TRUNCATE TABLE users;
```

---

## Joins

### INNER JOIN
```sql
SELECT u.name, o.order_date, o.amount
FROM users u
INNER JOIN orders o ON u.id = o.user_id;
```

### LEFT JOIN
```sql
SELECT u.name, o.order_date, o.amount
FROM users u
LEFT JOIN orders o ON u.id = o.user_id;
```

### RIGHT JOIN
```sql
SELECT u.name, o.order_date, o.amount
FROM users u
RIGHT JOIN orders o ON u.id = o.user_id;
```

### FULL OUTER JOIN
```sql
SELECT u.name, o.order_date, o.amount
FROM users u
FULL OUTER JOIN orders o ON u.id = o.user_id;
```

---

## Aggregate Functions

```sql
-- Count
SELECT COUNT(*) FROM users;
SELECT COUNT(DISTINCT city) FROM users;

-- Sum
SELECT SUM(amount) FROM orders;

-- Average
SELECT AVG(age) FROM users;

-- Min/Max
SELECT MIN(created_at), MAX(created_at) FROM users;

-- Group by
SELECT city, COUNT(*) as user_count 
FROM users 
GROUP BY city;

-- Having (filter groups)
SELECT city, COUNT(*) as user_count 
FROM users 
GROUP BY city 
HAVING COUNT(*) > 5;
```

---

## Subqueries

### WHERE Subquery
```sql
SELECT * FROM users 
WHERE id IN (SELECT user_id FROM orders WHERE amount > 1000);
```

### FROM Subquery
```sql
SELECT avg_age FROM (
    SELECT AVG(age) as avg_age FROM users GROUP BY city
) as city_averages;
```

### EXISTS
```sql
SELECT * FROM users u
WHERE EXISTS (SELECT 1 FROM orders o WHERE o.user_id = u.id);
```

---

## Indexes

- Create index
```sql
CREATE INDEX idx_email ON users(email);
CREATE INDEX idx_name_city ON users(name, city);
```

- Show indexes
```sql
-- MySQL
SHOW INDEX FROM table_name;

-- PostgreSQL
\di

-- SQLite
.indices table_name
```

- Drop index
```sql
DROP INDEX idx_email;
```

---

## Constraints

### Primary Key
```sql
ALTER TABLE users ADD PRIMARY KEY (id);
```

### Foreign Key
```sql
ALTER TABLE orders 
ADD CONSTRAINT fk_user_id 
FOREIGN KEY (user_id) REFERENCES users(id);
```

### Unique
```sql
ALTER TABLE users ADD CONSTRAINT uk_email UNIQUE (email);
```

### Check
```sql
ALTER TABLE users ADD CONSTRAINT chk_age CHECK (age >= 0);
```

### Not Null
```sql
ALTER TABLE users MODIFY COLUMN name VARCHAR(100) NOT NULL;
```

---

## Views

- Create view
```sql
CREATE VIEW active_users AS
SELECT id, name, email FROM users WHERE active = TRUE;
```

- Use view
```sql
SELECT * FROM active_users;
```

- Drop view
```sql
DROP VIEW active_users;
```

---

## Transactions

```sql
-- Start transaction
BEGIN;
-- or
START TRANSACTION;

-- Execute queries
INSERT INTO users (name, email) VALUES ('Test User', 'test@example.com');
UPDATE users SET active = TRUE WHERE id = LAST_INSERT_ID();

-- Commit changes
COMMIT;

-- Or rollback if something goes wrong
ROLLBACK;
```

---

## String Functions

```sql
-- Concatenation
SELECT CONCAT(first_name, ' ', last_name) as full_name FROM users;

-- Length
SELECT LENGTH(name) FROM users;

-- Substring
SELECT SUBSTRING(name, 1, 3) FROM users;

-- Upper/Lower case
SELECT UPPER(name), LOWER(email) FROM users;

-- Trim whitespace
SELECT TRIM(name) FROM users;

-- Replace
SELECT REPLACE(email, '@example.com', '@company.com') FROM users;
```

---

## Date Functions

```sql
-- Current date/time
SELECT NOW(), CURDATE(), CURTIME();

-- Date formatting
SELECT DATE_FORMAT(created_at, '%Y-%m-%d') FROM users;

-- Date arithmetic
SELECT DATE_ADD(created_at, INTERVAL 30 DAY) FROM users;
SELECT DATEDIFF(NOW(), created_at) as days_ago FROM users;

-- Extract parts
SELECT YEAR(created_at), MONTH(created_at), DAY(created_at) FROM users;
```

---

## Common Patterns

### Pagination
```sql
SELECT * FROM users 
ORDER BY id 
LIMIT 10 OFFSET 20;
```

### Find Duplicates
```sql
SELECT email, COUNT(*) 
FROM users 
GROUP BY email 
HAVING COUNT(*) > 1;
```

### Top N per Group
```sql
SELECT * FROM (
    SELECT *, ROW_NUMBER() OVER (PARTITION BY category ORDER BY price DESC) as rn
    FROM products
) ranked 
WHERE rn <= 3;
```

### Upsert (Insert or Update)
```sql
-- MySQL
INSERT INTO users (id, name, email) 
VALUES (1, 'John Doe', 'john@example.com')
ON DUPLICATE KEY UPDATE 
    name = VALUES(name), 
    email = VALUES(email);

-- PostgreSQL
INSERT INTO users (id, name, email) 
VALUES (1, 'John Doe', 'john@example.com')
ON CONFLICT (id) DO UPDATE SET 
    name = EXCLUDED.name, 
    email = EXCLUDED.email;
```

---

## Performance Tips

- Use indexes on frequently queried columns
- Avoid SELECT * in production queries
- Use LIMIT to restrict result sets
- Use appropriate data types
- Normalize your database design
- Use EXPLAIN to analyze query performance

```sql
-- Analyze query performance
EXPLAIN SELECT * FROM users WHERE email = 'john@example.com';
```

---

## Backup and Restore

### MySQL
```bash
# Backup
mysqldump -u username -p database_name > backup.sql

# Restore
mysql -u username -p database_name < backup.sql
```

### PostgreSQL
```bash
# Backup
pg_dump -U username database_name > backup.sql

# Restore
psql -U username database_name < backup.sql
```

### SQLite
```bash
# Backup
sqlite3 database.db ".backup backup.db"

# Restore
sqlite3 new_database.db ".restore backup.db"
```

---

## Resources

- [MySQL Documentation](https://dev.mysql.com/doc/)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- [SQLite Documentation](https://www.sqlite.org/docs.html)
- [SQL Tutorial - W3Schools](https://www.w3schools.com/sql/)
- [SQL Cheat Sheet - SQLBolt](https://sqlbolt.com/)