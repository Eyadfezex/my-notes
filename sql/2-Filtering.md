# Filtering Data in PostgreSQL

Filtering data allows you to retrieve only the rows that meet specific conditions. This is done using the `WHERE` clause in a `SELECT` statement.

---

## `WHERE` Clause

The `WHERE` clause is used to filter rows based on a condition.

### Syntax

```sql
SELECT columns
FROM table
WHERE condition;
```

### Examples

1. Filter rows where `age` is greater than 30:

   ```sql
   SELECT name, age FROM users WHERE age > 30;
   ```

2. Filter rows where `name` is 'John':

   ```sql
   SELECT * FROM employees WHERE name = 'John';
   ```

3. Filter rows where `salary` is between 50000 and 80000:

   ```sql
   SELECT name, salary FROM employees WHERE salary BETWEEN 50000 AND 80000;
   ```

---

## Common Operators for Filtering

### Comparison Operators

- `=` : Equal to
- `!=` or `<>` : Not equal to
- `>` : Greater than
- `<` : Less than
- `>=` : Greater than or equal to
- `<=` : Less than or equal to

### Logical Operators

- `AND` : Both conditions must be true.
- `OR` : At least one condition must be true.
- `NOT` : Negates a condition.

### Examples

1. Filter rows where `age` is greater than 25 **AND** `city` is 'New York':

   ```sql
   SELECT * FROM users WHERE age > 25 AND city = 'New York';
   ```

2. Filter rows where `department` is 'Sales' **OR** 'Marketing':

   ```sql
   SELECT * FROM employees WHERE department = 'Sales' OR department = 'Marketing';
   ```

3. Filter rows where `salary` is **NOT** 50000:

   ```sql
   SELECT * FROM employees WHERE NOT salary = 50000;
   ```

---

## Filtering with `IN` and `NOT IN`

Use `IN` to check if a value matches any value in a list. Use `NOT IN` to exclude values.

### Examples

1. Filter rows where `department` is either 'HR', 'IT', or 'Finance':

   ```sql
   SELECT * FROM employees WHERE department IN ('HR', 'IT', 'Finance');
   ```

2. Filter rows where `city` is **NOT** 'London' or 'Paris':

   ```sql
   SELECT * FROM users WHERE city NOT IN ('London', 'Paris');
   ```

---

## Filtering with `LIKE`

Use `LIKE` to filter rows based on patterns in text.

- `%` : Matches any sequence of characters.
- `_` : Matches a single character.

### Examples

1. Filter rows where `name` starts with 'J':

   ```sql
   SELECT * FROM users WHERE name LIKE 'J%';
   ```

2. Filter rows where `email` contains 'gmail':

   ```sql
   SELECT * FROM users WHERE email LIKE '%gmail%';
   ```

3. Filter rows where `name` has exactly 5 characters:

   ```sql
   SELECT * FROM users WHERE name LIKE '_____';
   ```

---

## Filtering with `IS NULL` and `IS NOT NULL`

Use these to filter rows where a column has `NULL` or non-`NULL` values.

### Examples

1. Filter rows where `email` is missing (`NULL`):

   ```sql
   SELECT * FROM users WHERE email IS NULL;
   ```

2. Filter rows where `phone` is not missing:

   ```sql
   SELECT * FROM users WHERE phone IS NOT NULL;
   ```

---

## Combining Filters

You can combine multiple conditions using parentheses for clarity.

### Example

Filter rows where `age` is greater than 25 **AND** (`city` is 'New York' **OR** `city` is 'London'):

```sql
SELECT * FROM users
WHERE age > 25
AND (city = 'New York' OR city = 'London');
```

---

## Notes

- Always test your conditions to ensure they return the expected results.
- Use indexes on filtered columns to improve query performance.

For more details, refer to the [official documentation](https://www.postgresql.org/docs/current/sql-select.html).
