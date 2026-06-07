# Unit 3: Database Management Systems (DBMS)

---

## 3.1 Introduction

**Database:** Organized collection of structured data stored electronically.  
**DBMS:** Software that manages databases (create, read, update, delete). Examples: MySQL, Oracle, PostgreSQL, SQL Server.  
**RDBMS:** Relational DBMS — stores data in tables with rows and columns and supports SQL. Data is related using keys.

### DBMS vs File System:
| Feature | File System | DBMS |
|---|---|---|
| Redundancy | High | Controlled |
| Consistency | Low | High |
| Concurrency | No support | Supported |
| Security | File-level | Fine-grained |
| Backup/Recovery | Manual | Automatic |

---

## 3.2 Data Definitions

| Term | Definition |
|---|---|
| **Table (Relation)** | A collection of related data organized in rows and columns |
| **Field (Attribute/Column)** | A single piece of data; defines the type of data stored |
| **Record (Tuple/Row)** | A single entry in a table; represents one complete data item |
| **Schema** | The structure/design of the database (tables, columns, types, constraints) |
| **Instance** | The actual data in the database at a given point in time |
| **Domain** | The set of permissible values for an attribute (e.g., age: 0-150) |
| **Degree** | Number of columns in a table |
| **Cardinality** | Number of rows in a table |

---

## 3.3 SQL and Data Manipulation

### SQL Categories:

| Category | Full Form | Commands | Purpose |
|---|---|---|---|
| **DDL** | Data Definition Language | CREATE, ALTER, DROP, TRUNCATE, RENAME | Define/modify database structure |
| **DML** | Data Manipulation Language | SELECT, INSERT, UPDATE, DELETE | Manipulate data |
| **DCL** | Data Control Language | GRANT, REVOKE | Control access permissions |
| **TCL** | Transaction Control Language | COMMIT, ROLLBACK, SAVEPOINT | Manage transactions |
| **DQL** | Data Query Language | SELECT | Query/retrieve data |

### Key SQL Commands:
```sql
-- DDL
CREATE TABLE students (id INT PRIMARY KEY, name VARCHAR(50), age INT);
ALTER TABLE students ADD email VARCHAR(100);
DROP TABLE students;
TRUNCATE TABLE students;   -- Deletes all rows, keeps structure

-- DML
INSERT INTO students VALUES (1, 'Amit', 21);
UPDATE students SET age = 22 WHERE id = 1;
DELETE FROM students WHERE id = 1;
SELECT * FROM students WHERE age > 20 ORDER BY name;

-- Aggregate Functions
SELECT COUNT(*), AVG(age), MAX(age), MIN(age), SUM(age) FROM students;

-- GROUP BY and HAVING
SELECT department, COUNT(*) FROM employees GROUP BY department HAVING COUNT(*) > 5;

-- JOINS
SELECT e.name, d.dept_name FROM employees e
INNER JOIN departments d ON e.dept_id = d.id;
```

### Types of Joins:
| Join | Description |
|---|---|
| **INNER JOIN** | Returns matching rows from both tables |
| **LEFT JOIN** | All rows from left + matching from right (NULL if no match) |
| **RIGHT JOIN** | All rows from right + matching from left |
| **FULL OUTER JOIN** | All rows from both tables |
| **CROSS JOIN** | Cartesian product of both tables |
| **SELF JOIN** | Table joined with itself |

### DELETE vs TRUNCATE vs DROP:
| Command | Type | Rows | Structure | Rollback | WHERE |
|---|---|---|---|---|---|
| DELETE | DML | Removes specific/all rows | Kept | Yes | Yes |
| TRUNCATE | DDL | Removes all rows | Kept | No | No |
| DROP | DDL | Removes all rows | Removed | No | No |

---

## 3.4 Database Keys

| Key | Definition |
|---|---|
| **Primary Key** | Uniquely identifies each row. NOT NULL, UNIQUE. One per table. |
| **Candidate Key** | All attributes that can be primary key (minimal superkey) |
| **Super Key** | Any set of attributes that uniquely identifies a row |
| **Foreign Key** | A field in one table that references the primary key of another table. Establishes relationship. |
| **Composite Key** | Primary key made of two or more columns |
| **Alternate Key** | Candidate keys that are NOT selected as primary key |
| **Unique Key** | Ensures all values are unique. Allows ONE NULL. |

