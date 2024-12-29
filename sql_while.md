# Handbook: Key Concepts in T-SQL

This handbook explains fundamental concepts and syntax in Transact-SQL (T-SQL) for writing efficient and readable SQL queries. The topics covered here include `WHILE` loops, conditional logic with `IF`, setting variables, using derived tables, and Common Table Expressions (CTEs), along with the `WITH` and `AS` clauses.

## Table of Contents:
1. [WHILE Loops](#while-loops)
2. [IF Statements](#if-statements)
3. [Setting Variables](#setting-variables)
4. [Derived Tables](#derived-tables)
5. [WITH Clause](#with-clause)
6. [Common Table Expressions (CTEs)](#common-table-expressions-ctes)

---

## 1. WHILE Loops

### Overview:
The `WHILE` loop is used to repeatedly execute a set of statements as long as a specified condition evaluates to true. It is particularly useful when you need to iterate over data or perform repetitive tasks.

### Syntax:
```sql
WHILE condition
BEGIN
    -- SQL statements to execute repeatedly
END
```

### Example:
```sql
DECLARE @Counter INT = 1;

WHILE @Counter <= 5
BEGIN
    PRINT 'The counter is ' + CAST(@Counter AS VARCHAR);
    SET @Counter = @Counter + 1;
END
```

### Notes:
- The condition is evaluated before each iteration. If it's `FALSE` initially, the loop doesn't execute.
- Be careful with loops as they can easily result in infinite loops if the condition is never met.

---

## 2. IF Statements

### Overview:
The `IF` statement in T-SQL is used to execute a block of code conditionally. If the condition evaluates to true, the code inside the `IF` block is executed. Otherwise, it can optionally execute code inside an `ELSE` block.

### Syntax:
```sql
IF condition
BEGIN
    -- SQL statements if condition is true
END
ELSE
BEGIN
    -- SQL statements if condition is false
END
```

### Example:
```sql
DECLARE @Age INT = 18;

IF @Age >= 18
BEGIN
    PRINT 'You are an adult.';
END
ELSE
BEGIN
    PRINT 'You are a minor.';
END
```

### Notes:
- The condition is evaluated as a Boolean expression (`TRUE` or `FALSE`).
- You can also use `ELSE IF` to check multiple conditions.

---

## 3. Setting Variables

### Overview:
T-SQL allows you to define and assign values to variables for use within a query or block of SQL code. Variables are useful for storing intermediate results or states.

### Syntax:
```sql
DECLARE @VariableName DataType;
SET @VariableName = value;
```

### Example:
```sql
DECLARE @ProductName VARCHAR(100);
DECLARE @Price DECIMAL(10,2);

SET @ProductName = 'Laptop';
SET @Price = 999.99;

PRINT 'The product is ' + @ProductName + ' and its price is ' + CAST(@Price AS VARCHAR);
```

### Notes:
- Variables must be declared before they are used.
- The `SET` statement is used to assign values to variables.
- You can also initialize variables during declaration.

---

## 4. Derived Tables

### Overview:
A derived table is a temporary result set that you create within a `FROM` clause. This allows you to structure your query in a more flexible and modular way.

### Syntax:
```sql
SELECT columns
FROM (SELECT columns FROM table WHERE condition) AS DerivedTableAlias
WHERE condition;
```

### Example:
```sql
SELECT EmployeeName, Department
FROM (SELECT EmployeeName, Department, Salary FROM Employees WHERE Salary > 50000) AS HighEarners
WHERE Department = 'Sales';
```

### Notes:
- Derived tables are temporary and only exist for the duration of the query.
- They are commonly used for subqueries within the `FROM` clause.

---

## 5. WITH Clause

### Overview:
The `WITH` clause is used to define Common Table Expressions (CTEs), which can be referenced later in the query. It improves readability and modularity of complex queries.

### Syntax:
```sql
WITH CTEName AS
(
    -- Query that defines the CTE
    SELECT columns FROM table WHERE condition
)
SELECT columns FROM CTEName WHERE condition;
```

### Example:
```sql
WITH DepartmentCTE AS
(
    SELECT Department, COUNT(*) AS EmployeeCount
    FROM Employees
    GROUP BY Department
)
SELECT Department FROM DepartmentCTE WHERE EmployeeCount > 10;
```

### Notes:
- CTEs are temporary result sets that are available for the duration of a query.
- You can define multiple CTEs using commas.

---

## 6. Common Table Expressions (CTEs)

### Overview:
CTEs are used to simplify complex joins and subqueries by breaking them into modular components. CTEs are defined using the `WITH` clause and can reference each other within the same query.

### Syntax:
```sql
WITH CTEName AS
(
    -- Query definition
    SELECT columns FROM table WHERE condition
)
SELECT * FROM CTEName;
```

### Example:
```sql
WITH SalesData AS
(
    SELECT SalesPersonID, SUM(SalesAmount) AS TotalSales
    FROM Sales
    GROUP BY SalesPersonID
)
SELECT SalesPersonID FROM SalesData WHERE TotalSales > 10000;
```

### Notes:
- CTEs are only available within the `SELECT`, `INSERT`, `UPDATE`, or `DELETE` statement that immediately follows the `WITH` clause.
- You can use multiple CTEs in a single query, separated by commas.

---

## Conclusion

This handbook provides a brief overview of key features in T-SQL for writing effective SQL queries. Understanding and applying these concepts — `WHILE` loops, `IF` statements, setting variables, derived tables, the `WITH` clause, and CTEs — can help you structure SQL queries that are easier to write, maintain, and optimize. 

Each concept allows for greater flexibility and efficiency when working with SQL Server, and mastering these techniques will enhance your ability to work with large datasets and complex queries.
