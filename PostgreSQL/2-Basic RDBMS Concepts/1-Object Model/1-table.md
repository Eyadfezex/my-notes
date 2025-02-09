# PostgreSQL Tables

In PostgreSQL, **tables** are used to store and organize data in a structured format. Each table consists of rows (records) and columns (fields).

---

## **1. Creating a Table**

Use the `CREATE TABLE` statement to create a table.

```sql
CREATE TABLE table_name (
    column1_name data_type constraints,
    column2_name data_type constraints,
    ...
);
```

_**Example**_

```sql
CREATE TABLE employees (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    salary NUMERIC(10, 2),
    hire_date DATE
);
```

---

## **2. Listing Tables**

To list all tables in the current database:

```sql
\dt
```

Or query the system catalog:

```sql
SELECT table_name FROM information_schema.tables WHERE table_schema = 'public';
```

---

## **3. Describing a Table**

To view the structure of a table:

```sql
\d table_name
```

---

## **4. Inserting Data**

Use the `INSERT INTO` statement to add data.

```sql
INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...);
```

_**Example**_

```sql
INSERT INTO employees (name, salary, hire_date)
VALUES ('John Doe', 60000, '2023-01-15');
```

---

## **5. Querying Data**

Use the `SELECT` statement to retrieve data.

```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

_**Example**_

```sql
SELECT * FROM employees WHERE salary > 50000;
```

---

## **6. Updating Data**

Use the `UPDATE` statement to modify data.

```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

_**Example**_

```sql
UPDATE employees
SET salary = 65000
WHERE name = 'John Doe';
```

---

## **7. Deleting Data**

Use the `DELETE` statement to remove rows.

```sql
DELETE FROM table_name
WHERE condition;
```

_**Example**_

```sql
DELETE FROM employees
WHERE id = 1;
```

---

## **8. Altering a Table**

Use the `ALTER TABLE` statement to modify the table structure.

### Add a Column

```sql
ALTER TABLE employees
ADD COLUMN department VARCHAR(50);
```

### Drop a Column

```sql
ALTER TABLE employees
DROP COLUMN department;
```

### Modify a Column

```sql
ALTER TABLE employees
ALTER COLUMN salary TYPE NUMERIC(12, 2);
```

### Rename a Table

```sql
ALTER TABLE employees
RENAME TO staff;
```

---

## **9. Dropping a Table**

Use the `DROP TABLE` statement to delete a table.

```sql
DROP TABLE table_name;
```

_**Example**_

```sql
DROP TABLE employees;
```

---

## **10. Constraints**

Constraints enforce rules on the data in a table.

### Primary Key

```sql
CREATE TABLE employees (
    id SERIAL PRIMARY KEY,
    ...
);
```

### Foreign Key

```sql
CREATE TABLE departments (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100)
);

CREATE TABLE employees (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    department_id INT REFERENCES departments(id)
);
```

### Unique

```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    email VARCHAR(100) UNIQUE
);
```

### Not Null

```sql
CREATE TABLE employees (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL
);
```

### Check

```sql
CREATE TABLE employees (
    id SERIAL PRIMARY KEY,
    salary NUMERIC(10, 2) CHECK (salary > 0)
);
```

---

## **11. Indexes**

Indexes improve query performance.

### Create an Index

```sql
CREATE INDEX idx_employees_name ON employees(name);
```

### Drop an Index

```sql
DROP INDEX idx_employees_name;
```

---

## **12\_**Example**\_orkflow**

1. **Create a Table**:

   ```sql
   CREATE TABLE employees (
       id SERIAL PRIMARY KEY,
       name VARCHAR(100) NOT NULL,
       salary NUMERIC(10, 2),
       hire_date DATE
   );
   ```

2. **Insert Data**:

   ```sql
   INSERT INTO employees (name, salary, hire_date)
   VALUES ('John Doe', 60000, '2023-01-15');
   ```

3. **Query Data**:

   ```sql
   SELECT * FROM employees WHERE salary > 50000;
   ```

4. **Update Data**:

   ```sql
   UPDATE employees
   SET salary = 65000
   WHERE name = 'John Doe';
   ```

5. **Delete Data**:

   ```sql
   DELETE FROM employees
   WHERE id = 1;
   ```

6. **Drop the Table**:

   ```sql
   DROP TABLE employees;
   ```
