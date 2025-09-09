# SQL Topics for Interviews

## 1️⃣ Basics

**Definition:**  
SQL (Structured Query Language) is used to **create, manage, and query relational databases**.

**Types of SQL Commands:**

| Category | Commands | Purpose |
|----------|----------|---------|
| **DDL** (Data Definition Language) | CREATE, ALTER, DROP, TRUNCATE | Define or modify database structure |
| **DML** (Data Manipulation Language) | SELECT, INSERT, UPDATE, DELETE | Perform data operations (read/write) |
| **DCL** (Data Control Language) | GRANT, REVOKE | Control access/permissions on DB objects |
| **TCL** (Transaction Control Language) | COMMIT, ROLLBACK, SAVEPOINT | Manage transactions to maintain data integrity |

**Notes:**  
- **DDL commands** affect the schema and structure of the database.  
- **DML commands** manipulate the actual data inside tables.  
- **DCL commands** control who can do what in the database.  
- **TCL commands** ensure that database operations are executed safely and consistently.

## 2️⃣ Data Types

**1. Numeric Types:**  
Used to store numbers.  

- `INT`  
  - Stores whole numbers (e.g., -2,147,483,648 to 2,147,483,647).  
  - Commonly used for counting or IDs.  

- `BIGINT`  
  - Stores very large whole numbers.  
  - Useful for huge datasets where `INT` might overflow.  

- `DECIMAL` (or `NUMERIC`)  
  - Stores exact decimal numbers with fixed precision.  
  - Example: `DECIMAL(10,2)` can store numbers like 12345678.90.  
  - Ideal for financial calculations to avoid rounding errors.  

- `FLOAT` / `REAL`  
  - Stores approximate decimal numbers.  
  - Less precise but requires less storage.  

---

**2. String Types:**  
Used to store text data.  

- `CHAR(n)`  
  - Fixed-length string of `n` characters.  
  - Example: `CHAR(10)` always uses 10 characters; extra space is padded with blanks.  
  - Faster for fixed-size data.  

- `VARCHAR(n)`  
  - Variable-length string up to `n` characters.  
  - Example: `VARCHAR(50)` uses only the space required.  
  - More flexible and storage-efficient than `CHAR`.  

- `TEXT`  
  - Stores large text data.  
  - Example: descriptions, articles, or comments.  

**Interview Tip:**  
- Know the difference between `CHAR` (fixed) and `VARCHAR` (variable).  
- Use `CHAR` for fixed-length codes and `VARCHAR` for variable-length text.  

---

**3. Date/Time Types:**  

- `DATE`  
  - Stores only date (`YYYY-MM-DD`).  
  - Example: `2025-09-07`.  

- `DATETIME`  
  - Stores date and time (`YYYY-MM-DD HH:MM:SS`).  
  - Example: `2025-09-07 14:30:00`.  

- `TIMESTAMP`  
  - Stores date and time with timezone info (depends on DBMS).  
  - Often used to track creation or update times.  

**Interview Tip:**  
- `DATE` only stores date.  
- `DATETIME` stores both date and time.  
- `TIMESTAMP` is often timezone-aware and can auto-update on changes.  

---

**4. Boolean Type:**  

- `BOOLEAN`  
  - Stores `TRUE` or `FALSE` values.  
  - Useful for flags like `is_active`, `is_deleted`, etc.  

**General Interview Tips:**  
- Always know storage requirements and differences between numeric types (`INT` vs `BIGINT`, `DECIMAL` vs `FLOAT`).  
- Understand when to use `CHAR` vs `VARCHAR`.  
- Be able to explain how date/time types differ and when to use each.

## 3️⃣ Table Operations

**1. Create Table**  
Used to create a new table in the database.  
Example:

```sql
CREATE TABLE Employee (
    EmpID INT PRIMARY KEY,       -- Unique identifier for each employee
    Name VARCHAR(50),            -- Employee name (up to 50 characters)
    Dept VARCHAR(20),            -- Department name (up to 20 characters)
    Salary DECIMAL(10,2)         -- Salary with 2 decimal places
);
```

- **PRIMARY KEY** ensures each row has a unique identifier.  
- **Data types** must be chosen carefully (e.g., `INT`, `VARCHAR`, `DECIMAL`, etc.).

## 2. Alter Table

Used to modify an existing table (add, modify, or delete columns).

**Example:**
```sql
ALTER TABLE Employee ADD COLUMN JoiningDate DATE;
```
**Key Points:**
- **ADD COLUMN** adds a new column.  
- You can also **MODIFY COLUMN** or **DROP COLUMN** depending on DBMS support.

## 3. Drop Table

Used to remove an entire table and its data permanently.

**Example:**
```sql
DROP TABLE Employee;
```

