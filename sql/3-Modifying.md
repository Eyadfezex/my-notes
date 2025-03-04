# Modifying Data in PostgreSQL

PostgreSQL provides several statements to modify data in tables: `INSERT`, `UPDATE`, `DELETE`, and `TRUNCATE`.

---

## 1. `INSERT` Statement

The `INSERT` statement is used to add new rows to a table.

### Syntax

```sql
INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...);
```

### Examples

1. Insert a single row:

   ```sql
   INSERT INTO employees (name, salary, department)
   VALUES ('John Doe', 60000, 'Sales');
   ```

2. Insert multiple rows at once:

   ```sql
   INSERT INTO employees (name, salary, department)
   VALUES
   ('Jane Smith', 55000, 'HR'),
   ('Mike Johnson', 70000, 'IT');
   ```

3. Insert data from another table:

   ```sql
   INSERT INTO managers (name, department)
   SELECT name, department FROM employees WHERE salary > 80000;
   ```

---

## 2. `UPDATE` Statement

The `UPDATE` statement is used to modify existing rows in a table.

### Syntax

```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

### Examples

1. Update a single column:

   ```sql
   UPDATE employees
   SET salary = 65000
   WHERE name = 'John Doe';
   ```

2. Update multiple columns:

   ```sql
   UPDATE employees
   SET salary = 70000, department = 'Finance'
   WHERE id = 101;
   ```

3. Update all rows (use with caution!):

   ```sql
   UPDATE employees
   SET salary = salary * 1.1; -- Give everyone a 10% raise
   ```

---

## 3. `DELETE` Statement

The `DELETE` statement is used to remove rows from a table.

### Syntax

```sql
DELETE FROM table_name
WHERE condition;
```

### Examples

1. Delete specific rows:

   ```sql
   DELETE FROM employees
   WHERE department = 'HR';
   ```

2. Delete all rows (use with caution!):

   ```sql
   DELETE FROM employees;
   ```

---

## 4. `TRUNCATE` Statement

The `TRUNCATE` statement is used to remove all rows from a table quickly. It is faster than `DELETE` because it doesn't scan the table.

### Syntax

```sql
TRUNCATE TABLE table_name;
```

### Example

```sql
TRUNCATE TABLE employees;
```

---

## Key Differences Between `DELETE` and `TRUNCATE`

| Feature              | `DELETE`                       | `TRUNCATE`                        |
| -------------------- | ------------------------------ | --------------------------------- |
| Speed                | Slower (scans rows)            | Faster (removes all rows at once) |
| `WHERE` Clause       | Can use `WHERE` to filter rows | No `WHERE` clause                 |
| Reset Auto-Increment | Does not reset auto-increment  | Resets auto-increment             |
| Transaction Safety   | Can be rolled back             | Cannot be rolled back             |

---

## Best Practices

1. Always use a `WHERE` clause with `UPDATE` and `DELETE` unless you intend to modify all rows.
2. Use `TRUNCATE` for clearing large tables quickly.
3. Test your `UPDATE` and `DELETE` statements with a `SELECT` query first to ensure they target the correct rows.

For more details, refer to the [official documentation](https://www.postgresql.org/docs/current/sql-commands.html).
