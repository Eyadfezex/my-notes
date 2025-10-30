# Set Operations in PostgreSQL

Set operations in PostgreSQL are used to combine or compare the results of two or more `SELECT` queries. These operations are essential for manipulating and analyzing data in relational databases. PostgreSQL supports the following set operations:

1. **UNION**
2. **UNION ALL**
3. **INTERSECT**
4. **EXCEPT**

---

## 1. **UNION**

The `UNION` operation combines the results of two or more `SELECT` queries into a single result set. It removes duplicate rows from the combined result.

### Syntax:

```sql
SELECT column1, column2, ...
FROM table1
UNION
SELECT column1, column2, ...
FROM table2;
```

### Example:

```sql
SELECT name FROM employees
UNION
SELECT name FROM contractors;
```

#### Response:

Assume the `employees` table contains:

| name    |
| ------- |
| Alice   |
| Bob     |
| Charlie |

And the `contractors` table contains:

| name  |
| ----- |
| Bob   |
| David |
| Alice |

The query will return:

| name    |
| ------- |
| Alice   |
| Bob     |
| Charlie |
| David   |

**Explanation**: Duplicate names (`Alice` and `Bob`) are removed, and the result contains unique names from both tables.

---

## 2. **UNION ALL**

The `UNION ALL` operation is similar to `UNION`, but it does **not remove duplicates**. It combines all rows from the queries, including duplicates.

### Syntax:

```sql
SELECT column1, column2, ...
FROM table1
UNION ALL
SELECT column1, column2, ...
FROM table2;
```

### Example:

```sql
SELECT name FROM employees
UNION ALL
SELECT name FROM contractors;
```

#### Response:

Using the same data as above:

- `employees` table:

  | name    |
  | ------- |
  | Alice   |
  | Bob     |
  | Charlie |

- `contractors` table:

  | name  |
  | ----- |
  | Bob   |
  | David |
  | Alice |

The query will return:

| name    |
| ------- |
| Alice   |
| Bob     |
| Charlie |
| Bob     |
| David   |
| Alice   |

**Explanation**: All names are included, even duplicates (`Alice` and `Bob` appear twice).

---

## 3. **INTERSECT**

The `INTERSECT` operation returns only the rows that are **common to both `SELECT` queries**. It finds the intersection of the two result sets.

### Syntax:

```sql
SELECT column1, column2, ...
FROM table1
INTERSECT
SELECT column1, column2, ...
FROM table2;
```

### Example:

```sql
SELECT name FROM employees
INTERSECT
SELECT name FROM contractors;
```

#### Response:

Using the same data:

- `employees` table:

  | name    |
  | ------- |
  | Alice   |
  | Bob     |
  | Charlie |

- `contractors` table:

  | name  |
  | ----- |
  | Bob   |
  | David |
  | Alice |

The query will return:

| name  |
| ----- |
| Alice |
| Bob   |

**Explanation**: Only the names that appear in both tables (`Alice` and `Bob`) are returned.

---

## 4. **EXCEPT**

The `EXCEPT` operation returns rows from the first `SELECT` query that are **not present** in the second `SELECT` query. It finds the difference between two result sets.

### Syntax:

```sql
SELECT column1, column2, ...
FROM table1
EXCEPT
SELECT column1, column2, ...
FROM table2;
```

### Example:

```sql
SELECT name FROM employees
EXCEPT
SELECT name FROM contractors;
```

#### Response:

Using the same data:

- `employees` table:

  | name    |
  | ------- |
  | Alice   |
  | Bob     |
  | Charlie |

- `contractors` table:

  | name  |
  | ----- |
  | Bob   |
  | David |
  | Alice |

The query will return:

| name    |
| ------- |
| Charlie |

**Explanation**: Only the name `Charlie` is returned because it is in the `employees` table but not in the `contractors` table.

---

## Example with `ORDER BY`

To sort the final result, use an `ORDER BY` clause at the end of the set operation.

### Example:

```sql
SELECT name FROM employees
UNION
SELECT name FROM contractors
ORDER BY name;
```

#### Response:

Using the same data:

- `employees` table:

  | name    |
  | ------- |
  | Alice   |
  | Bob     |
  | Charlie |

- `contractors` table:

  | name  |
  | ----- |
  | Bob   |
  | David |
  | Alice |

The query will return:

| name    |
| ------- |
| Alice   |
| Bob     |
| Charlie |
| David   |

**Explanation**: The result is sorted alphabetically by the `name` column.

---

## Practical Use Cases

- Combining data from multiple tables with similar structures.
- Finding common or unique records between tables.
- Aggregating results from different queries for reporting or analysis.

By mastering these set operations, you can efficiently manipulate and analyze data in PostgreSQL.
