# Joining Tables in SQL

Joins are used to combine rows from two or more tables based on a related column between them. Below is a simplified explanation of the different types of joins in PostgreSQL, along with examples and their expected results.

---

## Types of Joins

### 1. `INNER JOIN`

- Returns only rows where there is a match in both tables.
- Non-matching rows are excluded.

#### Syntax

```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

#### Example

**Query**:

```sql
SELECT employees.name, departments.department_name
FROM employees
INNER JOIN departments
ON employees.department_id = departments.id;
```

**Tables**:

- `employees`:

  | id  | name    | department_id |
  | --- | ------- | ------------- |
  | 1   | Alice   | 101           |
  | 2   | Bob     | 102           |
  | 3   | Charlie | 103           |

- `departments`:

  | id  | department_name |
  | --- | --------------- |
  | 101 | HR              |
  | 102 | Engineering     |
  | 104 | Sales           |

**Result**:

| name  | department_name |
| ----- | --------------- |
| Alice | HR              |
| Bob   | Engineering     |

- Only rows with matching `department_id` are included.

---

### 2. `LEFT JOIN` (or `LEFT OUTER JOIN`)

- Returns all rows from the left table (`table1`) and matching rows from the right table (`table2`).
- If no match is found, `NULL` values are returned for columns from the right table.

#### Syntax

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```

#### Example

**Query**:

```sql
SELECT employees.name, departments.department_name
FROM employees
LEFT JOIN departments
ON employees.department_id = departments.id;
```

**Result**:

| name    | department_name |
| ------- | --------------- |
| Alice   | HR              |
| Bob     | Engineering     |
| Charlie | NULL            |

- All rows from `employees` are included, even if there’s no matching `department_id`.

---

### 3. `RIGHT JOIN` (or `RIGHT OUTER JOIN`)

- Returns all rows from the right table (`table2`) and matching rows from the left table (`table1`).
- If no match is found, `NULL` values are returned for columns from the left table.

#### Syntax

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```

#### Example

**Query**:

```sql
SELECT employees.name, departments.department_name
FROM employees
RIGHT JOIN departments
ON employees.department_id = departments.id;
```

**Result**:

| name  | department_name |
| ----- | --------------- |
| Alice | HR              |
| Bob   | Engineering     |
| NULL  | Sales           |

- All rows from `departments` are included, even if there’s no matching `department_id`.

---

### 4. `FULL JOIN` (or `FULL OUTER JOIN`)

- Returns all rows when there is a match in either the left or right table.
- If no match is found, `NULL` values are returned for missing sides.

#### Syntax

```sql
SELECT columns
FROM table1
FULL JOIN table2
ON table1.column = table2.column;
```

#### Example

**Query**:

```sql
SELECT employees.name, departments.department_name
FROM employees
FULL JOIN departments
ON employees.department_id = departments.id;
```

**Result**:

| name    | department_name |
| ------- | --------------- |
| Alice   | HR              |
| Bob     | Engineering     |
| Charlie | NULL            |
| NULL    | Sales           |

- Combines all rows from both tables, with `NULL` for non-matching rows.

---

### 5. `CROSS JOIN`

- Returns the Cartesian product of the two tables (all possible combinations of rows).
- No `ON` clause is used.

#### Syntax

```sql
SELECT columns
FROM table1
CROSS JOIN table2;
```

#### Example

**Query**:

```sql
SELECT employees.name, departments.department_name
FROM employees
CROSS JOIN departments;
```

**Result**:

| name    | department_name |
| ------- | --------------- |
| Alice   | HR              |
| Alice   | Engineering     |
| Alice   | Sales           |
| Bob     | HR              |
| Bob     | Engineering     |
| Bob     | Sales           |
| Charlie | HR              |
| Charlie | Engineering     |
| Charlie | Sales           |

- Combines every row from `employees` with every row from `departments`.

---

### 6. `SELF JOIN`

- A table is joined with itself.
- Useful for comparing rows within the same table.

#### Syntax

```sql
SELECT columns
FROM table1 t1
JOIN table1 t2
ON t1.column = t2.column;
```

#### Example

**Query**:

```sql
SELECT e1.name AS employee, e2.name AS manager
FROM employees e1
JOIN employees e2
ON e1.manager_id = e2.id;
```

**Table** (`employees`):

| id  | name    | manager_id |
| --- | ------- | ---------- |
| 1   | Alice   | 3          |
| 2   | Bob     | 3          |
| 3   | Charlie | NULL       |

**Result**:

| employee | manager |
| -------- | ------- |
| Alice    | Charlie |
| Bob      | Charlie |

- Compares rows within the same table to find employees and their managers.

---

## Join Conditions

- Use the `ON` clause to specify the condition for joining tables.
- Use `AND` or `OR` for multiple conditions.

#### Example

**Query**:

```sql
SELECT employees.name, departments.department_name
FROM employees
INNER JOIN departments
ON employees.department_id = departments.id
AND departments.location = 'New York';
```

**Result**:

- Only includes rows where the department is located in New York.

---

## Best Practices

1. **Use Aliases**: Use meaningful table aliases to simplify queries.

   ```sql
   SELECT e.name, d.department_name
   FROM employees e
   INNER JOIN departments d ON e.department_id = d.id;
   ```

2. **Specify Join Conditions**: Always specify the join condition to avoid unintended Cartesian products.

3. **Choose the Right Join**:
   - Use `INNER JOIN` for matching rows.
   - Use `LEFT JOIN` to include non-matching rows from the left table.
