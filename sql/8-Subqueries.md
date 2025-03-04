# Subqueries in SQL

A **subquery** is a query inside another query. It’s like a mini-query that helps you solve a smaller part of a bigger problem. Subqueries can be used in `SELECT`, `FROM`, `WHERE`, and `HAVING` clauses. Below are examples of subqueries along with their expected responses.

---

## Example 1: Scalar Subquery (Single Value)

**Query**:

```sql
SELECT name, salary
FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```

**Response**:

| name  | salary |
| ----- | ------ |
| Alice | 90000  |
| Bob   | 85000  |

- The subquery `(SELECT AVG(salary) FROM employees)` calculates the average salary (e.g., 75000).
- The main query filters employees earning more than the average.

---

## Example 2: Column Subquery (List of Values)

**Query**:

```sql
SELECT name, department
FROM employees
WHERE department IN (SELECT department FROM employees WHERE name = 'John');
```

**Response**:

| name  | department |
| ----- | ---------- |
| John  | Sales      |
| Alice | Sales      |
| Bob   | Sales      |

- The subquery `(SELECT department FROM employees WHERE name = 'John')` returns the department(s) where John works (e.g., `Sales`).
- The main query finds all employees in the same department.

---

## Example 3: Table Subquery (Full Table)

**Query**:

```sql
SELECT name, salary
FROM (SELECT name, salary FROM employees ORDER BY salary DESC LIMIT 3) AS top_employees;
```

**Response**:

| name    | salary |
| ------- | ------ |
| Alice   | 90000  |
| Bob     | 85000  |
| Charlie | 80000  |

- The subquery `(SELECT name, salary FROM employees ORDER BY salary DESC LIMIT 3)` returns the top 3 highest-paid employees.
- The main query selects from this result.

---

## Example 4: Subquery in `FROM` Clause

**Query**:

```sql
SELECT department, avg_salary
FROM (SELECT department, AVG(salary) AS avg_salary
      FROM employees
      GROUP BY department) AS dept_avg
WHERE avg_salary > 50000;
```

**Response**:

| department  | avg_salary |
| ----------- | ---------- |
| Engineering | 75000      |
| Sales       | 60000      |

- The subquery calculates the average salary for each department.
- The main query filters departments where the average salary is greater than $50,000.

---

## Example 5: Subquery in `HAVING` Clause

**Query**:

```sql
SELECT department, COUNT(*) AS employee_count
FROM employees
GROUP BY department
HAVING COUNT(*) > (SELECT 5);
```

**Response**:

| department  | employee_count |
| ----------- | -------------- |
| Engineering | 10             |
| Sales       | 8              |

- The subquery `(SELECT 5)` returns the number 5.
- The `HAVING` clause filters departments with more than 5 employees.

---

## Correlated Subqueries

A **correlated subquery** is a subquery that references a column from the outer query. It runs once for each row in the outer query.

### Example: Find Employees Earning More Than Their Department Average

**Query**:

```sql
SELECT name, salary, department
FROM employees e
WHERE salary > (SELECT AVG(salary)
                FROM employees
                WHERE department = e.department);
```

**Response**:

| name  | salary | department  |
| ----- | ------ | ----------- |
| Alice | 90000  | Engineering |
| Bob   | 85000  | Engineering |

- The subquery calculates the average salary for the current employee’s department.
- The main query compares each employee’s salary to their department’s average.

---

## Subqueries vs Joins

| Feature         | Subquery                         | Join                                |
| --------------- | -------------------------------- | ----------------------------------- |
| **Use Case**    | Dynamic filtering, calculations  | Combining data from multiple tables |
| **Performance** | Can be slower for large datasets | Often faster for large datasets     |
| **Readability** | Can make queries harder to read  | Easier to read for simple joins     |

---

## When to Use Subqueries

1. **Filtering**: When you need to filter data based on dynamic conditions.
2. **Calculations**: When you need to calculate values (e.g., averages, totals) for use in the main query.
3. **Breaking Down Problems**: When you want to solve a smaller problem first and use the result in a bigger query.

---

## Performance Tips

- **Avoid Nested Subqueries**: Too many nested subqueries can slow down your query.
- **Use Indexes**: Make sure the subquery can use indexes for faster execution.
- **Test and Optimize**: Always check the performance of your queries.
