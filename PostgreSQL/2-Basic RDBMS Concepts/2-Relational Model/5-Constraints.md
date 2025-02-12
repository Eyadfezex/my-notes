# Constraints in Relational Databases (PostgreSQL)

**Constraints** are rules enforced on tables (relations) in a relational database to maintain data integrity, consistency, and accuracy. In **PostgreSQL**, constraints are used to define restrictions on the data that can be stored in a table. Below are detailed notes about constraints:

---

## 1. **Types of Constraints**

PostgreSQL supports several types of constraints:

1. **Primary Key**:

   - Ensures that a column (or a set of columns) uniquely identifies each row in a table.
   - Automatically enforces **NOT NULL** and **UNIQUE** constraints.
   - Example:

     ```sql
     CREATE TABLE employees (
         id SERIAL PRIMARY KEY,
         name TEXT NOT NULL
     );
     ```

2. **Foreign Key**:

   - Ensures referential integrity by linking a column in one table to the primary key of another table.
   - Example:

     ```sql
     CREATE TABLE departments (
         id SERIAL PRIMARY KEY,
         name TEXT NOT NULL
     );

     CREATE TABLE employees (
         id SERIAL PRIMARY KEY,
         name TEXT NOT NULL,
         department_id INT REFERENCES departments(id)
     );
     ```

3. **Unique**:

   - Ensures that all values in a column (or a set of columns) are unique.
   - Example:

     ```sql
     CREATE TABLE users (
         id SERIAL PRIMARY KEY,
         email TEXT UNIQUE
     );
     ```

4. **Not Null**:

   - Ensures that a column cannot have NULL values.
   - Example:

     ```sql
     CREATE TABLE employees (
         id SERIAL PRIMARY KEY,
         name TEXT NOT NULL
     );
     ```

5. **Check**:

   - Ensures that a condition is satisfied for all rows in the table.
   - Example:

     ```sql
     CREATE TABLE employees (
         id SERIAL PRIMARY KEY,
         name TEXT NOT NULL,
         salary NUMERIC CHECK (salary > 0)
     );
     ```

6. **Exclusion**:

   - Ensures that no two rows in the table satisfy a specified condition.
   - Example:

     ```sql
     CREATE TABLE reservations (
         room INT,
         during TSRANGE,
         EXCLUDE USING GIST (room WITH =, during WITH &&)
     );
     ```

---

## 2. **Adding Constraints**

Constraints can be added when creating a table or later using the `ALTER TABLE` statement.

### **During Table Creation**

```sql
CREATE TABLE employees (
    id SERIAL PRIMARY KEY,
    name TEXT NOT NULL,
    email TEXT UNIQUE,
    salary NUMERIC CHECK (salary > 0),
    department_id INT REFERENCES departments(id)
);
```

### **Using `ALTER TABLE`**

```sql
ALTER TABLE employees
ADD CONSTRAINT unique_email UNIQUE (email);

ALTER TABLE employees
ADD CONSTRAINT positive_salary CHECK (salary > 0);
```

---

## 3. **Dropping Constraints**

Constraints can be dropped using the `ALTER TABLE` statement:

```sql
ALTER TABLE employees
DROP CONSTRAINT unique_email;
```

---

## 4. **Enforcing Constraints**

- Constraints are enforced by PostgreSQL whenever data is inserted, updated, or deleted.
- If a constraint is violated, PostgreSQL raises an error and rejects the operation.

---

## 5. **Examples of Constraints**

### **Primary Key**

```sql
CREATE TABLE students (
    student_id SERIAL PRIMARY KEY,
    name TEXT NOT NULL
);
```

### **Foreign Key**

```sql
CREATE TABLE orders (
    order_id SERIAL PRIMARY KEY,
    product_id INT REFERENCES products(product_id),
    quantity INT
);
```

### **Unique**

```sql
CREATE TABLE users (
    user_id SERIAL PRIMARY KEY,
    username TEXT UNIQUE
);
```

### **Not Null**

```sql
CREATE TABLE employees (
    id SERIAL PRIMARY KEY,
    name TEXT NOT NULL
);
```

### **Check**

```sql
CREATE TABLE employees (
    id SERIAL PRIMARY KEY,
    age INT CHECK (age >= 18)
);
```

### **Exclusion**

```sql
CREATE TABLE room_reservations (
    room INT,
    during TSRANGE,
    EXCLUDE USING GIST (room WITH =, during WITH &&)
);
```

---

## 6. **Key Points to Remember**

- Constraints ensure data integrity and consistency in a relational database.
- PostgreSQL supports primary key, foreign key, unique, not null, check, and exclusion constraints.
- Constraints can be added during table creation or later using `ALTER TABLE`.
- Violations of constraints result in errors and rejection of the operation.
