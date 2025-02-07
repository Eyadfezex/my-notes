# What is SQL?

SQL (Structured Query Language) is a standard programming language used for managing and manipulating relational databases.

## SQL Commands

SQL commands can be categorized into different types:

### 1. Data Definition Language (DDL)

DDL commands are used to define and manage database schema.

- `CREATE`: Creates a new database, table, or index.
- `ALTER`: Modifies an existing database or table.
- `DROP`: Deletes a database, table, or index.
- `TRUNCATE`: Removes all records from a table without logging individual row deletions.

### 2. Data Manipulation Language (DML)

DML commands are used to manipulate data within tables.

- `SELECT`: Retrieves data from one or more tables.
- `INSERT`: Adds new records to a table.
- `UPDATE`: Modifies existing records in a table.
- `DELETE`: Removes records from a table.

### 3. Data Control Language (DCL)

DCL commands manage user permissions and security.

- `GRANT`: Provides access privileges to users.
- `REVOKE`: Removes access privileges from users.

### 4. Transaction Control Language (TCL)

TCL commands manage transactions in a database.

- `COMMIT`: Saves all changes made in the current transaction.
- `ROLLBACK`: Reverts all changes made in the current transaction.
- `SAVEPOINT`: Creates a savepoint within a transaction.

## SQL Clauses

- `WHERE`: Filters records based on a specified condition.
- `GROUP BY`: Groups rows that have the same values in specified columns.
- `HAVING`: Filters records after grouping.
- `ORDER BY`: Sorts the result set in ascending (`ASC`) or descending (`DESC`) order.
- `LIMIT`: Specifies the number of records to return.

## SQL Joins

Joins are used to retrieve data from multiple tables based on a related column.

- `INNER JOIN`: Returns records with matching values in both tables.
- `LEFT JOIN`: Returns all records from the left table and matching records from the right table.
- `RIGHT JOIN`: Returns all records from the right table and matching records from the left table.
- `FULL JOIN`: Returns all records from both tables.

## SQL Aggregate Functions

- `COUNT()`: Returns the number of rows.
- `SUM()`: Returns the sum of values in a column.
- `AVG()`: Returns the average value of a column.
- `MAX()`: Returns the highest value in a column.
- `MIN()`: Returns the lowest value in a column.

## SQL Constraints

Constraints enforce rules on data in tables.

- `PRIMARY KEY`: Uniquely identifies each record in a table.
- `FOREIGN KEY`: Establishes a relationship between tables.
- `UNIQUE`: Ensures all values in a column are unique.
- `NOT NULL`: Ensures a column cannot have NULL values.
- `CHECK`: Ensures that column values meet a specific condition.
- `DEFAULT`: Sets a default value for a column.

## SQL Normalization

Normalization is the process of structuring a database to reduce redundancy and improve data integrity.

- **1NF (First Normal Form)**: Eliminates duplicate columns and ensures atomicity.
- **2NF (Second Normal Form)**: Removes partial dependencies.
- **3NF (Third Normal Form)**: Removes transitive dependencies.

## Example Queries

```sql
-- Creating a table
CREATE TABLE Users (
    id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(255) UNIQUE
);

-- Inserting data
INSERT INTO Users (id, name, email) VALUES (1, 'John Doe', 'john@example.com');

-- Selecting data
SELECT * FROM Users WHERE name = 'John Doe';

-- Updating data
UPDATE Users SET email = 'john.doe@example.com' WHERE id = 1;

-- Deleting data
DELETE FROM Users WHERE id = 1;
```
