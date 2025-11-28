# SQL Data Constraints

Data constraints are rules defined on table columns to restrict the type of data that can be stored or to enforce certain properties for data integrity. Applying constraints ensures that the database remains accurate, consistent, and reliable.

## Common Types of Constraints (with examples)

- **NOT NULL**: Ensures that a column cannot have a NULL value; every row must have a value for this column.

  _Example:_

  ```sql
  name VARCHAR(100) NOT NULL
  ```

- **UNIQUE**: Guarantees that all values in a column (or combination of columns) are distinct across the table.

  _Example:_

  ```sql
  email VARCHAR(100) UNIQUE
  ```

  Or on multiple columns:

  ```sql
  CONSTRAINT unique_email_dept UNIQUE(email, department_id)
  ```

- **PRIMARY KEY**: Uniquely identifies each record in a table. A primary key column (or columns) automatically has both UNIQUE and NOT NULL properties.

  _Example:_

  ```sql
  id INT PRIMARY KEY
  ```

  Composite primary keys:

  ```sql
  PRIMARY KEY (order_id, product_id)
  ```

- **FOREIGN KEY**: Ensures referential integrity by requiring that a value in one table matches a value in another table’s primary (or unique) key.

  _Example:_

  ```sql
  department_id INT,
  FOREIGN KEY (department_id) REFERENCES Departments(id)
  ```

- **CHECK**: Restricts the allowable values for a column by enforcing a logical condition.

  _Example:_

  ```sql
  salary DECIMAL(10, 2) CHECK (salary > 0)
  ```

  Or:

  ```sql
  age INT CHECK (age >= 18 AND age <= 65)
  ```

- **DEFAULT**: Assigns a default value to a column if no value is provided during insertion.

  _Example:_

  ```sql
  hire_date DATE DEFAULT CURRENT_DATE
  ```

  Or:

  ```sql
  status VARCHAR(20) DEFAULT 'active'
  ```

---

## Examples: Applying Constraints in Table Creation

### Example 1: Full Table with Multiple Constraints

```sql
CREATE TABLE Employees (
  id INT PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  email VARCHAR(100) UNIQUE,
  department_id INT,
  salary DECIMAL(10, 2) CHECK (salary > 0),
  hire_date DATE DEFAULT CURRENT_DATE,
  status VARCHAR(20) DEFAULT 'active',
  FOREIGN KEY (department_id) REFERENCES Departments(id)
);
```

### Example 2: Composite Unique and Foreign Keys

```sql
CREATE TABLE ProjectAssignments (
  employee_id INT,
  project_id INT,
  assigned_at DATE DEFAULT CURRENT_DATE,
  PRIMARY KEY (employee_id, project_id),
  FOREIGN KEY (employee_id) REFERENCES Employees(id),
  FOREIGN KEY (project_id) REFERENCES Projects(id)
);
```