### Referential Integrity:
Foreign key must reference an existing primary key or be NULL. Prevents orphan records.

---

## 3.5 Normalization

**Normalization:** Process of organizing data to reduce redundancy and dependency.

| Normal Form | Rule |
|---|---|
| **1NF** | No multivalued/repeating groups; all values are atomic (single value per cell) |
| **2NF** | 1NF + No partial dependency (non-key attributes depend on the ENTIRE primary key) |
| **3NF** | 2NF + No transitive dependency (non-key attributes depend ONLY on primary key, not on other non-key attributes) |
| **BCNF** | 3NF + Every determinant is a candidate key |

**Partial Dependency:** Non-key attribute depends on PART of a composite key.  
**Transitive Dependency:** A → B → C (C depends on A through B).

### Denormalization:
Intentionally adding redundancy back to improve **read performance** (at cost of write complexity).

---

## 3.6 Transactions

**Transaction:** A sequence of operations performed as a single logical unit of work.

### ACID Properties:
| Property | Description |
|---|---|
| **Atomicity** | All or nothing — either all operations succeed or none do |
| **Consistency** | Database goes from one valid state to another valid state |
| **Isolation** | Concurrent transactions don't interfere with each other |
| **Durability** | Once committed, changes are permanent even after system failure |

### Transaction States:
Active → Partially Committed → Committed (success) OR Failed → Aborted

### Concurrency Control Issues:
| Problem | Description |
|---|---|
| **Dirty Read** | Reading uncommitted data from another transaction |
| **Non-Repeatable Read** | Same query returns different results in same transaction |
| **Phantom Read** | New rows appear in results of same query |
| **Lost Update** | Two transactions update same data; one update lost |

### Isolation Levels:
| Level | Dirty Read | Non-Repeatable | Phantom |
|---|---|---|---|
| Read Uncommitted | Yes | Yes | Yes |
| Read Committed | No | Yes | Yes |
| Repeatable Read | No | No | Yes |
| Serializable | No | No | No |

---

## MCQ Practice Questions (50+)

---

**Q1.** Which SQL command is used to add a new column to an existing table?
A. INSERT  B. UPDATE  **C. ALTER ✅**  D. CREATE

---

**Q2.** Which key uniquely identifies each row in a table?
**A. Primary Key ✅**  B. Foreign Key  C. Alternate Key  D. Super Key

---

**Q3.** DELETE is a _____ command:
A. DDL  **B. DML ✅**  C. DCL  D. TCL

---

**Q4.** TRUNCATE is a _____ command:
**A. DDL ✅**  B. DML  C. DCL  D. TCL

---

**Q5.** Which normal form eliminates transitive dependency?
A. 1NF  B. 2NF  **C. 3NF ✅**  D. BCNF

---

**Q6.** ACID property that ensures "all or nothing":
**A. Atomicity ✅**  B. Consistency  C. Isolation  D. Durability

---

**Q7.** Foreign key references which key of another table?
A. Alternate Key  B. Super Key  **C. Primary Key ✅**  D. Unique Key

---

**Q8.** Which join returns all rows from both tables?
A. INNER JOIN  B. LEFT JOIN  C. RIGHT JOIN  **D. FULL OUTER JOIN ✅**

---

**Q9.** Which aggregate function counts rows?
A. SUM()  B. AVG()  **C. COUNT() ✅**  D. MAX()

---

**Q10.** COMMIT belongs to which SQL category?
A. DDL  B. DML  C. DCL  **D. TCL ✅**

---

**Q11.** 1NF requires:
A. No transitive dependency  B. No partial dependency  **C. Atomic values (no repeating groups) ✅**  D. Every determinant is candidate key

---

**Q12.** GRANT and REVOKE are _____ commands:
A. DDL  B. DML  **C. DCL ✅**  D. TCL

---

**Q13.** Which keyword is used to remove duplicates in SELECT?
A. UNIQUE  **B. DISTINCT ✅**  C. REMOVE  D. DIFFERENT

---

**Q14.** GROUP BY is used with:
A. WHERE  **B. Aggregate functions ✅**  C. ORDER BY  D. LIKE

