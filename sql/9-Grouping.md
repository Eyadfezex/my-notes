# Grouping in SQL

Grouping in SQL is used to organize rows into groups based on one or more columns. It’s often used with aggregate functions like `COUNT`, `SUM`, `AVG`, `MIN`, and `MAX` to calculate values for each group. Below are examples of grouping queries along with their expected responses.

---

## Example 1: Count Employees in Each Department

**Query**:

```sql
SELECT department, COUNT(*) AS employee_count
FROM employees
GROUP BY department;
```

**Response**:

| department  | employee_count |
| ----------- | -------------- |
| HR          | 5              |
| Engineering | 10             |
| Sales       | 8              |

- Groups rows by `department`.
- Counts the number of employees in each group.

---

## Example 2: Calculate Average Salary by Department

**Query**:

```sql
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department;
```

**Response**:

| department  | avg_salary |
| ----------- | ---------- |
| HR          | 50000      |
| Engineering | 75000      |
| Sales       | 60000      |

- Groups rows by `department`.
- Calculates the average salary for each group.

---

## Example 3: Find Total Sales by Year

**Query**:

```sql
SELECT YEAR(order_date) AS order_year, SUM(sales_amount) AS total_sales
FROM orders
GROUP BY YEAR(order_date);
```

**Response**:

| order_year | total_sales |
| ---------- | ----------- |
| 2022       | 100000      |
| 2023       | 150000      |

- Groups rows by the year extracted from `order_date`.
- Sums the `sales_amount` for each year.

---

## Example 4: Group by Multiple Columns

**Query**:

```sql
SELECT region, product_id, COUNT(*) AS order_count
FROM orders
GROUP BY region, product_id;
```

**Response**:

| region | product_id | order_count |
| ------ | ---------- | ----------- |
| North  | 101        | 20          |
| North  | 102        | 15          |
| South  | 101        | 10          |

- Groups rows by both `region` and `product_id`.
- Counts the number of orders for each combination.

---

## Filtering Groups with `HAVING`

The `HAVING` clause is used to filter groups after they are created. It’s like `WHERE`, but for groups.

### Example: Find Departments with More Than 5 Employees

**Query**:

```sql
SELECT department, COUNT(*) AS employee_count
FROM employees
GROUP BY department
HAVING COUNT(*) > 5;
```

**Response**:

| department  | employee_count |
| ----------- | -------------- |
| Engineering | 10             |
| Sales       | 8              |

- Groups rows by `department`.
- Filters groups to show only those with more than 5 employees.

---

## Grouping with Aggregate Functions

You can use multiple aggregate functions in the same query.

### Example: Calculate Total and Average Salary by Department

**Query**:

```sql
SELECT department, SUM(salary) AS total_salary, AVG(salary) AS avg_salary
FROM employees
GROUP BY department;
```

**Response**:

| department  | total_salary | avg_salary |
| ----------- | ------------ | ---------- |
| HR          | 250000       | 50000      |
| Engineering | 750000       | 75000      |
| Sales       | 480000       | 60000      |

- Groups rows by `department`.
- Calculates both the total and average salary for each group.

---

## Grouping vs Distinct

| Feature                 | Grouping                       | Distinct                               |
| ----------------------- | ------------------------------ | -------------------------------------- |
| **Purpose**             | Summarize data by groups       | Remove duplicate rows                  |
| **Aggregate Functions** | Works with aggregate functions | Does not work with aggregate functions |
| **Use Case**            | Grouping and summarizing data  | Removing duplicates                    |

---

## Common Mistakes with Grouping

1. **Forgetting `GROUP BY`**: If you use an aggregate function without `GROUP BY`, it will treat the entire table as one group.
2. **Incorrect Columns in `SELECT`**: All columns in the `SELECT` clause must either be in the `GROUP BY` clause or used with an aggregate function.
3. **Confusing `WHERE` and `HAVING`**: Use `WHERE` to filter rows before grouping and `HAVING` to filter groups after grouping.

---

## Example: Correct vs Incorrect Grouping

### Correct

**Query**:

```sql
SELECT department, COUNT(*) AS employee_count
FROM employees
GROUP BY department;
```

**Response**:

| department  | employee_count |
| ----------- | -------------- |
| HR          | 5              |
| Engineering | 10             |
| Sales       | 8              |

### Incorrect (Missing `GROUP BY`)

**Query**:

```sql
SELECT department, COUNT(*) AS employee_count
FROM employees;
```

**Response**:

| department | employee_count |
| ---------- | -------------- |
| HR         | 23             |

- Treats the entire table as one group.

### Incorrect (Invalid Column in `SELECT`)

**Query**:

```sql
SELECT department, name, COUNT(*) AS employee_count
FROM employees
GROUP BY department;
```

**Response**:

- Error: Column `name` must appear in the `GROUP BY` clause or be used in an aggregate function.

---

## Performance Tips

- **Index Columns**: Index the columns used in `GROUP BY` for faster grouping.
- **Limit Group Size**: Use `HAVING` to filter out unnecessary groups.
- **Avoid Over-Grouping**: Only group by the columns you need.

---

Grouping is a powerful feature in SQL for summarizing and analyzing data. By using `GROUP BY` and aggregate functions, you can easily break down your data into meaningful groups and calculate useful statistics.
