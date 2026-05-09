# Database Systems
## Complete Topic Explanations — Exam Preparation Guide

---

# CHAPTER 1: Introduction to Databases

## What is a Database and Why Does It Exist?

Before databases existed, organizations stored their data in flat files — simple text or binary files managed by individual application programs. A university might have one file for student registrations, another for billing, and another for course enrollment. Each file was owned by a different department and managed by a different program. This approach seems workable until you realize what it actually means in practice: the same student's name and address is stored in three separate places. When that student moves, someone must update all three files, and if only two get updated, the data is now inconsistent. The system is lying about the same person in different ways depending on which file you consult.

This is the **data redundancy problem**, and it cascades into a **data inconsistency problem**. Traditional file systems had no mechanism to coordinate data across files, enforce consistent structure, or control who could access what. Every application program was responsible for its own data format, its own security checks, and its own backup strategy.

A **database** solves this by creating a single, organized collection of related data managed by a specialized software system. Rather than each application owning its own data files, all applications share a centrally managed data store with consistent structure, controlled access, and coordinated updates. The student's address lives in exactly one place, and every system that needs it reads from that one place.

## The Database Management System (DBMS)

A **Database Management System** is the software layer that sits between users or applications and the actual stored data. You never interact with raw database files directly — everything goes through the DBMS, which handles storage, retrieval, security, concurrency, and recovery on your behalf.

The DBMS is responsible for translating your requests — expressed in a high-level query language — into the actual file operations needed to fulfill them. It also ensures that multiple users accessing the database simultaneously do not interfere with each other, and that the database remains consistent even when hardware failures occur mid-operation.

Well-known DBMS products include Oracle Database, Microsoft SQL Server, MySQL, PostgreSQL, and SQLite. They differ in scale, performance, licensing, and features, but they all provide the same fundamental services defined by the database field.

## Advantages of the Database Approach

The move from file systems to databases brings concrete, measurable benefits that explain why virtually every serious information system uses a database today.

**Controlled redundancy** means data is stored in one place and referenced everywhere else it is needed, eliminating the inconsistency that comes from duplicate copies. **Data independence** means application programs are shielded from changes in the physical storage structure — if a database administrator reorganizes how data is stored on disk, existing programs continue to work without modification. **Concurrent access** means many users can read and modify the database simultaneously, with the DBMS coordinating their activities to prevent conflicts. **Backup and recovery** are handled systematically, ensuring data is not lost even when failures occur. **Security enforcement** means access to data can be controlled at a fine-grained level — some users can see certain tables but not others, some can modify data while others can only read it.

## Roles in a Database Environment

Understanding who is responsible for what in a database environment helps make sense of how database systems are designed and operated.

The **Database Administrator (DBA)** is responsible for the technical management of the database — installing and configuring the DBMS, defining the database structure, monitoring performance, managing backups and recovery, and controlling user access.

The **Database Designer** determines what data needs to be stored and how it should be structured — the conceptual and logical design of the database before any physical implementation.

**Application Developers** write programs that interact with the database to provide functionality to end users. **End Users** are the people who ultimately use the system through applications, often without any awareness of the database behind it.

---

# CHAPTER 2: Database Architecture and Data Models

## The Three-Level ANSI-SPARC Architecture

One of the most important theoretical contributions to database systems is the three-level architecture proposed by the ANSI-SPARC committee in the 1970s. It separates the database into three distinct levels, each serving a different audience and purpose. This separation is what enables data independence.

The **External Level** (also called the View Level) is what individual users or user groups see. Different users may have entirely different views of the same database — a nurse sees patient clinical information, a billing clerk sees financial information, and both are looking at the same underlying database but through different windows tailored to their needs.

The **Conceptual Level** (also called the Logical Level) is the complete logical structure of the entire database — all the entities, their attributes, and their relationships — without any reference to how the data is physically stored. This is the designer's view and the most important level for understanding database design.

The **Internal Level** (also called the Physical Level) describes how data is actually stored on disk — file organizations, index structures, compression, encryption, and storage allocation. This is the DBA's and system implementer's concern.

The architecture provides two levels of independence. **Logical data independence** means you can change the conceptual schema without affecting external views or application programs. **Physical data independence** means you can change the internal schema — reorganize physical storage — without affecting the conceptual or external schemas. This is the property that makes database systems so much more maintainable than file-based systems.

## Data Models

A data model is a set of concepts used to describe the structure of a database. It provides a way to think about and represent data before deciding on a physical implementation.

The **Relational Model**, proposed by E.F. Codd in 1970, organizes data into tables (called relations). Each table has rows (called tuples) representing individual records and columns (called attributes) representing the properties of those records. The relational model is extraordinarily successful — it has dominated database practice for over fifty years and underpins virtually every enterprise information system.

