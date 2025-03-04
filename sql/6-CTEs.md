# Common Table Expressions (CTEs)

Common Table Expressions (CTEs) are a powerful feature in SQL that allow you to define temporary result sets. These result sets can be referenced within a `SELECT`, `INSERT`, `UPDATE`, or `DELETE` statement. CTEs are defined using the `WITH` clause and improve the readability and modularity of complex queries.

---

## Basic Syntax

```sql
WITH cte_name AS (
    -- CTE query definition
    SELECT column1, column2, ...
    FROM table_name
    WHERE condition
)
-- Main query that uses the CTE
SELECT *
FROM cte_name;
```

---

## Key Features of CTEs

1. **Readability**: Breaks down complex queries into simpler, more manageable parts.
2. **Reusability**: A CTE can be referenced multiple times within the same query.
3. **Recursion**: Enables recursive queries, which are useful for hierarchical data (e.g., organizational charts, tree structures).

---

## Example 1: Simple CTE

```sql
WITH Sales_CTE AS (
    SELECT SalesPersonID, SUM(SalesAmount) AS TotalSales
    FROM Sales
    GROUP BY SalesPersonID
)
SELECT SalesPersonID, TotalSales
FROM Sales_CTE
WHERE TotalSales > 100000;
```

- This CTE calculates the total sales for each salesperson and filters the results to show only those with total sales greater than 100,000.

---

## Example 2: Recursive CTE

```sql
WITH Recursive_CTE AS (
    -- Anchor member
    SELECT EmployeeID, ManagerID, EmployeeName
    FROM Employees
    WHERE ManagerID IS NULL
    UNION ALL
    -- Recursive member
    SELECT e.EmployeeID, e.ManagerID, e.EmployeeName
    FROM Employees e
    INNER JOIN Recursive_CTE r ON e.ManagerID = r.EmployeeID
)
SELECT *
FROM Recursive_CTE;
```

- This recursive CTE retrieves a hierarchy of employees and their managers. The anchor member starts with top-level managers (those with no manager), and the recursive member joins the CTE with itself to find subordinates.

---

## Example 3: Multiple CTEs

```sql
WITH CTE1 AS (
    SELECT ProductID, SUM(Quantity) AS TotalQuantity
    FROM OrderDetails
    GROUP BY ProductID
),
CTE2 AS (
    SELECT ProductID, TotalQuantity
    FROM CTE1
    WHERE TotalQuantity > 50
)
SELECT p.ProductName, c.TotalQuantity
FROM Products p
JOIN CTE2 c ON p.ProductID = c.ProductID;
```

- This query uses two CTEs:
  - `CTE1` calculates the total quantity of each product sold.
  - `CTE2` filters products with a total quantity greater than 50.
- The final query joins `CTE2` with the `Products` table to get product names.

---

## Advantages of CTEs

- **Modularity**: Breaks down complex logic into smaller, reusable parts.
- **Readability**: Improves query readability by separating logic into named blocks.
- **Recursion**: Enables recursive queries for hierarchical data.

---

## Limitations of CTEs

- **Scope**: CTEs are only available within the scope of the query in which they are defined.
- **Performance**: CTEs are not always optimized by the query planner, so performance may vary compared to subqueries or temporary tables.
