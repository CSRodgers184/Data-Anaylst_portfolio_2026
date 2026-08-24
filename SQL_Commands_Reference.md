# SQL Commands Reference

Quick-reference guide for common SQL statements. Use this while working on Glorystone analysis and portfolio projects.

---

## SELECT

`SELECT` is the most commonly used SQL statement. It defines what data your query returns.

```sql
SELECT name
FROM customers;
```

### SELECT *

Returns all columns from the table.

```sql
SELECT * FROM customers;
```

### SELECT DISTINCT

Returns only unique values (removes duplicates).

```sql
SELECT DISTINCT name
FROM customers;
```

### SELECT INTO

Copies data from one table into a new table.

```sql
SELECT * INTO customers_backup
FROM customers;
```

### SELECT TOP

Returns the top *n* rows or percent (SQL Server syntax).

```sql
SELECT TOP 50 * FROM customers;

SELECT TOP 50 PERCENT * FROM customers;
```

---

## AS (Alias)

Renames a column or table with an alias.

```sql
SELECT name AS first_name
FROM customers;
```

---

## FROM

Specifies the table the data is pulled from.

```sql
SELECT name
FROM customers;
```

---

## WHERE

Filters rows that meet a condition. Works with operators: `=`, `>`, `<`, `>=`, `<=`, `<>`.

```sql
SELECT name
FROM customers
WHERE name = 'Bob';
```

### AND

Requires **all** conditions to be true.

```sql
SELECT name
FROM customers
WHERE name = 'Bob' AND age = 55;
```

### OR

Requires **at least one** condition to be true.

```sql
SELECT name
FROM customers
WHERE name = 'Bob' OR age = 55;
```

### BETWEEN

Filters for values within a range (inclusive).

```sql
SELECT name
FROM customers
WHERE age BETWEEN 45 AND 55;
```

### LIKE

Searches for a pattern in a column.

```sql
SELECT name
FROM customers
WHERE name LIKE '%Bob%';
```

**LIKE pattern operators:**

| Pattern   | Meaning                                      |
|-----------|----------------------------------------------|
| `%x`      | Values that begin with x                     |
| `%x%`     | Values that contain x                        |
| `x%`      | Values that end with x                       |
| `x%y`     | Values that begin with x and end with y      |
| `_x%`     | Values with x as the second character        |
| `x_%`     | Values that begin with x and are ≥ 2 chars   |

### IN

Matches any value in a list.

```sql
SELECT name
FROM customers
WHERE name IN ('Bob', 'Fred', 'Harry');
```

### IS NULL / IS NOT NULL

```sql
SELECT name
FROM customers
WHERE name IS NULL;

SELECT name
FROM customers
WHERE name IS NOT NULL;
```

---

## CREATE

### CREATE DATABASE

```sql
CREATE DATABASE dataquestDB;
```

### CREATE TABLE

```sql
CREATE TABLE customers (
    customer_id int,
    name varchar(255),
    age int
);
```

### CREATE INDEX

Speeds up data retrieval.

```sql
CREATE INDEX idx_name
ON customers (name);
```

### CREATE VIEW

Creates a virtual table based on a query result.

```sql
CREATE VIEW [Bob Customers] AS
SELECT name, age
FROM customers
WHERE name = 'Bob';
```

---

## DROP

**Use with extreme caution** — these permanently delete objects and data.

### DROP DATABASE

```sql
DROP DATABASE dataquestDB;
```

### DROP TABLE

```sql
DROP TABLE customers;
```

### DROP INDEX

```sql
DROP INDEX idx_name;
```

---

## UPDATE

Modifies existing data.

```sql
UPDATE customers
SET age = 56
WHERE name = 'Bob';
```

---

## DELETE

Removes rows (can be filtered with WHERE).

```sql
DELETE FROM customers
WHERE name = 'Bob';
```

---

## ALTER TABLE

Adds or removes columns.

```sql
ALTER TABLE customers
ADD surname varchar(255);

ALTER TABLE customers
DROP COLUMN surname;
```

---

## Aggregate Functions

Perform a calculation on a set of values and return a single result.

### COUNT

```sql
SELECT COUNT(*)
FROM customers;
```

### SUM

```sql
SELECT SUM(age)
FROM customers;
```

### AVG

```sql
SELECT AVG(age)
FROM customers;
```

### MIN / MAX

```sql
SELECT MIN(age)
FROM customers;

SELECT MAX(age)
FROM customers;
```

---

## GROUP BY

Groups rows that have the same values. Almost always used with aggregate functions.

```sql
SELECT name, AVG(age)
FROM customers
GROUP BY name;
```

### HAVING

Filters **after** aggregation (WHERE cannot filter aggregates).

```sql
SELECT COUNT(customer_id), name
FROM customers
GROUP BY name
HAVING COUNT(customer_id) > 2;
```

---

## ORDER BY

Sorts results. Default is ascending.

```sql
SELECT name
FROM customers
ORDER BY age;
```

### DESC

```sql
SELECT name
FROM customers
ORDER BY age DESC;
```

### OFFSET + FETCH

Skips rows, then returns a limited set (useful for pagination).

```sql
SELECT name
FROM customers
ORDER BY age
OFFSET 10 ROWS
FETCH NEXT 10 ROWS ONLY;
```

---

## JOINS

Combine rows from two or more tables.

### INNER JOIN

Only rows with matching values in both tables.

```sql
SELECT name
FROM customers
INNER JOIN orders
ON customers.customer_id = orders.customer_id;
```

### LEFT JOIN

All rows from the left table + matching rows from the right.

```sql
SELECT name
FROM customers
LEFT JOIN orders
ON customers.customer_id = orders.customer_id;
```

### RIGHT JOIN

All rows from the right table + matching rows from the left.

```sql
SELECT name
FROM customers
RIGHT JOIN orders
ON customers.customer_id = orders.customer_id;
```

### FULL OUTER JOIN

Rows that have a match in either table.

```sql
SELECT name
FROM customers
FULL OUTER JOIN orders
ON customers.customer_id = orders.customer_id;
```

---

## EXISTS

Tests for the existence of any record in a subquery.

```sql
SELECT name
FROM customers
WHERE EXISTS (
    SELECT order_id FROM orders WHERE customer_id = 1
);
```

---

## Permissions

### GRANT

```sql
GRANT SELECT, UPDATE ON customers TO usr_bob;
```

### REVOKE

```sql
REVOKE SELECT, UPDATE ON customers FROM usr_bob;
```

---

## Transaction Control

### SAVEPOINT

```sql
SAVEPOINT SAVEPOINT_NAME;
```

### COMMIT

Saves the transaction permanently.

```sql
DELETE FROM customers
WHERE name = 'Bob';
COMMIT;
```

### ROLLBACK

Undoes changes since the last COMMIT or to a named SAVEPOINT.

```sql
ROLLBACK TO SAVEPOINT_NAME;
```

---

## TRUNCATE

Removes all rows from a table but keeps the table structure. Faster than DELETE for full clears.

```sql
TRUNCATE TABLE customers;
```

---

## UNION / UNION ALL

Combine result sets from multiple SELECT statements.

- `UNION` removes duplicates  
- `UNION ALL` keeps duplicates

```sql
SELECT name FROM customers
UNION
SELECT name FROM orders;

SELECT name FROM customers
UNION ALL
SELECT name FROM orders;
```

---

*Reference built for Domain Specialist work – Glorystone Data Analytics track.*
