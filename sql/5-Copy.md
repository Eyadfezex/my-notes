# SQL `COPY` Command

The `COPY` command in SQL (primarily used in **PostgreSQL**) is a powerful tool for importing and exporting data between a database table and a file. It’s commonly used for bulk data operations, such as loading data from a CSV file or exporting data to a file.

---

## Why Use the `COPY` Command?

- **Efficient Data Transfer**: Quickly import or export large amounts of data.
- **File Support**: Works with CSV, TEXT, and BINARY formats.
- **Flexibility**: Can handle headers, delimiters, and other file-specific options.

---

## Basic Syntax

### Importing Data into a Table

```sql
COPY table_name (column1, column2, ...)
FROM 'file_path'
WITH (FORMAT csv, HEADER true);
```

- `table_name`: The table where data will be imported.
- `file_path`: The path to the file containing the data.
- `FORMAT csv`: Specifies the file format (e.g., CSV, TEXT, BINARY).
- `HEADER true`: Indicates the first row contains column names.

### Exporting Data to a File

```sql
COPY table_name TO 'file_path' WITH (FORMAT csv, HEADER true);
```

- `table_name`: The table from which data will be exported.
- `file_path`: The path where the file will be saved.

---

## Example 1: Import Data from a CSV File

**Query**:

```sql
COPY students FROM '/path/to/students.csv' WITH (FORMAT csv, HEADER true);
```

**File (`students.csv`)**:

```csv
id,name,age
1,Alice,20
2,Bob,22
3,Charlie,21
```

**Result**:

- The `students` table will now contain the following data:

| id  | name    | age |
| --- | ------- | --- |
| 1   | Alice   | 20  |
| 2   | Bob     | 22  |
| 3   | Charlie | 21  |

---

## Example 2: Export Data to a CSV File

**Query**:

```sql
COPY students TO '/path/to/output.csv' WITH (FORMAT csv, HEADER true);
```

**Result**:

- A file named `output.csv` will be created with the following content:

```csv
id,name,age
1,Alice,20
2,Bob,22
3,Charlie,21
```

---

## Key Points

1. **PostgreSQL-Specific**: The `COPY` command is primarily used in PostgreSQL and is not part of standard SQL.
2. **File Permissions**: Ensure the database server has read/write access to the file.
3. **Superuser Requirement**:
   - Only superusers can use `COPY` with file paths.
   - Non-superusers must use `\COPY`, which works with client-side files.
4. **Supported Formats**: CSV, TEXT, and BINARY.

---

## Alternative: `\COPY` for Non-Superusers

If you’re not a superuser, use `\COPY` in the PostgreSQL client (`psql`):

### Example: Import Data Using `\COPY`

**Query**:

```sql
\COPY students FROM 'students.csv' CSV HEADER;
```

- This command imports data from a client-side file (`students.csv`) into the `students` table.

### Example: Export Data Using `\COPY`

**Query**:

```sql
\COPY students TO 'output.csv' CSV HEADER;
```

- This command exports data from the `students` table to a client-side file (`output.csv`).

---

## Common Options for `COPY`

| Option          | Description                                                             |
| --------------- | ----------------------------------------------------------------------- |
| `FORMAT csv`    | Specifies the file format as CSV.                                       |
| `HEADER true`   | Indicates the file has a header row (for CSV files).                    |
| `DELIMITER ','` | Specifies the delimiter used in the file (default is comma for CSV).    |
| `NULL 'null'`   | Specifies how NULL values are represented in the file.                  |
| `QUOTE '"'`     | Specifies the quote character for CSV files (default is double quotes). |

---

## Example 3: Import Data with Custom Delimiter

**Query**:

```sql
COPY students FROM '/path/to/students.txt' WITH (FORMAT csv, DELIMITER '|', HEADER true);
```

**File (`students.txt`)**:

```text
id|name|age
1|Alice|20
2|Bob|22
3|Charlie|21
```

**Result**:

- The `students` table will contain the same data as in Example 1.

---

## Example 4: Export Data with NULL Values

**Query**:

```sql
COPY students TO '/path/to/output.csv' WITH (FORMAT csv, HEADER true, NULL 'NULL');
```

**Result**:

- If the `students` table contains NULL values, they will be represented as `NULL` in the output file.

---

## Performance Tips

- **Bulk Operations**: Use `COPY` for bulk data loading or exporting to improve performance.
- **Indexes**: Consider dropping indexes before bulk imports and recreating them afterward for faster loading.
- **File Format**: Use CSV for text-based data and BINARY for faster, more compact storage.

---

The `COPY` command is a versatile tool for efficiently moving data between PostgreSQL tables and files. By mastering its syntax and options, you can streamline data import/export tasks in your database workflows.
