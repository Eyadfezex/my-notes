# Basic SQL Syntax

SQL uses a standardized set of keywords and structures for working with relational databases. Keywords are usually written in **UPPERCASE**, but they are case-insensitive.

---

## Common SQL Keywords

### Querying Data

- `SELECT`: retrieve data from tables
- `FROM`: specify which table(s) to query
- `WHERE`: filter rows by conditions
- `DISTINCT`: return only unique results
- `ORDER BY`: sort the results
- `GROUP BY`: group rows for aggregation
- `HAVING`: filter groups after aggregation
- `LIMIT`, `OFFSET`: restrict or skip rows in the result

### Data Manipulation (DML)

- `INSERT INTO`: add records to a table
- `VALUES`: provide new record values
- `UPDATE`: modify existing records
- `SET`: assign new column values
- `DELETE`: remove records

### Data Definition (DDL)

- `CREATE TABLE`: create a new table  
  _Example_:

  ```sql
  CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(50)
  );
  ```

- `ALTER TABLE`: modify a table  
  _Example_:

  ```sql
  ALTER TABLE users ADD email VARCHAR(100);
  ```

- `DROP TABLE`: delete a table  
  _Example_:

  ```sql
  DROP TABLE users;
  ```

- `TRUNCATE TABLE`: remove all rows quickly  
  _Example_:

  ```sql
  TRUNCATE TABLE users;
  ```

- `PRIMARY KEY`, `FOREIGN KEY`: define keys and relationships  
  _Example_:

  ```sql
  CREATE TABLE orders (
    id INT PRIMARY KEY,
    user_id INT,
    FOREIGN KEY (user_id) REFERENCES users(id)
  );
  ```

- `UNIQUE`, `NOT NULL`, `CHECK`: enforce constraints  
  _Example_:

  ```sql
  CREATE TABLE products (
    id INT PRIMARY KEY,
    sku VARCHAR(20) UNIQUE,
    price DECIMAL(10,2) NOT NULL,
    quantity INT CHECK (quantity >= 0)
  );
  ```

### Joins

- `JOIN`, `INNER JOIN`: combine matching rows from tables  
  _Example_:

  ```sql
  SELECT users.name, orders.id
  FROM users
  INNER JOIN orders ON users.id = orders.user_id;
  ```

- `LEFT JOIN`, `RIGHT JOIN`: include all rows from one side, matched when possible  
  _Example (LEFT JOIN)_:

  ```sql
  SELECT users.name, orders.id
  FROM users
  LEFT JOIN orders ON users.id = orders.user_id;
  ```

  _Example (RIGHT JOIN)_:

  ```sql
  SELECT users.name, orders.id
  FROM users
  RIGHT JOIN orders ON users.id = orders.user_id;
  ```

- `FULL JOIN`: include all rows from both tables  
  _Example_:

  ```sql
  SELECT users.name, orders.id
  FROM users
  FULL JOIN orders ON users.id = orders.user_id;
  ```

- `ON`: specify joining conditions  
  _Example_:

  ```sql
  SELECT *
  FROM products
  JOIN orders ON products.id = orders.product_id;
  ```

- `USING`: join by common column  
  _Example_:

  ```sql
  SELECT *
  FROM products
  JOIN inventory USING (id);
  ```

### Functions and Expressions

- `COUNT()`, `SUM()`, `AVG()`, `MIN()`, `MAX()`: aggregate functions
- `CONCAT()`, `UPPER()`, `LOWER()`: string functions
- `CAST()`, `CONVERT()`: type conversions
- `NOW()`, `CURDATE()`, `DATEADD()`: date/time functions

### Subqueries and Advanced

- `WITH`: common table expressions (CTE)
- `EXISTS`: check row existence in a subquery
- `IN`: match values in a set
- `BETWEEN`: match within a range
- `LIKE`: pattern matching

### Transactions and Control

- `BEGIN`: start a transaction
- `COMMIT`: apply changes
- `ROLLBACK`: undo changes
- `SAVEPOINT`: set a transaction save point

---

# SQL Data Types

Data types specify the kind of values allowed in a column.

## Numeric Types

