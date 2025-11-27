# Data Manipulation Language (DML)

DML commands are used to manage the data within tables. They modify the rows but do not affect the structure of the table.

**Main DML commands:**

- `SELECT` – Retrieve data
- `INSERT` – Add data
- `UPDATE` – Modify existing data
- `DELETE` – Remove data

---

## 1. SELECT — Retrieve Data

Fetch data from one or more tables.

**Basic example:**

```sql
SELECT *
FROM Employees;
```

**Select specific columns:**

```sql
SELECT name, salary
FROM Employees;
```

**With a condition:**

```sql
SELECT name, department
FROM Employees
WHERE department = 'IT';
```

**Sort results:**

```sql
SELECT name, salary
FROM Employees
ORDER BY salary DESC;
```

---

## 2. INSERT — Add New Rows

Add new records to a table.

**Insert a single row:**

```sql
INSERT INTO Employees (id, name, department, salary)
VALUES (1, 'John Doe', 'IT', 5000);
```

**Insert multiple rows:**

```sql
INSERT INTO Employees (id, name, department, salary)
VALUES
    (2, 'Sarah', 'HR', 4200),
    (3, 'Tom', 'Finance', 6000);
```

---

## 3. UPDATE — Modify Existing Rows

Change data in existing rows.

**Update a specific record:**

```sql
UPDATE Employees
SET salary = 5500
WHERE id = 1;
```

**Update multiple rows:**

```sql
UPDATE Employees
SET department = 'General'
WHERE department = 'HR';
```

> ⚠️ Always use `WHERE` unless you want to update all rows.

---

## 4. DELETE — Remove Rows

Delete records from a table.

**Delete specific rows:**

```sql
DELETE FROM Employees
WHERE id = 3;
```

**Delete all rows (dangerous):**

```sql
DELETE FROM Employees;
```

> ⚠️ This deletes all rows but leaves the table structure intact.

---

## Quick Reference Table

| Command | Purpose     | Example                           |
| ------- | ----------- | --------------------------------- |
| SELECT  | Read data   | `SELECT * FROM users;`            |
| INSERT  | Add data    | `INSERT INTO users VALUES (...);` |
| UPDATE  | Change data | `UPDATE users SET name = 'Ali';`  |
| DELETE  | Remove data | `DELETE FROM users WHERE id = 1;` |