**Key Points:**
- Data and structure are permanently deleted.  
- Use with caution, especially in production databases.

**Interview Tips:**
- Be able to write basic `CREATE`, `ALTER`, and `DROP` statements.  
- Understand how constraints (`PRIMARY KEY`, `UNIQUE`, `NOT NULL`) affect table structure.  
- Know the difference between `DROP TABLE` (deletes table) and `TRUNCATE TABLE` (deletes all data but keeps structure).

## 4️⃣ Basic Queries

**1. Select All Columns**  
Retrieve all columns from a table.

```sql
SELECT * FROM Employee;
```
**Key Points:**
- `*` selects all columns.  
- Useful for quick checks but not recommended for large tables in production.

## 2. Select Specific Columns

Retrieve only the columns you need.

**Example:**
```sql
SELECT Name, Salary FROM Employee;
```
**Key Points:**
- Improves query performance by fetching only required data.  
- Makes result sets easier to read.

## 3. WHERE Clause

Filter rows based on conditions.

**Example:**
```sql
SELECT * FROM Employee WHERE Dept = 'IT';
```
**Key Points:**
- Filters rows where `Dept` equals `'IT'`.  
- Can use comparison operators (`=`, `>`, `<`, `>=`, `<=`, `<>`) and logical operators (`AND`, `OR`, `NOT`).

## 4. Operators with Conditions

**Example:**
```sql
SELECT * FROM Employee WHERE Salary > 50000 AND Dept = 'IT';
```
**Key Points:**
- Combine multiple conditions with `AND` or `OR`.  
- Logical operators help refine query results.

## 5. ORDER BY

Sort results based on one or more columns.

**Example:**
```sql
SELECT * FROM Employee ORDER BY Salary DESC;
```

**Key Points:**
- `ASC` → ascending (default)  
- `DESC` → descending  
- Can sort by multiple columns: `ORDER BY Dept ASC, Salary DESC`

**Interview Tips:**
- Understand the difference between `*` and selecting specific columns.  
- Be familiar with `WHERE` conditions and logical operators.  
- Know how to sort results using `ORDER BY`.  
- Be able to combine filters, sorting, and specific column selection in one query.

## 5️⃣ Aggregate Functions

**Definition:**  
Aggregate functions perform calculations on multiple rows of a table and return a single value.

**Common Aggregate Functions:**  
- `COUNT()` → Counts the number of rows  
- `SUM()` → Adds up numeric values  
- `AVG()` → Calculates the average of numeric values  
- `MIN()` → Finds the minimum value  
- `MAX()` → Finds the maximum value  

**Examples:**

```sql
-- Count total employees
SELECT COUNT(*) FROM Employee;

-- Average salary of IT department
SELECT AVG(Salary) FROM Employee WHERE Dept='IT';

-- Maximum salary in the company
SELECT MAX(Salary) FROM Employee;
```
**Key Points:**
- `COUNT(*)` counts all rows, including those with `NULL` values in other columns.  
- `SUM()` and `AVG()` ignore `NULL` values.  
- Aggregate functions are often used with `GROUP BY` for grouping data by categories.

**Interview Tips:**
- Be able to write queries using `COUNT`, `SUM`, `AVG`, `MIN`, `MAX`.  
- Know how to combine aggregate functions with `WHERE` and `GROUP BY`.  
- Understand how `NULL` values affect aggregate results.

# 1. GROUP BY Basics

- Used to **group rows** that have the same values in one or more columns.  
- Often used with aggregate functions:  
  - `COUNT`  
  - `SUM`  
  - `AVG`  
  - `MIN`  
  - `MAX`  

### Syntax:
```sql
SELECT column1, aggregate_function(column2)
FROM table
GROUP BY column1;
```

✅ **Example:**

```sql
SELECT Dept, COUNT(*) AS EmployeeCount
FROM Employee
GROUP BY Dept;
```

# 2. HAVING vs WHERE

- **WHERE**: Filters rows **before grouping**.  
- **HAVING**: Filters **after grouping**, based on aggregate functions.  

---

✅ **Example Difference:**

```sql
-- Using WHERE (filter rows before grouping)
SELECT Dept, AVG(Salary)
FROM Employee
WHERE Salary > 30000
GROUP BY Dept;

-- Using HAVING (filter groups after aggregation)
SELECT Dept, AVG(Salary)
FROM Employee
GROUP BY Dept
HAVING AVG(Salary) > 50000;
```

# 3. Example Query

```sql
SELECT Dept, AVG(Salary) AS AvgSalary
FROM Employee
GROUP BY Dept
HAVING AVG(Salary) > 50000;
```

🔎 **Step-by-Step Execution**