---

**Q15.** HAVING clause is used to filter:
A. Individual rows  **B. Groups (after GROUP BY) ✅**  C. Columns  D. Tables

---

**Q16.** Which normal form eliminates partial dependency?
A. 1NF  **B. 2NF ✅**  C. 3NF  D. 4NF

---

**Q17.** The number of rows in a table is called:
A. Degree  **B. Cardinality ✅**  C. Domain  D. Schema

---

**Q18.** The number of columns in a table is called:
**A. Degree ✅**  B. Cardinality  C. Domain  D. Instance

---

**Q19.** ROLLBACK is used to:
A. Save changes  **B. Undo changes to last COMMIT or SAVEPOINT ✅**  C. Delete table  D. Lock table

---

**Q20.** A Dirty Read occurs when:
**A. A transaction reads uncommitted data from another ✅**  B. Data is corrupted  C. Index is missing  D. Table is dropped

---

**Q21.** Which isolation level prevents all concurrency problems?
A. Read Uncommitted  B. Read Committed  C. Repeatable Read  **D. Serializable ✅**

---

**Q22.** DROP TABLE does what?
A. Deletes all rows  B. Removes a column  **C. Deletes the table structure and all data permanently ✅**  D. Empties the table

---

**Q23.** TRUNCATE vs DELETE — which can have a WHERE clause?
A. TRUNCATE  **B. DELETE ✅**  C. Both  D. Neither

---

**Q24.** A composite key is:
A. A key with no NULL values  **B. A primary key made of two or more columns ✅**  C. A foreign key  D. An auto-increment key

---

**Q25.** Candidate keys that are NOT selected as primary key are called:
A. Super keys  B. Foreign keys  **C. Alternate keys ✅**  D. Composite keys

---

**Q26.** Which SQL clause is used to sort results?
A. GROUP BY  **B. ORDER BY ✅**  C. HAVING  D. WHERE

---

**Q27.** Default sort order of ORDER BY?
**A. ASC (Ascending) ✅**  B. DESC  C. Random  D. None

---

**Q28.** INNER JOIN returns:
A. All rows from left table  B. All rows from right table  **C. Only matching rows from both tables ✅**  D. All rows from both

---

**Q29.** Which constraint ensures a column cannot have NULL values?
A. UNIQUE  **B. NOT NULL ✅**  C. CHECK  D. DEFAULT

---

**Q30.** Which constraint ensures column values are unique?
**A. UNIQUE ✅**  B. NOT NULL  C. PRIMARY KEY  D. CHECK

---

**Q31.** A primary key is _____ and _____:
A. NULL and UNIQUE  **B. NOT NULL and UNIQUE ✅**  C. NULL and not unique  D. Optional

---

**Q32.** Self Join is:
A. Joining two different tables  **B. Joining a table with itself ✅**  C. Cross product  D. Natural join

---

**Q33.** Cross Join produces:
**A. Cartesian product of both tables ✅**  B. Matching rows  C. Distinct rows  D. Nothing

---

**Q34.** Which function returns the average of a column?
A. SUM  **B. AVG ✅**  C. COUNT  D. TOTAL

---

**Q35.** WHERE clause filters _____ ; HAVING clause filters _____:
**A. Individual rows; groups ✅**  B. Groups; rows  C. Both filter rows  D. Both filter groups

---

**Q36.** INSERT INTO belongs to:
A. DDL  **B. DML ✅**  C. TCL  D. DCL

---

**Q37.** Referential integrity is maintained by:
A. Primary Key  **B. Foreign Key ✅**  C. Unique Key  D. Check Constraint

---

**Q38.** SAVEPOINT is used to:
A. End a transaction  **B. Set a rollback point within a transaction ✅**  C. Commit changes  D. Delete data

---

**Q39.** BCNF stands for:
A. Basic Codd Normal Form  **B. Boyce-Codd Normal Form ✅**  C. Binary Codd Normal Form  D. Base Column Normal Form

---

**Q40.** Denormalization is done to:
A. Reduce redundancy  **B. Improve read/query performance ✅**  C. Add more constraints  D. Remove tables

---

