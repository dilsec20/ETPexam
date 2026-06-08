# Unit 3: Database Management Systems (DBMS)

---

## 3.1 Introduction

**Database:** Organized collection of structured data.  
**DBMS:** Software that manages databases. Examples: MySQL, Oracle, PostgreSQL.  
**RDBMS:** Stores data in tables (relations) with rows and columns, related using keys.

> **PYQ: DBMS acts as interface between the user and the software** ✅

### Data Definitions:
| Term | Definition |
|---|---|
| **Table (Relation)** | Rows and columns of related data |
| **Field (Attribute/Column)** | Single piece of data |
| **Record (Tuple/Row)** | One complete entry |
| **Schema** | Structure/design of database |
| **Instance** | Actual data at a point in time |
| **Degree** | Number of columns |
| **Cardinality** | Number of rows |

### Data Redundancy Problem:
> **PYQ: If data is stored in two places in the db, changing in one spot will cause data inconsistency** ✅

---

## 3.2 SQL Categories

| Category | Commands | Purpose |
|---|---|---|
| **DDL** | CREATE, ALTER, DROP, TRUNCATE, RENAME | Define structure |
| **DML** | SELECT, INSERT, UPDATE, DELETE | Manipulate data |
| **DCL** | GRANT, REVOKE | Control access |
| **TCL** | COMMIT, ROLLBACK, SAVEPOINT | Manage transactions |

### Deleting Values from a Table:
```sql
DELETE FROM teachers;                    -- Deletes all rows (can rollback)
DELETE FROM teachers WHERE id = 'Null';  -- Deletes specific rows
TRUNCATE TABLE teachers;                 -- Removes all rows (cannot rollback)
DROP TABLE teachers;                     -- Removes table entirely
```

> **PYQ: Correct command to delete values in a relation? → DELETE FROM teaches** ✅  
> "Remove table teaches" = DROP, "Delete from teaches where id='Null'" deletes specific rows

### DELETE vs TRUNCATE vs DROP:
| Command | Type | Rows | Structure | Rollback | WHERE |
|---|---|---|---|---|---|
| DELETE | DML | Specific/all | Kept | ✅ Yes | ✅ Yes |
| TRUNCATE | DDL | All | Kept | ❌ No | ❌ No |
| DROP | DDL | All | Removed | ❌ No | ❌ No |

---

## 3.3 Database Keys

| Key | Definition |
|---|---|
| **Primary Key** | Uniquely identifies each row. NOT NULL + UNIQUE. One per table. |
| **Foreign Key** | References primary key of another table. Maintains referential integrity. |
| **Candidate Key** | All attributes that CAN be primary key |
| **Super Key** | Any set of attributes that uniquely identifies a row |
| **Composite Key** | Primary key made of 2+ columns |
| **Alternate Key** | Candidate keys NOT selected as primary key |
| **Unique Key** | Ensures uniqueness. Allows ONE NULL. Multiple per table. |

> **PYQ: Foreign key requires PRIMARY KEY to function in a relational database** ✅

---

## 3.4 ER Model vs Relational Model

### ER Model:
- An **attribute of an entity CAN have more than one value** (multivalued attribute)
- An **attribute CAN be composite** (e.g., Name = First + Last)

### Relational Model:
- In a row of a relational table, an attribute can have **exactly one value or a NULL value**
- A relational table attribute **CANNOT have more than one value** (1NF rule)

> **PYQ: Which is INCORRECT?**  
> "In a row of a relational table, an attribute can have more than one value" → **INCORRECT ✅** (violates 1NF)

---

## 3.5 Normalization

| Normal Form | Rule |
|---|---|
| **1NF** | Atomic values only (no multivalued/repeating groups) |
| **2NF** | 1NF + No partial dependency |
| **3NF** | 2NF + No transitive dependency |
| **BCNF** | 3NF + Every determinant is a candidate key |

---

## 3.6 Transactions & ACID

| Property | Description |
|---|---|
| **Atomicity** | All or nothing |
| **Consistency** | Valid state → valid state |
| **Isolation** | No interference between concurrent transactions |
| **Durability** | Committed = permanent |

### Concurrency Issues:
| Problem | Description |
|---|---|
| **Dirty Read** | Reading uncommitted data |
| **Lost Update** | One update overwrites another |
| **Non-Repeatable Read** | Same query, different results |
| **Phantom Read** | New rows appear |

---

## 3.7 Joins

