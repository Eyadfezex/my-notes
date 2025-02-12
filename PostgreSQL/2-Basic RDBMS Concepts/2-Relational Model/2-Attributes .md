# Attributes in the Relational Model

In the relational model, **attributes** are the properties or characteristics that define the columns of a table. They describe the type of data stored in each column and play a key role in structuring and organizing data in a database.

---

## Key Concepts

### 1. **Definition**

- An attribute is a named column in a table.
- It represents a specific property of the entity described by the table.
- Example: In a `Students` table, attributes could include `StudentID`, `Name`, `Age`, and `Email`.

### 2. **Types of Attributes**

Attributes can be categorized based on their characteristics:

1. **Simple vs. Composite**:

   - **Simple Attribute**: Cannot be divided further (e.g., `Age`, `StudentID`).
   - **Composite Attribute**: Can be divided into smaller sub-parts (e.g., `Name` can be split into `FirstName` and `LastName`).

2. **Single-Valued vs. Multi-Valued**:

   - **Single-Valued Attribute**: Holds a single value (e.g., `Age`).
   - **Multi-Valued Attribute**: Can hold multiple values (e.g., `PhoneNumbers`).

3. **Derived Attribute**:

   - An attribute whose value is derived from another attribute (e.g., `Age` can be derived from `DateOfBirth`).

4. **Key Attribute**:
   - An attribute that uniquely identifies a tuple (row) in a table (e.g., `StudentID`).

---

## Properties of Attributes

1. **Name**:

   - Each attribute has a unique name within a table.

2. **Data Type**:

   - Specifies the kind of data the attribute can hold (e.g., `INTEGER`, `STRING`, `DATE`).

3. **Domain**:

   - Defines the set of valid values for the attribute (e.g., `Age` must be a positive integer).

4. **Nullability**:
   - Specifies whether the attribute can have `NULL` values.

---

## Example of Attributes in a Table

Consider a `Students` table:

| StudentID | Name     | Age | Email                |
| --------- | -------- | --- | -------------------- |
| 1         | John Doe | 21  | john.doe@example.com |
| 2         | Jane Doe | 22  | jane.doe@example.com |

### Attributes:

- **`StudentID`**: A key attribute (unique identifier).
- **`Name`**: A composite attribute (can be split into `FirstName` and `LastName`).
- **`Age`**: A simple, single-valued attribute.
- **`Email`**: A simple, single-valued attribute.

---

## Creating Attributes in a Table (PostgreSQL)

To create attributes in a table, you use the `CREATE TABLE` statement in SQL. Here's how you can define attributes with their data types and constraints:

### Syntax:

```sql
CREATE TABLE table_name (
  column1_name data_type [constraints],
  column2_name data_type [constraints],
  ...
);
```

### Example: Creating a `Students` Table

```sql
CREATE TABLE Students (
  StudentID SERIAL PRIMARY KEY,       -- Unique identifier (key attribute)
  FirstName TEXT NOT NULL,            -- Simple attribute
  LastName TEXT NOT NULL,             -- Simple attribute
  Age INT CHECK (Age >= 0 AND Age <= 120),  -- Simple attribute with domain constraint
  Email TEXT UNIQUE NOT NULL          -- Simple attribute with uniqueness constraint
);
```

### Explanation:

- **`StudentID`**: A key attribute with `SERIAL` data type (auto-incremented integer) and `PRIMARY KEY` constraint.
- **`FirstName`** and **`LastName`**: Simple attributes of type `TEXT` with `NOT NULL` constraints.
- **`Age`**: A simple attribute with a domain constraint (`CHECK`) to ensure values are between `0` and `120`.
- **`Email`**: A simple attribute with `UNIQUE` and `NOT NULL` constraints.

---

## Adding Attributes to an Existing Table

You can add new attributes to an existing table using the `ALTER TABLE` statement:

### Syntax:

```sql
ALTER TABLE table_name
ADD COLUMN column_name data_type [constraints];
```

### Example: Adding a `DateOfBirth` Attribute

```sql
ALTER TABLE Students
ADD COLUMN DateOfBirth DATE;
```

---

## Modifying Attributes

You can modify existing attributes (e.g., change data type or constraints) using the `ALTER TABLE` statement:

### Syntax:

```sql
ALTER TABLE table_name
ALTER COLUMN column_name SET DATA TYPE new_data_type;
```

### Example: Changing the `Age` Attribute to `SMALLINT`

```sql
ALTER TABLE Students
ALTER COLUMN Age SET DATA TYPE SMALLINT;
```

---

## Summary

- Attributes are the columns in a table that define the properties of an entity.
- They can be simple, composite, single-valued, multi-valued, derived, or key attributes.
- Attributes ensure data integrity, organization, and efficiency in a relational database.
- In PostgreSQL, you can create, add, and modify attributes using `CREATE TABLE`, `ALTER TABLE`, and `ALTER COLUMN`.

For more details, refer to the [Guru99 Article on the Relational Model](https://www.guru99.com/relational-data-model-dbms.html).
