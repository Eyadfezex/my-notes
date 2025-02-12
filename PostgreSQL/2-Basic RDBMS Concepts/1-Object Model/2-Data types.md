# PostgreSQL Data Types: An Introduction

PostgreSQL is a powerful relational database that supports a wide range of data types. These data types help define the kind of data that can be stored in a column and how it can be manipulated.

---

## Categories of PostgreSQL Data Types

### 1. **Numeric Types**

- Used for storing numbers.
- Examples:
  - `SMALLINT`: 2-byte integer.
  - `INTEGER`: 4-byte integer.
  - `BIGINT`: 8-byte integer.
  - `DECIMAL` or `NUMERIC`: Exact precision numbers.
  - `REAL`: 4-byte floating-point number.
  - `DOUBLE PRECISION`: 8-byte floating-point number.

### 2. **Character Types**

- Used for storing text data.
- Examples:
  - `CHAR(n)`: Fixed-length character string.
  - `VARCHAR(n)`: Variable-length character string with a limit.
  - `TEXT`: Variable-length string without a limit.

### 3. **Date/Time Types**

- Used for storing dates, times, and intervals.
- Examples:
  - `DATE`: Stores a date (year, month, day).
  - `TIME`: Stores a time of day.
  - `TIMESTAMP`: Stores both date and time.
  - `INTERVAL`: Stores a time interval.

### 4. **Boolean Type**

- Used for storing true/false values.
- Example:
  - `BOOLEAN`: Can be `TRUE`, `FALSE`, or `NULL`.

### 5. **Binary Data Types**

- Used for storing binary data.
- Examples:
  - `BYTEA`: Stores binary strings (e.g., images, files).

### 6. **Geometric Types**

- Used for storing geometric shapes.
- Examples:
  - `POINT`: A geometric point.
  - `LINE`: A straight line.
  - `POLYGON`: A closed geometric shape.

### 7. **Network Address Types**

- Used for storing IP addresses and MAC addresses.
- Examples:
  - `INET`: Stores an IPv4 or IPv6 address.
  - `CIDR`: Stores an IP network address.
  - `MACADDR`: Stores a MAC address.

### 8. **JSON and JSONB Types**

- Used for storing JSON data.
- Examples:
  - `JSON`: Stores JSON data as plain text.
  - `JSONB`: Stores JSON data in a binary format (more efficient for querying).

### 9. **Array Types**

- Used for storing arrays of any data type.
- Example:
  - `INTEGER[]`: An array of integers.

### 10. **Composite Types**

- Used for defining custom data types.
- Example:
  - `CREATE TYPE person AS (name TEXT, age INTEGER);`

### 11. **Range Types**

- Used for storing a range of values.
- Examples:
  - `INT4RANGE`: A range of integers.
  - `DATERANGE`: A range of dates.

### 12. **UUID Type**

- Used for storing universally unique identifiers.
- Example:
  - `UUID`: Stores a 128-bit UUID.

### 13. **Special Types**

- Used for specific use cases.
- Examples:
  - `MONEY`: Stores currency amounts.
  - `XML`: Stores XML data.

---

## Choosing the Right Data Type

- **Precision**: Use data types that match the precision required (e.g., `DECIMAL` for exact values).
- **Storage Efficiency**: Choose data types that minimize storage (e.g., `SMALLINT` instead of `INTEGER` if values are small).
- **Functionality**: Use specialized types (e.g., `JSONB` for JSON data, `UUID` for unique identifiers).

---

## Example Table with Data Types

```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    is_active BOOLEAN DEFAULT TRUE,
    metadata JSONB
);
```

---

## Key Takeaways

- PostgreSQL provides a rich set of data types to handle various kinds of data.
- Choosing the right data type ensures efficient storage and querying.
- Specialized types like `JSONB`, `UUID`, and `ARRAY` make PostgreSQL versatile for modern applications.

---

For more details, refer to the [Prisma Data Guide on PostgreSQL Data Types](https://www.prisma.io/dataguide/postgresql/introduction-to-data-types).