| Join | Returns |
|---|---|
| **INNER JOIN** | Only matching rows from both |
| **LEFT JOIN** | All left + matching right |
| **RIGHT JOIN** | All right + matching left |
| **FULL OUTER JOIN** | All rows from both |
| **CROSS JOIN** | Cartesian product |
| **SELF JOIN** | Table joined with itself |

---

## MCQ Practice Questions (50+ PYQ Style)

---

**Q1.** The DBMS acts as an interface between _____ and _____ of an enterprise-class system:

a) Data and the DBMS  
b) Application and SQL  
c) Database application and the database  
**d) The user and the software ✅**

---

**Q2.** Which command correctly deletes values in a relation 'teaches'?

**a) Delete from teaches; ✅**  
b) Delete from teaches where id = 'Null';  
c) Remove table teaches;  
d) Drop table teaches;

---

**Q3.** If data is stored in two places in the db, what happens?

a) Storage is wasted & changing one will cause inconsistency  
b) Can be more easily accessed  
**c) Changing data in one spot will cause data inconsistency ✅**  
d) Storage is wasted

---

**Q4.** Which key constraint is required for foreign keys in a relational database?

a) Unique Key  
**b) Primary Key ✅**  
c) Candidate Key  
d) Check Key

---

**Q5.** Given ER and relational models, which is INCORRECT?

a) An attribute of an entity can have more than one value  
b) An attribute of an entity can be composite  
**c) In a row of a relational table, an attribute can have more than one value ✅**  
d) In a relational table, an attribute can have exactly one value or NULL

---

**Q6.** Which SQL command adds a new column?

a) INSERT  
b) UPDATE  
**c) ALTER ✅**  
d) CREATE

---

**Q7.** Primary Key is:

**a) NOT NULL and UNIQUE ✅**  
b) NULL and UNIQUE  
c) NOT NULL only  
d) Optional

---

**Q8.** DELETE is a _____ command:

a) DDL  
**b) DML ✅**  
c) DCL  
d) TCL

---

**Q9.** TRUNCATE is a _____ command:

**a) DDL ✅**  
b) DML  
c) DCL  
d) TCL

---

**Q10.** Which normal form eliminates transitive dependency?

a) 1NF  
b) 2NF  
**c) 3NF ✅**  
d) BCNF

---

**Q11.** ACID "all or nothing" property:

**a) Atomicity ✅**  
b) Consistency  
c) Isolation  
d) Durability

---

**Q12.** Foreign key references:

a) Alternate Key  
**b) Primary Key ✅**  
c) Super Key  
d) Unique Key

---

**Q13.** INNER JOIN returns:

a) All left rows  
b) All right rows  
**c) Only matching rows from both ✅**  
d) All rows

---

**Q14.** COUNT() is which type of function?

a) String  
**b) Aggregate ✅**  
c) Date  
d) Conversion

---

**Q15.** COMMIT belongs to:

a) DDL  
b) DML  
c) DCL  
**d) TCL ✅**

---

**Q16.** 1NF requires:

**a) Atomic values (no repeating groups) ✅**  
b) No transitive dependency  
c) No partial dependency  
d) Every determinant is candidate key

---

**Q17.** GRANT and REVOKE are:

a) DDL  
b) DML  
**c) DCL ✅**  
d) TCL

---

**Q18.** DISTINCT removes:

**a) Duplicate rows ✅**  
b) NULL rows  
c) All rows  
d) Columns

---

**Q19.** HAVING clause filters:

a) Individual rows  
**b) Groups (after GROUP BY) ✅**  
c) Columns  
d) Tables

---

**Q20.** 2NF eliminates:

**a) Partial dependency ✅**  
b) Transitive dependency  
c) Redundancy  
d) All anomalies

---

**Q21.** Number of rows = ?

a) Degree  
**b) Cardinality ✅**  
c) Domain  
d) Schema

---

**Q22.** Number of columns = ?

**a) Degree ✅**  
b) Cardinality  
c) Domain  
d) Instance

---

**Q23.** ROLLBACK:

a) Saves changes  
**b) Undoes changes to last COMMIT/SAVEPOINT ✅**  
c) Deletes table  
d) Locks table

---

**Q24.** Dirty Read:

**a) Reading uncommitted data from another transaction ✅**  
b) Data corruption  
c) Missing index  
d) Table dropped

---

**Q25.** Serializable isolation level prevents:

a) Only dirty reads  
b) Only phantom reads  
**c) All concurrency problems ✅**  
d) Nothing

---