1. **FROM Employee** → Load all records.  
2. **GROUP BY Dept** → Group employees by department.  
3. **AVG(Salary)** → Calculate average salary per department.  
4. **HAVING AVG(Salary) > 50000** → Keep only those departments where the average salary is greater than **50,000**.  
5. **SELECT Dept, AvgSalary** → Return department name + average salary.

# 4. Key Points for Interviews

- **HAVING** is applied **after GROUP BY** and aggregates are computed.  

✅ Always remember the **order of execution**:  
**WHERE → GROUP BY → HAVING → SELECT → ORDER BY**

- **HAVING** can use **aggregate functions**; **WHERE cannot**.  
- You can use both **WHERE** and **HAVING** together.  

✅ **Combined Example (WHERE + HAVING)**

```sql
SELECT Dept, AVG(Salary) AS AvgSalary
FROM Employee
WHERE Salary > 20000          -- row-level filter
GROUP BY Dept
HAVING AVG(Salary) > 50000;   -- group-level filter 
```

# 5. Common Interview Questions

**Q1. Difference between WHERE and HAVING?**  
👉 **WHERE** filters rows **before grouping**,  
👉 **HAVING** filters groups **after aggregation**.  

**Q2. Can we use HAVING without GROUP BY?**  
👉 Yes, but then it acts like a **WHERE** on aggregate results.  

✅ **Example:**

```sql
SELECT AVG(Salary)
FROM Employee
HAVING AVG(Salary) > 50000;
```

**Q3. Can GROUP BY be used without aggregates?**  
👉 Yes, but usually it’s combined with aggregates. Without aggregates, it just groups duplicates.  

✅ **Example:**

```sql
SELECT Dept
FROM Employee
GROUP BY Dept;
```
**Q4. What is the performance impact of WHERE vs HAVING?**  
👉 Use **WHERE** to filter early for efficiency,  
👉 then use **HAVING** for final group filtering.

# 📌 SQL Joins – Interview Notes

## 1. INNER JOIN
- Returns only the rows that have **matching values** in both tables.  
- Most common type of join.  

✅ **Example:**

```sql
SELECT e.Name, d.DeptName
FROM Employee e
INNER JOIN Department d ON e.DeptId = d.DeptId;
```

## 2. LEFT JOIN (LEFT OUTER JOIN)
- Returns all rows from the **left table**, and the matched rows from the right table.  
- If no match → `NULL` values for right table.  

✅ **Example:**

```sql
SELECT e.Name, d.DeptName
FROM Employee e
LEFT JOIN Department d ON e.DeptId = d.DeptId;
```

## 3. RIGHT JOIN (RIGHT OUTER JOIN)
- Returns all rows from the **right table**, and the matched rows from the left table.  
- If no match → `NULL` values for left table.  

✅ **Example:**

```sql
SELECT e.Name, d.DeptName
FROM Employee e
RIGHT JOIN Department d ON e.DeptId = d.DeptId;
```

## 4. FULL JOIN (FULL OUTER JOIN)
- Returns all rows from **both tables**.  
- Non-matching rows will have `NULL` values.  

✅ **Example:**

```sql
SELECT e.Name, d.DeptName
FROM Employee e
FULL JOIN Department d ON e.DeptId = d.DeptId;
```

## 5. CROSS JOIN
- Produces the **Cartesian product** of two tables.  
- Each row of the first table combines with **all rows** of the second table.  

✅ **Example:**

```sql
SELECT e.Name, d.DeptName
FROM Employee e
CROSS JOIN Department d;
```

## 6. SELF JOIN
- Table is joined with **itself**.  
- Useful for **hierarchical or relational data** (like managers & employees).  

✅ **Example:**

```sql
SELECT e.Name AS Employee, m.Name AS Manager
FROM Employee e
INNER JOIN Employee m ON e.ManagerId = m.EmpId;
```

## 7. Key Differences – Interview Quick Reference

| Join Type   | Returns                                               |
|------------|------------------------------------------------------|
| INNER JOIN | Only matching rows from both tables                  |
| LEFT JOIN  | All rows from left + matching rows from right       |
| RIGHT JOIN | All rows from right + matching rows from left       |
| FULL JOIN  | All rows from both tables (matches + non-matches)   |
| CROSS JOIN | Cartesian product (all combinations)                |
| SELF JOIN  | A table joined with itself                           |

## 8. Common Interview Questions

**Q1. Difference between INNER JOIN and OUTER JOIN?**  
👉 **INNER JOIN** → only matching rows.  
👉 **OUTER JOIN** → includes non-matching rows (LEFT, RIGHT, FULL).  

**Q2. What is the result size of a CROSS JOIN?**  
👉 `Rows_in_A × Rows_in_B`  