- **INT / INTEGER**: whole numbers (e.g. 1, 50, 999)
- **SMALLINT / TINYINT**: small-range whole numbers
- **BIGINT**: large whole numbers
- **DECIMAL(p, s)**: exact decimal numbers (e.g. for money)
- **NUMERIC(p, s)**: like DECIMAL
- **FLOAT / REAL**: approximate decimals
- **DOUBLE**: higher-precision floating point

## Character & String Types

- **CHAR(n)**: fixed-length text
- **VARCHAR(n)**: variable-length text
- **TEXT**: large text field
- **NVARCHAR / NCHAR**: Unicode strings

## Date & Time Types

- **DATE**: YYYY-MM-DD
- **TIME**: HH:MM:SS
- **DATETIME**: date and time
- **TIMESTAMP**: auto-updating time (varies by DB)
- **YEAR**: stores a year

## Boolean Type

- **BOOLEAN / BOOL**: TRUE or FALSE (may be stored as 0/1)

## Binary Types

- **BINARY**: fixed-length binary data
- **VARBINARY**: variable-length binary data
- **BLOB**: large binary objects

## JSON & Semi-Structured Types

- **JSON**: JSON data (Postgres, MySQL)
- **JSONB**: binary JSON (Postgres)

## Spatial / Geographic Types

- **POINT**, **LINESTRING**, **POLYGON**: geographic data (DB-dependent)

## Special Types (DB-specific)

- **ENUM**: predefined values (MySQL)
- **UUID**: universally unique identifiers (Postgres)
- **SERIAL / AUTO_INCREMENT**: auto-incrementing integer

---

## **SQL Operators**

SQL operators let you filter, compare, and manipulate data inside queries. They’re the little tools you flex to shape your results.

### **1. Comparison Operators**

Used to compare values in `WHERE` clauses.

| Operator     | Meaning          | Example                    |
| ------------ | ---------------- | -------------------------- |
| `=`          | Equal            | `WHERE age = 20`           |
| `!=` or `<>` | Not equal        | `WHERE status != 'active'` |
| `>`          | Greater than     | `WHERE score > 90`         |
| `<`          | Less than        | `WHERE price < 50`         |
| `>=`         | Greater or equal | `WHERE height >= 180`      |
| `<=`         | Less or equal    | `WHERE points <= 10`       |

---

### 2. Logical Operators

| Operator | Meaning                        | Example                                         |
| -------- | ------------------------------ | ----------------------------------------------- |
| `AND`    | Both conditions are true       | `WHERE country = 'USA' AND population > 100000` |
| `OR`     | At least one condition is true |                                                 |
| `NOT`    | Negates a condition            |                                                 |

---

### 3. Arithmetic Operators

| Operator | Meaning             | Example            |
| -------- | ------------------- | ------------------ |
| `+`      | Add                 | `salary + 1000`    |
| `-`      | Subtract            | `price - discount` |
| `*`      | Multiply            | `quantity * cost`  |
| `/`      | Divide              | `total / 2`        |
| `%`      | Modulus (remainder) | `id % 2 = 0`       |

---

### 4. String Operators

| Operator   | Meaning              | Example                                     |
| ---------- | -------------------- | ------------------------------------------- |
| `LIKE`     | Pattern matching     | `WHERE name LIKE 'A%'`                      |
| `NOT LIKE` | Not matching pattern | `WHERE email NOT LIKE '%gmail%'`            |
| `CONCAT()` | String concatenation | `SELECT CONCAT(first_name, ' ', last_name)` |

---

### 5. Set Operators

| Operator            | Meaning                              |
| ------------------- | ------------------------------------ |
| `UNION`             | Combines results, removes duplicates |
| `UNION ALL`         | Combines results, keeps duplicates   |
| `INTERSECT`         | Rows present in both queries         |
| `EXCEPT` or `MINUS` | Rows in first query, not in second   |

---

### 6. Special Operators

| Operator      | Meaning                   | Example                               |
| ------------- | ------------------------- | ------------------------------------- |
| `IN`          | Matches a value in a list | `WHERE id IN (1, 2, 3)`               |
| `NOT IN`      | Does not match list       | `WHERE city NOT IN ('Paris', 'Rome')` |
| `BETWEEN`     | Range matching            | `WHERE age BETWEEN 18 AND 30`         |
| `IS NULL`     | Checks for null           | `WHERE phone IS NULL`                 |
| `IS NOT NULL` | Checks for not null       | `WHERE phone IS NOT NULL`             |