The **Hierarchical Model** organizes data in a tree structure where each record has one parent. It was popular in early mainframe database systems (IBM's IMS is the canonical example) but its rigid parent-child structure makes it awkward for data with multiple relationships.

The **Network Model** extends the hierarchical model to allow records to have multiple parents, forming a graph structure. It was more flexible than the hierarchical model but required navigating the data structure explicitly through pointers, making applications complex and tightly coupled to the data structure.

**NoSQL models** emerged in the 2000s to address the needs of internet-scale applications. They include document stores (MongoDB), key-value stores (Redis), column-family stores (Cassandra), and graph databases (Neo4j). They sacrifice some of the relational model's rigor in exchange for horizontal scalability and flexibility with unstructured data.

---

# CHAPTER 3: The Entity-Relationship Model

## Conceptual Design and the ER Model

Before you can build a database, you need a clear, unambiguous description of what the database needs to represent. This is **conceptual design**, and the primary tool for it is the **Entity-Relationship (ER) model**, developed by Peter Chen in 1976.

The ER model provides a graphical language for describing the real world in terms that can be directly translated into a database structure. It is the bridge between the requirements gathered from users and the technical implementation in a DBMS. A good ER diagram communicates both to a business analyst who knows nothing about databases and to a developer who will implement it.

## Entities and Attributes

An **entity** is a distinct, identifiable thing in the real world that we want to store information about. A student, a course, a book, a bank account, an employee — these are all entities. In an ER diagram, entities are represented as rectangles.

An **attribute** is a property of an entity that we want to record. A Student entity might have attributes: StudentID, Name, DateOfBirth, Email, Address. Attributes are represented as ovals connected to their entity.

Attributes come in several varieties that matter for design:

- **Simple attributes** cannot be divided further — StudentID, Age, Salary.
- **Composite attributes** are made up of sub-attributes — Name can be split into FirstName and LastName; Address can be split into Street, City, and PostalCode. Whether to keep a composite attribute whole or split it depends on whether the application ever needs the parts individually.
- **Single-valued attributes** hold one value per entity instance — a person has one date of birth.
- **Multi-valued attributes** can hold multiple values — a person may have multiple phone numbers. Multi-valued attributes require special handling in the relational model.
- **Derived attributes** can be calculated from other stored data — Age can be derived from DateOfBirth and the current date.

## Keys

A **key** is an attribute or combination of attributes whose value uniquely identifies each entity instance. No two students can have the same StudentID. Keys are the fundamental mechanism for distinguishing entities from one another and for connecting related data across tables.

When multiple attributes could each serve as a key, each is called a **candidate key**. The designer selects one as the **primary key** — the one that will be used as the main identifier. A good primary key is stable (it does not change over a person's lifetime), unique, and not null. This is why student ID numbers make better primary keys than names — names are not unique and can change.

A **composite key** is a primary key made from multiple attributes combined. Neither attribute alone uniquely identifies the entity, but together they do.

## Relationships

A **relationship** represents a meaningful association between entities. Between a Student entity and a Course entity there is an "enrolls in" relationship. In an ER diagram, relationships are represented as diamonds connected to the entities they relate.

Relationships have a **cardinality** that specifies how many instances of one entity can be associated with how many instances of another:

- **One-to-One (1:1):** Each entity instance relates to at most one instance of the other. A country has one capital city; a capital city belongs to one country.
- **One-to-Many (1:N):** One entity instance relates to many instances of the other, but each of those relates to only one of the first. One department has many employees; each employee belongs to one department.
- **Many-to-Many (M:N):** Many instances of one entity relate to many instances of the other. A student enrolls in many courses; a course has many students enrolled.

Cardinality is one of the most important decisions in database design. Getting it wrong leads to a model that cannot represent the real world correctly.

**Participation constraints** specify whether an entity's involvement in a relationship is mandatory or optional. If every employee must belong to a department, the Employee entity has total participation in the "works in" relationship. If some projects may have no employees assigned yet, Project has partial participation.

## Weak Entities

A **weak entity** is one that cannot be uniquely identified by its own attributes alone — it depends on another entity (called the **owner** or **identifying entity**) for its existence and identity. A dependent's record in a payroll system might only be identifiable by the employee it belongs to combined with the dependent's name. Without the relationship to the employee, the dependent record has no independent meaning.

---

# CHAPTER 4: The Relational Model

## Relations, Tuples, and Attributes

In the relational model, every piece of data lives in a **relation** — a table with a specific structure. The formal terminology is important to understand precisely:

- A **relation** is a table.
- A **tuple** is a row in that table — one record.
- An **attribute** is a column — one property being recorded.
- A **domain** is the set of permitted values for an attribute. The domain of a "grade" attribute might be the set {A, B, C, D, F}; any value outside this set is invalid.
- The **degree** of a relation is the number of attributes (columns) it has.
- The **cardinality** of a relation is the number of tuples (rows) it currently contains.

A relation is not just any table — it has mathematical properties that distinguish it from a spreadsheet. Every tuple must be unique (no duplicate rows). The order of tuples does not matter — a relation is a set, not a sequence. The order of attributes does not matter. Every attribute value must be atomic — it cannot itself be a list or a record.

## Relational Keys

The key concepts of the relational model depend on uniquely identifying tuples:

A **superkey** is any set of attributes that uniquely identifies tuples. In a Student table, {StudentID} is a superkey, but so is {StudentID, Name} — though the second is redundant.

A **candidate key** is a minimal superkey — one where removing any attribute would lose the uniqueness property. {StudentID} alone is sufficient for uniqueness, so it is a candidate key. {StudentID, Name} is not a candidate key because {StudentID} alone already works.

The **primary key** is the candidate key chosen as the main identifier, typically the simplest and most stable option. Primary key values must never be null.

A **foreign key** is the mechanism for representing relationships between tables. If the Employee table contains a DepartmentID column that references the primary key of the Department table, then DepartmentID in Employee is a foreign key. It enforces that every DepartmentID value in the Employee table must exist as a DepartmentID in the Department table — you cannot assign an employee to a department that does not exist. This constraint is called **referential integrity**.

## Relational Integrity Constraints

Integrity constraints are rules that the DBMS enforces to keep the data accurate and consistent.

**Entity integrity** requires that no primary key attribute can be null. A tuple that cannot be identified is meaningless.

**Referential integrity** requires that every foreign key value either matches a primary key value in the referenced table or is null (if null is permitted). It prevents orphaned records — employee records pointing to non-existent departments.

**Domain constraints** restrict attribute values to their defined domain — a date column cannot contain text, a percentage cannot exceed 100.

**Business rules** are organization-specific constraints — a salary cannot be negative, a student cannot enroll in more than six courses per semester, a product cannot have zero as its price. These are implemented as CHECK constraints in SQL.

---

# CHAPTER 5: Normalization

## Why Normalization Exists

When you first design a database, the natural impulse is to put related information together in one large table. A table for student enrollment might include the student's name and address, the course name and department, the instructor's name and office number, and the grade — all in one row. This seems convenient until you realize what problems it creates.

If an instructor's office number changes, you must update every single row in the table that mentions that instructor. Miss even one row and the data becomes inconsistent. This is called an **update anomaly**. If you want to add a new course to the catalog before any students have enrolled in it, you cannot — there is no student information to fill the student columns. This is an **insertion anomaly**. If the last student drops a course, deleting that row destroys the record of the course itself. This is a **deletion anomaly**.

These anomalies all arise from the same root cause: **functional dependency problems** — storing facts about multiple things (students, courses, instructors) in a single table. Normalization is the process of restructuring tables to eliminate these anomalies.

## Functional Dependency

The theoretical foundation of normalization is **functional dependency**. An attribute B is functionally dependent on attribute A (written A → B) when every value of A is associated with exactly one value of B. In a Student table, StudentID → Name because for any given StudentID there is exactly one Name. But Name does not determine StudentID because multiple students can share the same name.

Functional dependencies reflect real-world facts about the data. Discovering them requires understanding the business rules of the domain, not just looking at sample data. Just because the current data happens to have no two students with the same name does not mean Name → StudentID is a valid dependency — the real world allows name duplicates.

## First Normal Form (1NF)

A relation is in **First Normal Form** when every attribute value is atomic — indivisible. No attribute can contain a list, a set, or a repeating group. If a Student table has a column called "Phone Numbers" that contains multiple phone numbers separated by commas, it violates 1NF. The fix is to create a separate Phone table where each row stores one phone number for one student.

1NF is the baseline — without it, the relational model's mathematical properties do not apply.

## Second Normal Form (2NF)

A relation is in **Second Normal Form** when it is in 1NF and every non-key attribute is fully functionally dependent on the entire primary key — not just part of it. 2NF only comes into play when the primary key is composite.

Consider an Enrollment table with primary key (StudentID, CourseID). Suppose the table also stores CourseName. CourseName depends only on CourseID, not on the combination of StudentID and CourseID. This is a **partial dependency**, and it violates 2NF. The fix is to move CourseName out into a separate Course table where CourseID is the sole primary key.

## Third Normal Form (3NF)

A relation is in **Third Normal Form** when it is in 2NF and no non-key attribute is transitively dependent on the primary key through another non-key attribute.

A **transitive dependency** occurs when A → B and B → C, so A → C transitively. In an Employee table with primary key EmployeeID, suppose DepartmentID and DepartmentName are both stored. EmployeeID → DepartmentID (each employee belongs to one department), and DepartmentID → DepartmentName. So EmployeeID → DepartmentName transitively through DepartmentID. DepartmentName should be moved to a separate Department table.

## Boyce-Codd Normal Form (BCNF)

**BCNF** is a slightly stronger version of 3NF that eliminates some anomalies 3NF misses. A relation is in BCNF when, for every functional dependency A → B, A is a superkey. In other words, the only attributes that can determine other attributes are superkeys — no non-key attribute can determine any other attribute.

BCNF and 3NF are the same for most relations. Differences arise only in unusual situations where a relation has multiple overlapping candidate keys.

## Higher Normal Forms

**Fourth Normal Form (4NF)** addresses **multi-valued dependencies** — situations where one attribute independently determines multiple values of two other attributes, causing spurious combinations. **Fifth Normal Form (5NF)** addresses **join dependencies** — situations where a table can be decomposed into smaller tables and perfectly reconstructed by joining them, indicating redundancy in the original.

In practice, most well-designed databases are normalized to 3NF or BCNF. Higher normal forms are theoretically important but encountered rarely in typical database design work.

---

# CHAPTER 6: Structured Query Language (SQL)

## SQL and the Relational Model

SQL (Structured Query Language) is the standard language for interacting with relational databases. Originally developed at IBM in the 1970s as SEQUEL, it became an ISO standard and is now supported by every major DBMS. SQL is declarative — you describe what data you want, not how to retrieve it. The DBMS figures out the most efficient way to execute your query.

SQL is divided into sub-languages based on what kind of operation is being performed.

## Data Definition Language (DDL)

DDL statements define the structure of the database — creating, modifying, and deleting tables and other database objects.

`CREATE TABLE` defines a new table with its columns, data types, and constraints:

```sql
CREATE TABLE Student (
    StudentID   INT          PRIMARY KEY,
    Name        VARCHAR(100) NOT NULL,
    Email       VARCHAR(100) UNIQUE,
    DateOfBirth DATE,
    GPA         DECIMAL(3,2) CHECK (GPA >= 0.0 AND GPA <= 4.0)
);
```

Each column definition specifies a name, a data type, and optional constraints. `PRIMARY KEY` enforces entity integrity. `NOT NULL` prevents missing values. `UNIQUE` ensures no two rows share the same value. `CHECK` enforces a business rule.

`ALTER TABLE` modifies an existing table's structure — adding a column, dropping a column, or adding a constraint. `DROP TABLE` permanently deletes a table and all its data.

## Data Manipulation Language (DML)

DML statements manipulate the data within tables.

**INSERT** adds new rows:

```sql
INSERT INTO Student (StudentID, Name, Email, GPA)
VALUES (1001, 'Ali Hassan', 'ali@university.edu', 3.75);
```

**UPDATE** modifies existing rows. The WHERE clause is critical — without it, every row in the table is updated:

```sql
UPDATE Student
SET GPA = 3.80
WHERE StudentID = 1001;
```

**DELETE** removes rows. Again, WHERE is essential — omitting it deletes everything:

```sql
DELETE FROM Student
WHERE StudentID = 1001;
```

## The SELECT Statement

`SELECT` is the most powerful and most used statement in SQL. Its full syntax is:

```sql
SELECT   column_list
FROM     table_list
WHERE    condition
GROUP BY grouping_columns
HAVING   group_condition
ORDER BY sort_columns;
```

The clauses execute in a specific logical order: FROM first (identify the source data), then WHERE (filter rows), then GROUP BY (group matching rows), then HAVING (filter groups), then SELECT (compute output columns), then ORDER BY (sort the results). Understanding this order explains many behaviors that otherwise seem surprising.

**The WHERE clause** filters individual rows before grouping. It supports conditions using comparison operators, logical operators (AND, OR, NOT), range tests (BETWEEN), membership tests (IN), pattern matching (LIKE), and null tests (IS NULL).

The LIKE operator uses two wildcards: `%` matches any sequence of characters, and `_` matches exactly one character. `LIKE 'Ali%'` matches 'Ali', 'Ali Hassan', 'Alibaba'. `LIKE '_a_'` matches any three-character string with 'a' in the middle.

## Aggregate Functions and GROUP BY

Aggregate functions compute a single result from a set of rows:

- `COUNT(*)` counts rows; `COUNT(column)` counts non-null values in a column
- `SUM(column)` totals numeric values
- `AVG(column)` computes the average
- `MAX(column)` and `MIN(column)` find the largest and smallest values

`GROUP BY` divides rows into groups and applies aggregate functions to each group separately. The query below counts how many students are enrolled in each department:

```sql
SELECT DepartmentID, COUNT(*) AS StudentCount
FROM Student
GROUP BY DepartmentID;
```

`HAVING` filters groups after grouping, the way WHERE filters rows before grouping. To find only departments with more than 100 students, add `HAVING COUNT(*) > 100`.

## Joins

Joins are the mechanism for combining data from multiple tables based on related columns. They are the relational model's answer to data normalization — data is stored once across normalized tables and brought together when needed through joins.

**INNER JOIN** returns only rows where the join condition is satisfied in both tables — rows with no match are excluded from the result:

```sql
SELECT Student.Name, Course.CourseName
FROM Student
INNER JOIN Enrollment ON Student.StudentID = Enrollment.StudentID
INNER JOIN Course     ON Enrollment.CourseID = Course.CourseID;
```

**LEFT OUTER JOIN** returns all rows from the left table, and the matched rows from the right table. Where there is no match, right-table columns appear as NULL. This is used when you want all students including those enrolled in no courses.

**RIGHT OUTER JOIN** is the mirror image — all rows from the right table, matched rows from the left.

**FULL OUTER JOIN** returns all rows from both tables, with NULLs where matches are absent.

**SELF JOIN** joins a table to itself, treating it as two separate tables. This is used for hierarchical data — finding an employee's manager when both employees and managers are in the same Employee table.

## Subqueries

A subquery is a SELECT statement nested inside another SQL statement. The inner query executes first, and its result is used by the outer query.

A **scalar subquery** returns a single value — for example, finding all students with a GPA above the average:

```sql
SELECT Name FROM Student
WHERE GPA > (SELECT AVG(GPA) FROM Student);
```

A **subquery with IN** tests whether a value appears in a set returned by the inner query — finding all students enrolled in any Computer Science course:

```sql
SELECT Name FROM Student
WHERE StudentID IN (
    SELECT StudentID FROM Enrollment
    WHERE CourseID IN (
        SELECT CourseID FROM Course WHERE Department = 'CS'
    )
);
```

A **correlated subquery** references the outer query in its WHERE clause — it executes once for each row of the outer query. This is more powerful but also slower than uncorrelated subqueries.

## Views

A view is a virtual table defined by a stored SELECT query. It does not store data itself — when you query a view, the DBMS executes the underlying query and returns the results as if from a real table.

Views serve multiple important purposes. They simplify complex queries by encapsulating joins and conditions behind a simple name. They enforce security by exposing only selected columns and rows to certain users — a view of the Employee table for HR staff might exclude salary information visible only to payroll staff. They provide logical data independence — if the underlying table structure changes, only the view definition needs updating, not every application that uses the data.

---

# CHAPTER 7: Transaction Management

## What is a Transaction?

A **transaction** is a logical unit of work that must either complete entirely or not happen at all. The classic example is a bank transfer: deducting $500 from Account A and crediting $500 to Account B. These are two separate database operations, but they form one logical unit. If the system crashes after the deduction but before the credit, $500 has simply disappeared. The only acceptable outcomes are both operations succeeding together, or neither happening at all.

This all-or-nothing requirement is **atomicity**, and it is the first of the four **ACID properties** that define what a transaction guarantees:

**Atomicity** — A transaction is treated as a single indivisible unit. Either all its operations complete successfully, or none of them take effect. If any operation fails, the entire transaction is rolled back to the state before it began.

**Consistency** — A transaction takes the database from one valid consistent state to another valid consistent state. All integrity constraints must be satisfied both before and after the transaction. A transaction that would violate a constraint is not permitted to commit.

**Isolation** — Concurrent transactions execute as if they were running alone. Each transaction operates on a snapshot of the database and cannot see intermediate, uncommitted states of other transactions. Without isolation, two simultaneous transfers from the same account could both read the initial balance, both deduct from it, and together overdraw the account.

**Durability** — Once a transaction commits successfully, its effects are permanently recorded even if the system crashes immediately afterward. This requires writing changes to non-volatile storage before acknowledging the commit.

## Concurrency Control

Modern database systems serve many users simultaneously. Without coordination, concurrent transactions can interfere with each other in ways that corrupt data.

**Lost update** occurs when two transactions both read the same value, both compute an update based on it, and both write their result — the second write overwrites the first, and one update is silently lost.

**Dirty read** occurs when a transaction reads data written by another transaction that has not yet committed. If the other transaction later rolls back, the first transaction acted on data that never officially existed.

**Non-repeatable read** occurs when a transaction reads the same row twice and gets different values because another transaction modified it between the two reads.

**Phantom read** occurs when a transaction re-executes a query and finds additional rows because another transaction inserted them between the two executions.

**Locking** is the primary mechanism for preventing these problems. Before reading or modifying data, a transaction acquires a lock on it. **Shared locks** (read locks) allow multiple transactions to read simultaneously but prevent writing. **Exclusive locks** (write locks) give one transaction sole access — no other transaction can read or write the locked data until the lock is released.

**Deadlock** occurs when two transactions are each waiting for a lock held by the other, creating a cycle where neither can proceed. The DBMS detects deadlocks and resolves them by aborting one of the transactions, which is why applications must always be prepared to retry aborted transactions.

## Recovery Management

When a system failure occurs — power outage, hardware fault, software crash — the DBMS must restore the database to a consistent state. It uses a **transaction log** (also called a write-ahead log) that records every change made before it is applied to the database. On restart after a failure, the DBMS uses the log to:

- **Redo** committed transactions whose changes may not have been written to disk yet
- **Undo** uncommitted transactions whose partial changes must be reversed

The log records before-images (the data's value before the change) for undo and after-images (the value after the change) for redo. Periodic **checkpoints** create stable points in the log from which recovery can begin, limiting how much of the log must be replayed.

---

# CHAPTER 8: Database Design Process

## Phases of Database Design

Database design moves through a sequence of increasingly detailed phases, each building on the previous one:

**Requirement Analysis** is the starting point — interviewing users, studying existing systems, and documenting what data needs to be stored and what operations need to be supported. The output is not yet a design; it is a clear understanding of the problem.

**Conceptual Design** translates the requirements into a high-level, implementation-independent model — typically an ER diagram. It captures what entities exist, what their attributes are, and how they relate. No thought is given yet to tables, columns, or specific DBMS products.

**Logical Design** maps the conceptual model to the data model of the chosen DBMS — in most cases, converting the ER diagram into a set of relational tables, applying normalization, and defining primary and foreign keys. The result is a schema that is theoretically correct but still independent of any specific DBMS implementation.

**Physical Design** decides how the logical design will be implemented on actual hardware — choosing file organizations, defining indexes for performance, deciding on partitioning and clustering strategies. Physical design is performance-oriented and DBMS-specific.

**Implementation** creates the database using DDL statements, populates it with initial data, and deploys the application.

## Converting ER Diagrams to Relational Tables

The mapping from ER model to relational tables follows a set of rules that are worth understanding clearly:

Each **regular (strong) entity type** becomes a table. Each simple attribute of the entity becomes a column. The primary key of the entity becomes the primary key of the table. Composite attributes are expanded into their component simple attributes.

Each **weak entity type** becomes a table whose primary key combines its own partial key with the primary key of its owner entity. A foreign key references the owner entity's table.

Each **1:N relationship** is represented by adding a foreign key to the table on the "many" side. The foreign key references the primary key of the "one" side. If the relationship has attributes, those attributes also become columns in the "many" side table.

Each **M:N relationship** becomes a separate table (called a junction table or associative table) whose primary key is the combination of the foreign keys of both participating entities. Any attributes of the relationship become additional columns in this junction table.

Each **1:1 relationship** can be handled by adding a foreign key on either side. The choice depends on which side has total participation — the foreign key goes there, minimizing null values.

**Multi-valued attributes** become separate tables. The new table's primary key combines the original entity's primary key with the multi-valued attribute.

---

# CHAPTER 9: Indexing and Query Optimization

## Why Indexing Matters

Without an index, finding a specific row in a large table requires scanning every row from the first to the last — a **full table scan**. For a table with millions of rows, this is catastrophically slow. An index is a separate data structure that allows the DBMS to find rows matching a condition without reading the entire table.

Think of an index like the index at the back of a textbook. Instead of reading the entire book to find mentions of "normalization," you look up "normalization" in the index, get a list of page numbers, and go directly to those pages. A database index works on the same principle.

## B-Tree Indexes

The most common index structure is the **B-tree** (balanced tree). In a B-tree index, the leaf nodes contain the actual index values together with pointers to the corresponding table rows. The non-leaf nodes contain guide values that direct the search toward the correct leaf node.

The tree is kept **balanced** — all leaf nodes are at the same depth — so every search takes roughly the same amount of time regardless of which value is being sought. For a table of one million rows, a B-tree index typically requires only about 20 comparisons to find any specific value.

B-tree indexes are excellent for:

- Exact match queries (`WHERE email = 'ali@example.com'`)
- Range queries (`WHERE salary BETWEEN 50000 AND 80000`)
- ORDER BY operations on indexed columns
- JOIN operations on indexed columns

## Hash Indexes

A **hash index** applies a hash function to the search key value, producing a hash code that directly identifies the storage location of the matching row. Hash indexes are extremely fast for exact-match lookups — essentially O(1). However, they are useless for range queries because hashing destroys the ordering of values.

## Index Trade-offs

Indexes are not free. Every index on a table must be updated every time a row is inserted, updated, or deleted. A table with ten indexes requires ten index updates for every insertion. For tables that are read far more than they are written, this overhead is easily worth it. For tables that receive constant high-volume inserts, excessive indexing can become a performance bottleneck.

Primary keys are always indexed automatically by the DBMS. Foreign keys should almost always be indexed because joins on unindexed foreign keys require full table scans. Columns that frequently appear in WHERE clauses with selective conditions — conditions that eliminate a large fraction of rows — are good candidates for indexing.

## Query Optimization

When you submit an SQL query, the DBMS does not simply execute it as written. The **query optimizer** examines the query, considers multiple execution strategies (called execution plans), estimates the cost of each, and executes the cheapest one.

The optimizer considers factors like:

- Which indexes are available on the tables being queried
- The estimated number of rows each operation will produce
- The cost of joining tables in different orders
- Whether a sort can be avoided by using an index

Understanding query optimization helps you write queries that the optimizer can execute efficiently and helps you understand why adding an index can dramatically accelerate a query that previously ran slowly.

---

# CHAPTER 10: Relational Algebra

## The Theoretical Foundation of SQL

Relational algebra is the formal mathematical foundation underlying SQL. While SQL is the practical language database users write, relational algebra is the theoretical framework that defines what the relational model can express and how queries should be interpreted.

Understanding relational algebra deepens your understanding of SQL because SQL queries can be expressed as sequences of relational algebra operations. The query optimizer works internally in terms of relational algebra expressions when planning query execution.

## Fundamental Operations

**Selection (σ)** filters rows based on a condition — it is the formal counterpart of the SQL WHERE clause. `σ (salary > 50000) (Employee)` produces a new relation containing only employees with salary above 50000.

**Projection (π)** extracts specific columns and removes duplicates — it corresponds to the column list in SELECT. `π (name, salary) (Employee)` produces a relation with only the name and salary columns.

**Union (∪)** combines the rows of two relations that have the same schema, removing duplicates. The two relations must be union-compatible — same number of columns with compatible domains.

**Set Difference (−)** returns the rows that appear in the first relation but not in the second. Again, the relations must be union-compatible.

**Cartesian Product (×)** combines every row of one relation with every row of another — the foundation of join operations. A Cartesian product of a 100-row table and a 200-row table produces a 20,000-row result. In SQL this is equivalent to listing two tables in the FROM clause without a join condition.

**Rename (ρ)** assigns a new name to a relation or its attributes, necessary when the same table appears multiple times in a query (self-joins).

## Derived Operations

**Join** is derived by combining Cartesian Product with Selection. A natural join automatically matches columns with the same name across two relations — it is equivalent to a Cartesian product followed by a selection that requires matching values, followed by a projection that removes duplicate columns.

**Intersection (∩)** returns rows that appear in both relations. It is derivable from set difference: R ∩ S = R − (R − S).

**Division (÷)** finds the values in one relation that are associated with all values in another — it is the relational algebra counterpart of queries involving "for all" conditions. Find all students who are enrolled in every course offered.

---

# CHAPTER 11: Database Security

## Why Database Security is Critical

A database typically contains the most sensitive assets an organization has — customer records, financial data, personnel files, medical histories, intellectual property. A security breach does not just cause immediate damage; it exposes the organization to legal liability, regulatory penalties, and lasting reputational harm. Database security is not a feature to be added after a system is built — it must be designed in from the beginning.

## Authentication and Authorization

**Authentication** establishes who you are — verifying identity through passwords, certificates, or multi-factor authentication before any database access is granted.

**Authorization** determines what an authenticated user is permitted to do — which tables they can see, which operations they can perform, which rows are accessible to them. Authorization in SQL is managed through the GRANT and REVOKE commands.

`GRANT SELECT ON Student TO hr_clerk;` allows a user named hr_clerk to read the Student table.
`GRANT SELECT, INSERT, UPDATE ON Enrollment TO registrar;` gives the registrar permission to read and modify enrollment records.
`REVOKE SELECT ON Student FROM hr_clerk;` removes the previously granted permission.

Privileges can be granted WITH GRANT OPTION, allowing the recipient to pass the privilege on to other users. This creates chains of privilege delegation that can be complex to track and manage.

## Views as a Security Mechanism

Views provide a powerful, flexible security mechanism beyond simple table-level permissions. By granting a user access to a view rather than the underlying table, you can:

- Restrict visible columns (hide salary data from non-HR users)
- Restrict visible rows (show a manager only their own team's records)
- Prevent certain data modifications while allowing others

A view is read-only by default unless it meets specific criteria — a view over a single table without aggregation or derived columns is typically updatable.

## SQL Injection

**SQL injection** is one of the most dangerous and most common database security vulnerabilities. It occurs when user input is incorporated directly into SQL queries without proper sanitization, allowing an attacker to modify the query's logic.

If an application builds a login query as:
`"SELECT * FROM Users WHERE username = '" + input + "'"` and the user enters `' OR '1'='1`, the resulting query becomes `SELECT * FROM Users WHERE username = '' OR '1'='1'` — a condition that is always true, potentially granting access to every account.

The defense is **parameterized queries** (also called prepared statements), where the query structure is fixed and user input is treated as data values, never as SQL syntax. The DBMS ensures values can never be interpreted as SQL commands.

## Encryption

Sensitive data in a database should be encrypted — both in storage (data at rest) and during transmission (data in transit). Encrypting entire databases or specific columns prevents an attacker who gains access to the storage files from reading the data without the encryption keys. Secure communication protocols (TLS) prevent network interception.

---

# CHAPTER 12: Stored Procedures, Triggers, and Advanced SQL

## Stored Procedures

A **stored procedure** is a named, compiled SQL program stored in the database itself and executed on the database server. Rather than sending many individual SQL statements from an application, a stored procedure encapsulates the logic and the application calls it by name.

The benefits are substantial. Network traffic is reduced — instead of sending multiple SQL statements, the application sends a single call. Performance improves because stored procedures are pre-compiled and cached. Security improves because users can be granted permission to execute a procedure without being granted direct access to the underlying tables. Code reuse is enabled — the same logic is called from multiple applications.

## Triggers

A **trigger** is a stored procedure that executes automatically when a specified database event occurs — typically INSERT, UPDATE, or DELETE on a table. Unlike a stored procedure which is called explicitly, a trigger fires automatically in response to data changes.

Triggers are used for:

- **Enforcing complex business rules** that cannot be expressed as simple constraints
- **Auditing** — automatically recording who changed what data and when
- **Maintaining derived data** — automatically updating summary tables when detail data changes
- **Cascading updates** — automatically propagating a change to related tables

A trigger specifies the event that fires it (BEFORE or AFTER INSERT/UPDATE/DELETE), the table it watches, and the body of code to execute. Inside the trigger body, special references like `NEW` and `OLD` provide access to the new values being inserted and the old values being replaced or deleted.

## Cursors

SQL is set-oriented — most statements operate on entire sets of rows at once. Sometimes, however, you need to process rows one at a time, applying different logic to each. A **cursor** is a database object that allows row-by-row navigation through a result set.

Working with a cursor involves four steps:

1. **DECLARE** the cursor, defining the SELECT query it is based on
2. **OPEN** the cursor, executing the query and creating the result set
3. **FETCH** rows one at a time, processing each in sequence
4. **CLOSE** the cursor when finished

Cursors should be used sparingly because row-by-row processing is far slower than set-oriented operations. Experienced database programmers solve most problems without cursors by writing set-oriented SQL.

---

# CHAPTER 13: NoSQL Databases

## Why NoSQL Emerged

The relational model and SQL dominated databases for decades and still dominate enterprise systems. But in the 2000s, internet companies like Google, Amazon, and Facebook encountered data problems the relational model was not designed for.

These companies needed to store and process data at scales of billions of records across thousands of machines simultaneously. Relational databases scale vertically — you handle more load by upgrading to bigger, more powerful hardware. This approach has physical and economic limits. Internet companies needed **horizontal scalability** — adding more commodity machines to a cluster rather than upgrading existing ones.

The relational model's strict schema also became a constraint — when you have hundreds of millions of users with varying attributes, a fixed table schema feels rigid. And some data — social graphs, geographic data, document collections — is simply not naturally tabular.

NoSQL databases trade away some of the relational model's guarantees in exchange for scalability and flexibility. Most NoSQL systems relax the ACID guarantees in favor of **eventual consistency** — the guarantee that if no new updates are made, all replicas of the data will eventually converge to the same value. For many internet applications, this trade-off is acceptable.

## Types of NoSQL Databases

**Document stores** such as MongoDB store data as JSON-like documents. Each document is self-describing — it contains its own structure rather than conforming to a predefined schema. Documents representing the same kind of entity can have different fields. This is ideal for content management, user profiles, and catalogs where different records have different attributes.

**Key-Value stores** such as Redis store data as simple pairs of a key and a value. The value can be anything — a string, a number, a serialized object. Retrieval requires knowing the exact key. Key-value stores are extremely fast and are commonly used as caches, session stores, and for any data where you always know the key you want.

**Column-family stores** such as Apache Cassandra organize data into rows identified by a key, where each row can have a large and different set of columns grouped into families. They are optimized for reading and writing large volumes of data across many machines and are used for time-series data, IoT telemetry, and analytics workloads.

**Graph databases** such as Neo4j store data as nodes (entities) and edges (relationships) in a graph structure. They are designed for data where the relationships are as important as the data itself — social networks, recommendation engines, fraud detection, and knowledge graphs. Traversing complex relationships in a graph database is far more efficient than the equivalent multi-join SQL query.

---

# CHAPTER 14: Database Administration

## The DBA's Responsibilities

The **Database Administrator** is the custodian of the database — responsible for its performance, availability, security, and integrity. In small organizations, the DBA role may be combined with other responsibilities; in large enterprises, there may be teams of DBAs specializing in different aspects.

The DBA's core responsibilities span several domains:

**Schema management** involves creating and maintaining the database structure, applying changes when requirements evolve, managing versions, and ensuring changes do not break existing applications.

**Performance tuning** involves monitoring query performance, identifying slow queries, creating or modifying indexes, adjusting DBMS configuration parameters, and occasionally restructuring data to improve performance.

**Backup and recovery** involves designing and implementing backup strategies, verifying that backups are complete and restorable, and executing recovery procedures when failures occur. A backup that has never been tested is not a backup — it is a hope.

**Security administration** involves creating user accounts, assigning appropriate privileges, auditing access, and responding to security incidents.

**Capacity planning** involves monitoring storage usage growth, predicting future requirements, and ensuring the system has adequate resources before they become constraints.

## Backup Strategies

Databases require systematic backup strategies that balance the need for data protection against the cost of performing and storing backups.

A **full backup** copies the entire database. It is the simplest type of backup and the simplest to restore from, but it takes the most time to create and the most storage to hold. Performing full backups frequently is practical only for small databases.

An **incremental backup** copies only the data that has changed since the last backup of any type. It is the fastest to perform and smallest in size, but restoring requires the last full backup plus every subsequent incremental backup applied in order.

A **differential backup** copies all data that has changed since the last full backup. It takes more time and space than incremental backups but less than full backups, and restoring requires only the last full backup plus the last differential backup.

Most organizations combine these strategies — for example, a full backup weekly, differential backups daily, and transaction log backups hourly. The recovery time objective (how long recovery takes) and the recovery point objective (how much data can be lost) drive the choice of strategy.

---

*End of Database Systems Course Guide*

*Key Reference: Ramez Elmasri & Shamkant Navathe — "Fundamentals of Database Systems"*
*Supporting Reference: C.J. Date — "An Introduction to Database Systems"*