**Q3. When do you use SELF JOIN?**  
👉 For **hierarchical relationships** (e.g., employees and managers).  

**Q4. Can FULL OUTER JOIN be simulated in MySQL?**  
👉 Yes, by using `LEFT JOIN UNION RIGHT JOIN`.

## ⚡ SQL Joins – One-Line Summary

- **INNER** = only matches  
- **LEFT** = all left + matches  
- **RIGHT** = all right + matches  
- **FULL** = all from both sides  
- **CROSS** = all combinations  
- **SELF** = join table with itself

## 7️⃣ Subqueries

### Types: Single-row / Multiple-row

✅ **Example 1 – Single-row subquery:**

```sql
SELECT Name
FROM Employee
WHERE Salary > (SELECT AVG(Salary) FROM Employee);
```

### ✅ Example 2 – Multiple-row subquery:

```SQL
SELECT Name
FROM Employee
WHERE Dept IN (SELECT DeptID FROM Department WHERE Location = 'SomeLocation');
```

# 📌 SQL Indexing & Optimization – Interview Notes

## 1. What is an Index?

- An **index** is a database structure that improves the **speed of data retrieval**.  
- Works like an **index in a book** → points to the exact location of data.  
- **Reduces the number of rows** the database has to scan.

✅ **Example:**

```sql
CREATE INDEX idx_salary ON Employee(Salary);
```
- Creates an index on the **Salary** column in the `Employee` table.  
- Queries like `SELECT * FROM Employee WHERE Salary > 50000;` become faster.

## 2. Types of Indexes

| Index Type        | Description                                                                 |
|------------------|-----------------------------------------------------------------------------|
| Primary Key Index | Automatically created on primary key columns. Enforces uniqueness.          |
| Unique Index      | Ensures no duplicate values in the indexed column.                          |
| Composite Index   | Index on multiple columns for queries using multiple columns in WHERE/ORDER BY. |
| Full-Text Index   | For searching text in large text fields (MySQL specific).                   |
| Clustered Index   | Determines physical storage order of table rows (one per table).            |
| Non-Clustered Index | Separate structure from table data, can have multiple per table.          |

## 3. Primary Key / Foreign Key

- **Primary Key (PK):** Unique identifier for table rows. Automatically indexed.  
- **Foreign Key (FK):** Maintains **referential integrity** between tables.  

✅ **Example:**

```sql
CREATE TABLE Department (
    DeptID INT PRIMARY KEY,
    DeptName VARCHAR(50)
);

CREATE TABLE Employee (
    EmpID INT PRIMARY KEY,
    Name VARCHAR(50),
    DeptID INT,
    FOREIGN KEY (DeptID) REFERENCES Department(DeptID)
);
```
**PK ensures uniqueness; FK ensures valid references.**

## 4. Query Optimization

SQL queries can be slow if:  

- **Full table scans** are done.  
- **Joins** are on non-indexed columns.  
- **Large datasets** are not indexed.


## Tools / Techniques: EXPLAIN PLAN

- **EXPLAIN PLAN** shows how the database executes a query.  
- Helps identify **bottlenecks** like full table scans.  

✅ **Example:**

```sql
EXPLAIN SELECT * FROM Employee WHERE Salary > 50000;
```
**Look for index usage vs full table scan.**

## SQL Optimization Tips

- **Use Indexes:** Columns in `WHERE`, `JOIN`, `ORDER BY` are good candidates.  
- **Avoid `SELECT *`:** Only fetch required columns.  
- **Use `LIMIT`:** Avoid fetching unnecessary rows in large tables.  
- **Partitioning / Sharding:** Split huge tables to reduce query load (advanced).

## 5. Key Points for Interviews

- **Indexes** improve read/search performance but **slow down inserts/updates/deletes** (because the index needs updating).  
- **Primary keys** are automatically indexed.  
- **Foreign keys** help maintain data integrity but may add slight overhead.  
- **EXPLAIN PLAN** is critical for analyzing query performance.  
- **Composite indexes** are better for queries using multiple columns in conditions.


## ⚡ SQL Indexing & Optimization – One-Line Summary

- **Index** → Faster search.  
- **Primary/Foreign Key** → Constraints + data integrity.  
- **EXPLAIN PLAN** → Analyze query performance & optimize.


## 13️⃣ Common Interview Questions

- Difference between **INNER JOIN** vs **LEFT JOIN**  
- Difference between **WHERE** and **HAVING**  
- Explain **ACID properties**  
- Write a query to find **second highest salary**  
- Difference between **TRUNCATE** vs **DELETE**  
- Difference between **Primary Key** vs **Unique Key**  
- Difference between **Clustered** and **Non-Clustered Index**

