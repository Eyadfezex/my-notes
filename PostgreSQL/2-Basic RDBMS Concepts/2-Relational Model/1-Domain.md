# Domain in the Relational Model

In the relational model, a **domain** defines the set of valid values that an attribute (column) can take. It is a fundamental concept that ensures data integrity and consistency in a database.

---

## Key Points About Domain

1. **Definition**:

   - A domain specifies the **type of data** that can be stored in an attribute.
   - It also defines the **range of valid values** for that attribute.

2. **Examples of Domains**:

   - `INTEGER`: All whole numbers (e.g., `1`, `2`, `3`).
   - `STRING`: A sequence of characters (e.g., `"John"`, `"Doe"`).
   - `DATE`: A valid date (e.g., `2023-10-15`).
   - `BOOLEAN`: `TRUE` or `FALSE`.

3. **Domain Constraints**:

   - Domains enforce constraints to ensure that only valid data is stored in an attribute.
   - Example: An `Age` attribute might have a domain of positive integers between `0` and `120`.

4. **User-Defined Domains**:
   - Databases allow the creation of custom domains to enforce specific rules.
   - Example: A domain `EMAIL` could be defined to store only valid email addresses.

---

## Importance of Domains

1. **Data Integrity**:

   - Ensures that only valid and consistent data is stored in the database.

2. **Error Prevention**:

   - Prevents invalid data from being inserted into the database.

3. **Clarity**:
   - Makes the database schema more understandable by explicitly defining what kind of data is expected.

---

## Example of Domains in a Table

Consider a `Students` table:

| StudentID | Name     | Age | Email                |
| --------- | -------- | --- | -------------------- |
| 1         | John Doe | 21  | john.doe@example.com |
| 2         | Jane Doe | 22  | jane.doe@example.com |

### Domains for Each Attribute:

- **`StudentID`**: `INTEGER` (positive integers).
- **`Name`**: `STRING` (alphanumeric characters).
- **`Age`**: `INTEGER` (values between `0` and `120`).
- **`Email`**: `STRING` (valid email format).

---

## Domain vs. Data Type

- **Data Type**: Specifies the kind of data (e.g., integer, string, date).
- **Domain**: Specifies the data type **and** the range of valid values.

### Example:

- Data Type: `INTEGER`.
- Domain: `INTEGER` with values between `0` and `120`.

---

## Creating a Domain in PostgreSQL

PostgreSQL allows you to create custom domains using the `CREATE DOMAIN` statement. This is useful for enforcing specific constraints across multiple columns or tables.

### Syntax:

```sql
CREATE DOMAIN domain_name AS data_type
  [DEFAULT default_value]
  [CONSTRAINT constraint_name CHECK (condition)];
```

### Example 1: Creating a Domain for Age

```sql
CREATE DOMAIN age_domain AS INTEGER
  CHECK (VALUE >= 0 AND VALUE <= 120);
```

### Example 2: Creating a Domain for Email

```sql
CREATE DOMAIN email_domain AS TEXT
  CHECK (VALUE ~ '^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\\.[A-Za-z]{2,}$');
```

### Using the Domain in a Table

Once a domain is created, you can use it as a column type in a table:

```sql
CREATE TABLE Students (
  StudentID SERIAL PRIMARY KEY,
  Name TEXT NOT NULL,
  Age age_domain,
  Email email_domain
);
```

---

## Summary

- A domain defines the valid values for an attribute in a relational database.
- It ensures data integrity, prevents errors, and improves clarity.
- Domains can be predefined (e.g., `INTEGER`, `STRING`) or user-defined (e.g., `EMAIL`).
- In PostgreSQL, you can create custom domains using the `CREATE DOMAIN` statement.

For more details, refer to the [GeeksforGeeks Article on the Relational Model](https://www.geeksforgeeks.org/relational-model-in-dbms/).
