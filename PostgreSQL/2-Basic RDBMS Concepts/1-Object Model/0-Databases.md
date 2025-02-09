# Databases in PostgreSQL

## Overview

In PostgreSQL, a **database** is a named collection of database objects, such as:

- **Tables**: Store structured data.
- **Indexes**: Improve query performance.
- **Views**: Provide virtual tables based on SQL queries.
- **Stored Procedures**: Encapsulate reusable logic.
- **Other Objects**: Sequences, triggers, functions, etc.

Each PostgreSQL server can manage **multiple databases**, allowing for the separation and organization of data sets for different applications, projects, or users.

---

## Key Features of PostgreSQL Databases

1. **Separation of Data**:

   - Databases are isolated from each other, ensuring that data for one application or project does not interfere with another.
   - Example: A single PostgreSQL server can host separate databases for `app1`, `app2`, and `analytics`.

2. **Access Control**:

   - PostgreSQL provides granular permissions for databases, allowing administrators to control who can access or modify specific databases.

3. **Scalability**:

   - Multiple databases can be managed on a single server, making it easier to scale and organize data for large systems.

4. **Backup and Recovery**:
   - Databases can be backed up and restored individually, simplifying maintenance and disaster recovery.

---

## Creating a Database in PostgreSQL

To create a new database, use the `CREATE DATABASE` SQL command:

```sql
CREATE DATABASE my_database;
```

### Optional Parameters

- **Owner**: Specify the user who owns the database.

  ```sql
  CREATE DATABASE my_database OWNER my_user;

  ```

- **Template**: Create a database using a template (e.g., `template0` or `template1`).

  ```sql
  CREATE DATABASE my_database TEMPLATE template0;

  ```

- **Encoding**: Set the character encoding for the database.

  ```sql
  CREATE DATABASE my_database ENCODING 'UTF8';

  ```

---

## Managing Databases

PostgreSQL provides several commands and tools for managing databases:

1. **List Databases**:

   - Use the `\l` command in the `psql` CLI or the following SQL query:

     ```sql
     SELECT datname FROM pg_database;

     ```

2. **Switch Databases**:

   - Use the `\c` command in the `psql` CLI:

     ```sql
     \c my_database

     ```

3. **Drop a Database**:

   - Use the `DROP DATABASE` command:

     ```sql
     DROP DATABASE my_database;

     ```

4. **Backup a Database**:

   - Use the `pg_dump` utility:

     ```bash
     pg_dump my_database > my_database_backup.sql

     ```

5. **Restore a Database**:

   - Use the `psql` utility:

     - ```bash

       psql my_database < my_database_backup.sql

       ```

## References

- [PostgreSQL Documentation on Databases](https://www.postgresql.org/docs/current/managing-databases.html)
- PostgreSQL: Up and Running by Regina Obe and Leo Hsu
