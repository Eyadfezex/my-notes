# PostgreSQL Query Basics

Queries in PostgreSQL are used to retrieve data from tables using the `SELECT` statement. Below are the key concepts and syntax for writing queries.

---

## 1. Basic Query Structure

```sql
SELECT column1, column2, ...
FROM table_name;
```

- **`SELECT`**: Specifies the columns to retrieve.
- **`FROM`**: Specifies the table from which to retrieve data.

---

## 2. Retrieving All Columns

Use the `*` wildcard to retrieve all columns from a table:

```sql
SELECT * FROM table_name;
```

---

## 3. Retrieving Specific Columns

List the columns you want to retrieve after the `SELECT` keyword:

```sql
SELECT column1, column2 FROM table_name;
```

---

## 4. Filtering Rows with `WHERE`

The `WHERE` clause filters rows based on a condition:

```sql
SELECT column1, column2
FROM table_name
WHERE condition;
```

### Example:

```sql
SELECT name, age
FROM users
WHERE age > 18;
```

---

## 5. Sorting Results with `ORDER BY`

The `ORDER BY` clause sorts the result set by one or more columns:

```sql
SELECT column1, column2
FROM table_name
ORDER BY column1 ASC, column2 DESC;
```

- **`ASC`**: Ascending order (default).
- **`DESC`**: Descending order.

### Example:

```sql
SELECT name, age
FROM users
ORDER BY age DESC;
```

---

## 6. Limiting Results with `LIMIT`

The `LIMIT` clause restricts the number of rows returned:

```sql
SELECT column1, column2
FROM table_name
LIMIT number_of_rows;
```

### Example:

```sql
SELECT name, age
FROM users
LIMIT 10;
```

---

## 7. Skipping Rows with `OFFSET`

The `OFFSET` clause skips a specified number of rows before returning results:

```sql
SELECT column1, column2
FROM table_name
LIMIT number_of_rows OFFSET number_of_rows_to_skip;
```

### Example:

```sql
SELECT name, age
FROM users
LIMIT 10 OFFSET 20;  -- Skips the first 20 rows and returns the next 10
```

---

## 8. Combining Conditions with `AND`/`OR`

Use `AND` and `OR` to combine multiple conditions in the `WHERE` clause:

```sql
SELECT column1, column2
FROM table_name
WHERE condition1 AND condition2;
```

### Example:

```sql
SELECT name, age
FROM users
WHERE age > 18 AND country = 'USA';
```

---

## 9. Using `DISTINCT` to Remove Duplicates

The `DISTINCT` keyword removes duplicate rows from the result set:

```sql
SELECT DISTINCT column1, column2
FROM table_name;
```

### Example:

```sql
SELECT DISTINCT country
FROM users;
```

---

## 10. Aggregating Data with `GROUP BY`

The `GROUP BY` clause groups rows that have the same values into summary rows:

```sql
SELECT column1, COUNT(*)
FROM table_name
GROUP BY column1;
```

### Example:

```sql
SELECT country, COUNT(*)
FROM users
GROUP BY country;
```

---

## 11. Filtering Groups with `HAVING`

The `HAVING` clause filters groups based on a condition (used with `GROUP BY`):

```sql
SELECT column1, COUNT(*)
FROM table_name
GROUP BY column1
HAVING condition;
```

### Example:

```sql
SELECT country, COUNT(*)
FROM users
GROUP BY country
HAVING COUNT(*) > 10;
```

---

## 12. Combining Tables with `JOIN`

Use `JOIN` to combine rows from two or more tables based on a related column:

```sql
SELECT column1, column2
FROM table1
JOIN table2 ON table1.column = table2.column;
```

### Example:

```sql
SELECT users.name, orders.order_id
FROM users
JOIN orders ON users.id = orders.user_id;
```

---

## 13. Subqueries

A subquery is a query nested inside another query:

```sql
SELECT column1
FROM table_name
WHERE column2 = (SELECT column2 FROM another_table WHERE condition);
```

### Example:

```sql
SELECT name
FROM users
WHERE age = (SELECT MAX(age) FROM users);
```

---

## 14. Using `CASE` for Conditional Logic

The `CASE` statement allows conditional logic in queries:

```sql
SELECT column1,
       CASE
           WHEN condition1 THEN result1
           WHEN condition2 THEN result2
           ELSE result3
       END AS new_column_name
FROM table_name;
```

### Example:

```sql
SELECT name,
       CASE
           WHEN age < 18 THEN 'Minor'
           ELSE 'Adult'
       END AS age_group
FROM users;
```

---

## Summary

- Use `SELECT` to retrieve data.
- Filter rows with `WHERE`.
- Sort results with `ORDER BY`.
- Limit results with `LIMIT` and `OFFSET`.
- Remove duplicates with `DISTINCT`.
- Group data with `GROUP BY` and filter groups with `HAVING`.
- Combine tables with `JOIN`.
- Use subqueries and `CASE` for advanced logic.

For more details, refer to the [PostgreSQL SELECT Documentation](https://www.postgresql.org/docs/current/tutorial-select.html).