**Q41.** A view in SQL is:
A. A physical table  **B. A virtual table based on a query ✅**  C. A stored procedure  D. A trigger

---

**Q42.** Which command creates a view?
A. MAKE VIEW  **B. CREATE VIEW ✅**  C. BUILD VIEW  D. VIEW CREATE

---

**Q43.** An index in a database:
**A. Speeds up data retrieval ✅**  B. Slows down queries  C. Deletes data  D. Creates tables

---

**Q44.** LIKE 'A%' matches:
**A. Strings starting with A ✅**  B. Strings ending with A  C. Strings containing A  D. Exact match 'A'

---

**Q45.** LIKE '%A' matches:
A. Strings starting with A  **B. Strings ending with A ✅**  C. Exact match  D. Any string

---

**Q46.** NULL = NULL evaluates to:
A. TRUE  B. FALSE  **C. UNKNOWN/NULL ✅**  D. Error

---

**Q47.** To check for NULL values, we use:
A. = NULL  **B. IS NULL ✅**  C. == NULL  D. EQUALS NULL

---

**Q48.** Which keyword is used to rename a column/table temporarily?
**A. AS (Alias) ✅**  B. RENAME  C. CHANGE  D. SET

---

**Q49.** Subquery is also called:
A. Super query  **B. Inner query / Nested query ✅**  C. Outer query  D. Main query

---

**Q50.** Which SQL operator is used to test for a range of values?
A. IN  **B. BETWEEN ✅**  C. LIKE  D. EXISTS

---

## Scenario & One-Line Answer Questions

---

**S1.** You need to remove all rows from a table but keep the table structure. Which command?
> **TRUNCATE TABLE tablename;** — Removes all rows but keeps the table structure. Cannot be rolled back.

**S2.** What is the difference between DELETE and TRUNCATE?
> **DELETE** is DML (can have WHERE, can rollback, fires triggers). **TRUNCATE** is DDL (removes all rows, cannot rollback, faster, no triggers).

**S3.** A column stores phone numbers like "9876543210, 1234567890" in one cell. Which normal form is violated?
> **1NF** is violated — 1NF requires atomic values (no multivalued attributes in a single cell).

**S4.** An employee table has (EmpID, EmpName, DeptID, DeptName). DeptName depends on DeptID, not EmpID. What dependency is this?
> **Transitive Dependency** (EmpID → DeptID → DeptName). Violates **3NF**. Fix by creating a separate Department table.

**S5.** Two transactions modify the same account balance simultaneously and one update is lost. What problem is this?
> **Lost Update** problem — a concurrency control issue where one transaction's changes are overwritten by another.

**S6.** A transaction reads data that another transaction has not yet committed. What is this called?
> **Dirty Read** — reading uncommitted data that may later be rolled back.

**S7.** What does ACID stand for?
> **Atomicity** (all or nothing), **Consistency** (valid state to valid state), **Isolation** (no interference), **Durability** (permanent after commit).

**S8.** What is the difference between HAVING and WHERE?
> **WHERE** filters individual rows BEFORE grouping. **HAVING** filters groups AFTER GROUP BY.

**S9.** What is referential integrity?
> A constraint that ensures a **foreign key value must match an existing primary key** in the referenced table, or be NULL. Prevents orphan records.

**S10.** What is the difference between a primary key and a unique key?
> **Primary Key**: uniquely identifies rows, NOT NULL, only ONE per table. **Unique Key**: ensures uniqueness, allows ONE NULL, multiple per table.

**S11.** Write a query to find the second highest salary.
> `SELECT MAX(salary) FROM employees WHERE salary < (SELECT MAX(salary) FROM employees);`

**S12.** What is a stored procedure?
> A **precompiled set of SQL statements** stored in the database that can be executed repeatedly. Improves performance and reduces network traffic.

**S13.** What is a trigger?
> A **special stored procedure that automatically executes** when a specific event (INSERT, UPDATE, DELETE) occurs on a table.

**S14.** What is a cursor in SQL?
> A database object used to **retrieve and process rows one at a time** from a result set. Used when row-by-row processing is needed.

**S15.** What is normalization in one line?
> Normalization is the process of **organizing data to minimize redundancy and dependency** by dividing tables and defining relationships.

---
