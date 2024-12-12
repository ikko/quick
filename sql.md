Here's a **Databricks ANSI SQL cheatsheet** highlighting the most important features of SQL, including key concepts and functions often used in Databricks environments. This includes basic SQL operations, window functions, and advanced querying techniques.

---

### **Databricks ANSI SQL Cheatsheet**

#### **1. Basic SQL Operations**

- **Select All Columns**:
    ```sql
    SELECT * FROM table_name;
    ```

- **Select Specific Columns**:
    ```sql
    SELECT column1, column2 FROM table_name;
    ```

- **Filtering Rows**:
    ```sql
    SELECT * FROM table_name WHERE column1 > 10;
    ```

- **Sorting Rows**:
    ```sql
    SELECT * FROM table_name ORDER BY column1 DESC;
    ```

- **Distinct Values**:
    ```sql
    SELECT DISTINCT column1 FROM table_name;
    ```

- **Limiting Results**:
    ```sql
    SELECT * FROM table_name LIMIT 10;
    ```

#### **2. Aggregate Functions**

- **COUNT, SUM, AVG, MIN, MAX**:
    ```sql
    SELECT COUNT(*) FROM table_name;
    SELECT SUM(column1) FROM table_name;
    SELECT AVG(column1) FROM table_name;
    SELECT MIN(column1), MAX(column1) FROM table_name;
    ```

- **GROUP BY**:
    ```sql
    SELECT column1, COUNT(*) FROM table_name GROUP BY column1;
    ```

- **HAVING** (Filtering groups):
    ```sql
    SELECT column1, COUNT(*) 
    FROM table_name 
    GROUP BY column1 
    HAVING COUNT(*) > 5;
    ```

#### **3. Joins**

- **INNER JOIN**:
    ```sql
    SELECT * 
    FROM table1 t1
    INNER JOIN table2 t2 ON t1.column1 = t2.column1;
    ```

- **LEFT JOIN (or LEFT OUTER JOIN)**:
    ```sql
    SELECT * 
    FROM table1 t1
    LEFT JOIN table2 t2 ON t1.column1 = t2.column1;
    ```

- **RIGHT JOIN (or RIGHT OUTER JOIN)**:
    ```sql
    SELECT * 
    FROM table1 t1
    RIGHT JOIN table2 t2 ON t1.column1 = t2.column1;
    ```

- **FULL JOIN (or FULL OUTER JOIN)**:
    ```sql
    SELECT * 
    FROM table1 t1
    FULL JOIN table2 t2 ON t1.column1 = t2.column1;
    ```

- **SELF JOIN** (Joining a table to itself):
    ```sql
    SELECT a.*, b.*
    FROM table_name a
    JOIN table_name b ON a.column1 = b.column1;
    ```

#### **4. Subqueries**

- **Subquery in SELECT**:
    ```sql
    SELECT column1, (SELECT COUNT(*) FROM table2 WHERE table2.column1 = table1.column1) AS count
    FROM table1;
    ```

- **Subquery in WHERE**:
    ```sql
    SELECT * 
    FROM table1
    WHERE column1 = (SELECT MAX(column1) FROM table2);
    ```

- **Correlated Subquery**:
    ```sql
    SELECT a.column1
    FROM table1 a
    WHERE a.column2 = (SELECT MAX(b.column2) FROM table2 b WHERE b.column1 = a.column1);
    ```

#### **5. Case Statements**

- **Simple CASE Statement**:
    ```sql
    SELECT column1,
           CASE 
               WHEN column1 > 10 THEN 'High'
               ELSE 'Low'
           END AS column_category
    FROM table_name;
    ```

- **CASE with Multiple Conditions**:
    ```sql
    SELECT column1,
           CASE
               WHEN column1 BETWEEN 1 AND 10 THEN 'Low'
               WHEN column1 BETWEEN 11 AND 20 THEN 'Medium'
               ELSE 'High'
           END AS column_range
    FROM table_name;
    ```

#### **6. Window Functions**

Window functions perform calculations across a set of rows related to the current row, allowing for more advanced analysis.

- **Basic Window Function (ROW_NUMBER)**:
    ```sql
    SELECT column1,
           ROW_NUMBER() OVER (PARTITION BY column2 ORDER BY column1 DESC) AS row_num
    FROM table_name;
    ```

- **RANK and DENSE_RANK**:
    ```sql
    SELECT column1, 
           RANK() OVER (PARTITION BY column2 ORDER BY column1 DESC) AS rank,
           DENSE_RANK() OVER (PARTITION BY column2 ORDER BY column1 DESC) AS dense_rank
    FROM table_name;
    ```