**Q26.** DROP TABLE does:

a) Deletes rows  
b) Removes column  
**c) Deletes table structure and all data ✅**  
d) Empties table

---

**Q27.** TRUNCATE can have WHERE clause?

a) Yes  
**b) No ✅**

---

**Q28.** Composite key is:

a) Foreign key  
**b) Primary key of 2+ columns ✅**  
c) Auto-increment key  
d) Unique key

---

**Q29.** Alternate keys are:

a) Foreign keys  
**b) Candidate keys NOT chosen as primary key ✅**  
c) Super keys  
d) Composite keys

---

**Q30.** ORDER BY default sort:

**a) ASC (Ascending) ✅**  
b) DESC  
c) Random  
d) None

---

**Q31.** Self Join is:

**a) Table joined with itself ✅**  
b) Two different tables  
c) Cross product  
d) Natural join

---

**Q32.** Cross Join produces:

**a) Cartesian product ✅**  
b) Matching rows  
c) Distinct rows  
d) Nothing

---

**Q33.** WHERE filters _____; HAVING filters _____:

**a) Rows; groups ✅**  
b) Groups; rows  
c) Both rows  
d) Both groups

---

**Q34.** Referential integrity is maintained by:

a) Primary Key  
**b) Foreign Key ✅**  
c) Unique Key  
d) Check

---

**Q35.** SAVEPOINT:

a) Ends transaction  
**b) Sets rollback point within transaction ✅**  
c) Commits  
d) Deletes

---

**Q36.** BCNF stands for:

**a) Boyce-Codd Normal Form ✅**  
b) Basic Codd NF  
c) Binary Codd NF  
d) Base Column NF

---

**Q37.** Denormalization improves:

**a) Read/query performance ✅**  
b) Write performance  
c) Normalization  
d) Security

---

**Q38.** A view is:

**a) Virtual table based on a query ✅**  
b) Physical table  
c) Stored procedure  
d) Trigger

---

**Q39.** An index:

**a) Speeds up data retrieval ✅**  
b) Slows queries  
c) Deletes data  
d) Creates tables

---

**Q40.** LIKE 'A%' matches:

**a) Strings starting with A ✅**  
b) Ending with A  
c) Containing A  
d) Exact 'A'

---

**Q41.** To check for NULL:

a) = NULL  
**b) IS NULL ✅**  
c) == NULL  
d) EQUALS NULL

---

**Q42.** AS keyword creates:

**a) Alias (temporary name) ✅**  
b) Permanent rename  
c) New table  
d) Index

---

**Q43.** Subquery is also called:

**a) Inner/Nested query ✅**  
b) Outer query  
c) Super query  
d) Main query

---

**Q44.** BETWEEN tests for:

a) Pattern match  
**b) Range of values ✅**  
c) Existence  
d) NULL

---

**Q45.** NULL = NULL evaluates to:

a) TRUE  
b) FALSE  
**c) UNKNOWN ✅**  
d) Error

---

**Q46.** Second highest salary query:

a) SELECT MIN(salary)  
**b) SELECT MAX(salary) WHERE salary < (SELECT MAX(salary)) ✅**  
c) SELECT salary LIMIT 2  
d) SELECT TOP 2

---

**Q47.** A trigger is:

a) A manual procedure  
**b) Auto-executed procedure on INSERT/UPDATE/DELETE ✅**  
c) A view  
d) A constraint

---

**Q48.** Stored procedure is:

**a) Precompiled set of SQL statements stored in DB ✅**  
b) A temporary table  
c) A constraint  
d) A view

---

**Q49.** Unique key allows:

a) No NULLs  
**b) One NULL ✅**  
c) Multiple NULLs  
d) Duplicates

---

**Q50.** Primary key per table:

**a) Only one ✅**  
b) Multiple  
c) None required  
d) Depends

---

## Scenario / One-Line Answers

**S1.** DBMS acts as interface between user and software/database.  
**S2.** Data in two places → changing one causes inconsistency (anomaly).  
**S3.** Foreign key needs primary key of referenced table to maintain referential integrity.  
**S4.** ER model allows multivalued attributes; relational model does NOT (1NF requires atomic values).  
**S5.** DELETE = DML (can rollback, can use WHERE). TRUNCATE = DDL (no rollback, no WHERE).  
**S6.** WHERE filters before grouping; HAVING filters after GROUP BY.  
**S7.** Normalization = minimize redundancy. Denormalization = add redundancy for read speed.

---
