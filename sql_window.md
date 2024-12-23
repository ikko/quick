### **Handbook for T-SQL Window Functions**

#### **Introduction**
T-SQL (Transact-SQL) window functions are a powerful feature in SQL Server that allow you to perform calculations across a set of rows related to the current row within a result set. These calculations are done without having to group the rows (as is necessary with aggregate functions). Window functions are essential for tasks like running totals, ranking, and moving averages.

This guide provides an overview of **T-SQL window functions**, including the syntax, common types, and examples.

---

### **Key Concepts of Window Functions**

1. **Windowing**: A window function works over a set of rows, called a "window." Each row in the result set is evaluated in the context of the window defined by the query.
   
2. **Syntax**: The basic syntax of a window function looks like this:
   ```sql
   SELECT column1, window_function() OVER (PARTITION BY column2 ORDER BY column3) AS result
   FROM table_name;
   ```

   - **`PARTITION BY`**: Divides the result set into partitions to perform the calculation.
   - **`ORDER BY`**: Defines the order in which the rows are processed within each partition.
   - **`OVER`**: Specifies the window of rows for the window function.

---

### **Types of Window Functions**

1. **Aggregate Window Functions**
   
   Aggregate window functions are similar to regular aggregate functions but are used to perform calculations over a defined window of rows.

   **Examples:**
   - `SUM()`: Calculates the sum of a given column over the window.
   - `AVG()`: Computes the average of a column in the window.
   - `COUNT()`: Counts the rows within the window.
   - `MIN()` and `MAX()`: Return the minimum or maximum value within the window.

   **Example**:
   ```sql
   SELECT EmployeeID, Salary,
          SUM(Salary) OVER (PARTITION BY Department ORDER BY Salary DESC) AS RunningTotal
   FROM Employees;
   ```

2. **Ranking Window Functions**
   
   Ranking functions assign ranks to rows based on the order specified in the `ORDER BY` clause.

   **Examples:**
   - `ROW_NUMBER()`: Assigns a unique, sequential number to each row within a partition.
   - `RANK()`: Assigns a rank to each row, with ties receiving the same rank but leaving gaps in the sequence.
   - `DENSE_RANK()`: Similar to `RANK()`, but does not leave gaps between tied ranks.
   - `NTILE()`: Divides the result set into a specified number of groups and assigns each row a group number.

   **Example**:
   ```sql
   SELECT EmployeeID, Salary,
          ROW_NUMBER() OVER (PARTITION BY Department ORDER BY Salary DESC) AS Rank
   FROM Employees;
   ```

3. **Value Window Functions**
   
   These functions provide access to individual rows' values within the window.

   **Examples:**
   - `LEAD()`: Returns the value of the following row in the result set.
   - `LAG()`: Returns the value of the preceding row.
   - `FIRST_VALUE()`: Returns the first value in the window.
   - `LAST_VALUE()`: Returns the last value in the window.

   **Example**:
   ```sql
   SELECT EmployeeID, Salary,
          LEAD(Salary) OVER (ORDER BY Salary DESC) AS NextSalary
   FROM Employees;
   ```

4. **Window Frame Functions**
   
   Window frame functions define how rows are included in the window. You can use the `ROWS` or `RANGE` clauses to define how the window is framed relative to the current row.

   **Examples:**
   - `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`: Includes all rows from the beginning of the partition up to the current row.
   - `RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`: Works similarly but considers rows with equal values in the `ORDER BY` clause.

   **Example**:
   ```sql
   SELECT EmployeeID, Salary,
          SUM(Salary) OVER (PARTITION BY Department ORDER BY Salary ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS RunningTotal
   FROM Employees;
   ```

---

### **Practical Use Cases**

1. **Running Totals**:
   To calculate the running total of a column, use the `SUM()` window function along with `ORDER BY` to specify the order of rows.
   
   **Example**:
   ```sql
   SELECT OrderID, OrderDate, Amount,
          SUM(Amount) OVER (ORDER BY OrderDate) AS RunningTotal
   FROM Orders;
   ```

2. **Top N Records**:
   Using `ROW_NUMBER()`, you can select the top N records based on a certain criterion, such as the highest salary or top sales.
   
   **Example**:
   ```sql
   SELECT EmployeeID, Salary,
          ROW_NUMBER() OVER (ORDER BY Salary DESC) AS Rank
   FROM Employees
   WHERE Rank <= 10;
   ```

3. **Calculating Moving Averages**:
   A moving average can be calculated using the `AVG()` function and the `ROWS BETWEEN` clause.

   **Example**:
   ```sql
   SELECT OrderDate, Amount,
          AVG(Amount) OVER (ORDER BY OrderDate ROWS BETWEEN 2 PRECEDING AND CURRENT ROW) AS MovingAvg
   FROM Orders;
   ```

4. **Find Previous or Next Row Values**:
   Using `LEAD()` and `LAG()`, you can easily compare values between consecutive rows.

   **Example**:
   ```sql
   SELECT EmployeeID, Salary,
          LAG(Salary, 1) OVER (ORDER BY Salary DESC) AS PreviousSalary
   FROM Employees;
   ```

5. **Ranking Employees by Salary**:
   You can use `RANK()` or `DENSE_RANK()` to rank employees by their salary within a department.
   
   **Example**:
   ```sql
   SELECT Department, EmployeeID, Salary,
          RANK() OVER (PARTITION BY Department ORDER BY Salary DESC) AS SalaryRank
   FROM Employees;
   ```

---

### **Performance Considerations**

- **Efficiency**: Window functions can sometimes lead to performance issues if not used carefully. It's important to ensure that your `PARTITION BY` and `ORDER BY` clauses are optimized, especially when dealing with large datasets.
- **Indexing**: Indexes on columns used in `ORDER BY` and `PARTITION BY` can help improve performance.
- **Avoiding Overuse**: While window functions are powerful, overusing them (especially in complex queries with multiple windowing clauses) can cause slowdowns. It's essential to strike a balance.

---

### **Conclusion**
Window functions in T-SQL provide significant flexibility and power when working with complex queries. They allow you to perform calculations over a range of rows, giving you more control and efficiency than traditional aggregate functions. By understanding the various window functions and their use cases, you can leverage them to solve a wide array of SQL problems.

Happy querying!