- **NTILE** (Divides rows into a specified number of groups):
    ```sql
    SELECT column1,
           NTILE(4) OVER (ORDER BY column1 DESC) AS quartile
    FROM table_name;
    ```

- **LEAD and LAG** (Accesses next or previous row’s data):
    ```sql
    SELECT column1,
           LAG(column1, 1) OVER (ORDER BY column1) AS previous_value,
           LEAD(column1, 1) OVER (ORDER BY column1) AS next_value
    FROM table_name;
    ```

- **Aggregating with Window Functions**:
    ```sql
    SELECT column1,
           SUM(column2) OVER (PARTITION BY column1 ORDER BY column2) AS cumulative_sum
    FROM table_name;
    ```

- **Window Function with Filtering (WHERE clause)**:
    ```sql
    SELECT column1, 
           COUNT(*) OVER (PARTITION BY column2) AS count_partition
    FROM table_name
    WHERE column1 > 10;
    ```

#### **7. String Functions**

- **Concatenate Strings**:
    ```sql
    SELECT CONCAT(column1, ' ', column2) AS full_name FROM table_name;
    ```

- **Substring**:
    ```sql
    SELECT SUBSTRING(column1, 1, 3) FROM table_name;  -- Get first 3 characters
    ```

- **String Length**:
    ```sql
    SELECT LENGTH(column1) FROM table_name;
    ```

- **Upper and Lowercase**:
    ```sql
    SELECT UPPER(column1), LOWER(column1) FROM table_name;
    ```

- **Replace Substring**:
    ```sql
    SELECT REPLACE(column1, 'old_value', 'new_value') FROM table_name;
    ```

#### **8. Date and Time Functions**

- **Current Date/Time**:
    ```sql
    SELECT CURRENT_DATE, CURRENT_TIMESTAMP;
    ```

- **Extract Date Parts**:
    ```sql
    SELECT EXTRACT(YEAR FROM column1) AS year, EXTRACT(MONTH FROM column1) AS month
    FROM table_name;
    ```

- **Date Add/Subtract**:
    ```sql
    SELECT DATE_ADD(column1, 10) FROM table_name;  -- Adds 10 days
    SELECT DATE_SUB(column1, 10) FROM table_name;  -- Subtracts 10 days
    ```

- **Format Date**:
    ```sql
    SELECT DATE_FORMAT(column1, 'yyyy-MM-dd') FROM table_name;
    ```

#### **9. Mathematical Functions**

- **Round, Ceiling, and Floor**:
    ```sql
    SELECT ROUND(column1, 2) FROM table_name;  -- Round to 2 decimal places
    SELECT CEIL(column1) FROM table_name;      -- Round up
    SELECT FLOOR(column1) FROM table_name;     -- Round down
    ```

- **Random Number Generation**:
    ```sql
    SELECT RAND() AS random_value;
    ```

#### **10. Creating and Modifying Tables**

- **Create Table**:
    ```sql
    CREATE TABLE table_name (
        column1 INT,
        column2 STRING,
        column3 DATE
    );
    ```

- **Alter Table (Add Column)**:
    ```sql
    ALTER TABLE table_name ADD COLUMN new_column STRING;
    ```

- **Drop Table**:
    ```sql
    DROP TABLE table_name;
    ```

- **Rename Table**:
    ```sql
    ALTER TABLE old_table_name RENAME TO new_table_name;
    ```

---

### **Common SQL Functions Summary**

| **Function**              | **Syntax**                                        |
|---------------------------|---------------------------------------------------|
| **COUNT**                 | `SELECT COUNT(*) FROM table_name;`                |
| **SUM**                   | `SELECT SUM(column1) FROM table_name;`            |
| **AVG**                   | `SELECT AVG(column1) FROM table_name;`            |
| **MAX / MIN**             | `SELECT MAX(column1) FROM table_name;`            |
| **RANK**                  | `RANK() OVER (PARTITION BY column2 ORDER BY column1)` |
| **ROW_NUMBER**            | `ROW_NUMBER() OVER (PARTITION BY column2 ORDER BY column1)` |
| **LEAD / LAG**            | `LEAD(column1, 1) OVER (ORDER BY column1)`        |
| **CONCAT**                | `CONCAT(column1, column2)`                        |
| **DATE_FORMAT**           | `DATE_FORMAT(column1, 'yyyy-MM-dd')`             |

---

This cheatsheet covers the most commonly used features of **Databricks ANSI SQL** for data analysis, including window functions, aggregation, joins, subqueries, and date manipulation. It’s a great reference for writing efficient SQL queries in Databricks.