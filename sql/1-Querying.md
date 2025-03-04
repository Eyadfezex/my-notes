# `SELECT` Statement

The `SELECT` statement is used to fetch data from one or more tables in a database.

## Basic Syntax

```sql
SELECT columns
FROM table
WHERE condition
ORDER BY column
LIMIT number;
```

## Key Parts of `SELECT`

### `SELECT`

- Choose which columns to display.
- Use `*` to select all columns.
- Use `DISTINCT` to remove duplicates.

### `FROM`

- Specify the table(s) to get data from.

### `WHERE`

- Filter rows based on a condition (e.g., `salary > 50000`).

### `ORDER BY`

- Sort results by a column.
- Use `ASC` for ascending (default) or `DESC` for descending.

### `LIMIT`

- Limit the number of rows returned.

### `GROUP BY`

- Group rows with the same values (e.g., group by department).
- Often used with functions like `COUNT`, `SUM`, or `AVG`.

### `HAVING`

- Filter groups after `GROUP BY` (e.g., `HAVING AVG(salary) > 50000`).

### `UNION`, `INTERSECT`, `EXCEPT`

- Combine results from multiple queries:
  - `UNION`: Combine results, remove duplicates.
  - `INTERSECT`: Show common rows.
  - `EXCEPT`: Show rows in the first query but not the second.

### `OFFSET`

- Skip a number of rows before returning results.

### `FETCH`

- Retrieve a specific number of rows (similar to `LIMIT`).

## Examples

### Simple Query

```sql
SELECT name, age FROM users;
```

### Filter with `WHERE`

```sql
SELECT name FROM employees WHERE salary > 50000;
```

### Sort with `ORDER BY`

```sql
SELECT name, salary FROM employees ORDER BY salary DESC;
```

### Limit Results

```sql
SELECT name FROM users LIMIT 10;
```

### Group Data

```sql
SELECT department, AVG(salary)
FROM employees
GROUP BY department;
```

### Combine Queries with `UNION`

```sql
SELECT name FROM employees
UNION
SELECT name FROM contractors;
```

## Tips

- Use `EXPLAIN` to check how your query runs.
- Add indexes to speed up queries on large tables.

For more details, visit the [official documentation](https://www.postgresql.org/docs/current/sql-select.html).
