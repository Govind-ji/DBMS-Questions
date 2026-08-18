# DBMS — TECHNICAL INTERVIEW QUESTIONS
# EASY SET — 25 QUESTIONS

---

## Q1. What is DBMS?

### Answer

DBMS stands for Database Management System. It is software that
allows users and applications to create, store, organize,
retrieve, update, and manage data in a database.

### Explanation

A DBMS acts as an interface between applications and the
database.

Application
    ↓
DBMS
    ↓
Database

### Examples

- MySQL
- PostgreSQL
- Oracle
- SQL Server

### Possible Follow-up Questions

- What is a database?
- What is RDBMS?
- Why do we need a DBMS?

---

## Q2. What is a database?

### Answer

A database is an organized collection of data that can be
stored, accessed, managed, and updated efficiently.

### Example

A college database may contain:

Students
Courses
Teachers
Marks
Attendance

### Explanation

Instead of storing information randomly in separate files,
a database organizes it in a structured manner.

### Possible Follow-up Questions

- What is a DBMS?
- What is a relational database?
- What is a table?

---

## Q3. What is RDBMS?

### Answer

RDBMS stands for Relational Database Management System. It
stores data in tables consisting of rows and columns and
supports relationships between tables.

### Examples

- MySQL
- PostgreSQL
- Oracle
- SQL Server

### Example

Students table:

student_id | name | course_id

Courses table:

course_id | course_name

The course_id connects the two tables.

### Possible Follow-up Questions

- DBMS vs RDBMS?
- What is a relationship?
- What is a primary key?

---

## Q4. What is the difference between DBMS and RDBMS?

### Answer

DBMS is a general database management system, while RDBMS is
specifically based on the relational model and stores data
in related tables.

### Explanation

RDBMS generally provides:

- Tables
- Relationships
- Primary keys
- Foreign keys
- Constraints
- SQL support
- Transaction management

### Possible Follow-up Questions

- Is every DBMS an RDBMS?
- Give examples of RDBMS.
- Why are relationships important?

---

## Q5. What is a table?

### Answer

A table is a structured collection of data organized into
rows and columns.

### Example

Students:

| ID | Name | Age |
|----|------|-----|
| 1  | Rahul | 21 |
| 2  | Aman | 22 |

### Explanation

Rows represent records and columns represent attributes.

### Possible Follow-up Questions

- What is a row?
- What is a column?
- What is a tuple?

---

## Q6. What is a row and what is a column?

### Answer

A row represents one complete record in a table, while a
column represents an attribute or property of the records.

### Example

Students:

| ID | Name | Age |
|----|------|-----|
| 1  | Rahul | 21 |

Here:

Row → One student record

Column → ID, Name, or Age

### Possible Follow-up Questions

- What is a tuple?
- What is an attribute?
- What is a field?

---

## Q7. What is SQL?

### Answer

SQL stands for Structured Query Language. It is used to
communicate with relational databases.

### SQL can be used to

- Create tables
- Insert data
- Retrieve data
- Update data
- Delete data
- Manage permissions
- Control transactions

### Example

SELECT * FROM students;

### Possible Follow-up Questions

- What is DDL?
- What is DML?
- What is DCL?
- What is TCL?

---

## Q8. What are DDL, DML, DCL and TCL?

### Answer

SQL commands are commonly divided into different categories.

### DDL

Data Definition Language.

Examples:

CREATE
ALTER
DROP
TRUNCATE

### DML

Data Manipulation Language.

Examples:

SELECT
INSERT
UPDATE
DELETE

### DCL

Data Control Language.

Examples:

GRANT
REVOKE

### TCL

Transaction Control Language.

Examples:

COMMIT
ROLLBACK
SAVEPOINT

### Possible Follow-up Questions

- DELETE vs TRUNCATE?
- What is COMMIT?
- What is ROLLBACK?

---

## Q9. What is a primary key?

### Answer

A primary key is a column or combination of columns that
uniquely identifies every record in a table.

### Example

Students:

student_id | name

student_id can be the primary key.

### Properties

- Unique
- Cannot contain NULL
- Identifies each record

### Possible Follow-up Questions

- Can a table have multiple primary keys?
- What is a composite primary key?
- Primary key vs unique key?

---

## Q10. What is a foreign key?

### Answer

A foreign key is a column that references a key in another
table and is used to establish a relationship between tables.

### Example

Students:

student_id | name

Orders:

order_id | student_id

student_id in Orders can reference student_id in Students.

### Possible Follow-up Questions

- What is referential integrity?
- Can a foreign key contain NULL?
- Can a table have multiple foreign keys?

---

## Q11. What is a candidate key?

### Answer

A candidate key is a column or set of columns that can uniquely
identify each record in a table.

One candidate key is selected as the primary key.

### Example

If both email and student_id are unique:

student_id
email

Both can be candidate keys.

One can be selected as the primary key.

### Possible Follow-up Questions

- Candidate key vs primary key?
- What is a super key?
- What is an alternate key?

---

## Q12. What is a super key?

### Answer

A super key is any set of one or more attributes that can
uniquely identify a record.

### Example

If student_id uniquely identifies a student:

student_id

is a super key.

If student_id + name also uniquely identifies the student,
that combination is also a super key.

### Important Difference

A candidate key is a minimal super key.

### Possible Follow-up Questions

- What is a candidate key?
- What is a composite key?

---

## Q13. What is a unique key?

### Answer

A unique key ensures that values in a column or combination
of columns are unique.

### Example

An email column can have a UNIQUE constraint so that two
users cannot register with the same email.

### Difference from Primary Key

A table has one primary key, while it can have multiple
unique constraints.

NULL handling can also differ depending on the database
system.

### Possible Follow-up Questions

- Primary key vs unique key?
- Can a unique key contain NULL?

---

## Q14. What is NULL?

### Answer

NULL represents the absence of a value or an unknown value.

It is not the same as:

0

empty string

false

### Example

If a student's phone number is unknown:

phone_number = NULL

### Possible Follow-up Questions

- How do you check NULL?
- Why can't we use = NULL?
- What is IS NULL?

---

## Q15. What is a constraint?

### Answer

A constraint is a rule applied to database columns to maintain
data accuracy and integrity.

### Common Constraints

- PRIMARY KEY
- FOREIGN KEY
- UNIQUE
- NOT NULL
- CHECK
- DEFAULT

### Example

age INT CHECK(age >= 18)

### Possible Follow-up Questions

- Why are constraints important?
- What is referential integrity?
- Can constraints be added later?

---

## Q16. What is normalization?

### Answer

Normalization is the process of organizing data in a database
to reduce redundancy and improve data integrity.

### Explanation

Instead of storing repeated information in one large table,
we divide data into related tables.

### Example

Instead of:

Student + Course + Teacher information repeatedly

we can create:

Students
Courses
Teachers

and connect them using keys.

### Possible Follow-up Questions

- Explain 1NF.
- Explain 2NF.
- Explain 3NF.
- What is denormalization?

---

## Q17. What is a relationship in DBMS?

### Answer

A relationship represents an association between entities or
tables.

### Common Relationships

- One-to-One
- One-to-Many
- Many-to-Many

### Example

One department can have many employees.

Department
    ↓
Employees

This is a one-to-many relationship.

### Possible Follow-up Questions

- Explain many-to-many.
- How is many-to-many implemented?

---

## Q18. What is a one-to-one relationship?

### Answer

A one-to-one relationship means one record in one table is
associated with at most one record in another table.

### Example

One person may have one passport.

Person
    ↕
Passport

### Possible Follow-up Questions

- When would you use one-to-one?
- How is it implemented?

---

## Q19. What is a one-to-many relationship?

### Answer

A one-to-many relationship means one record in one table can
be related to multiple records in another table.

### Example

One department can have many employees.

Department
    ↓
Employee
Employee
Employee

### Implementation

The foreign key is usually placed in the "many" side.

### Possible Follow-up Questions

- Give a real-world example.
- Where is the foreign key stored?

---

## Q20. What is a many-to-many relationship?

### Answer

A many-to-many relationship means multiple records in one
table can be associated with multiple records in another table.

### Example

Students can enroll in multiple courses, and a course can
have multiple students.

Students
    ↕
Courses

### Implementation

A junction or bridge table is used.

Student_Course:

student_id
course_id

### Possible Follow-up Questions

- Why do we need a junction table?
- What is a composite key?

---

## Q21. What is a JOIN?

### Answer

A JOIN combines rows from two or more tables based on a
related column.

### Example

Students:

student_id | name | course_id

Courses:

course_id | course_name

We can join them using course_id.

### Common JOIN Types

- INNER JOIN
- LEFT JOIN
- RIGHT JOIN
- FULL OUTER JOIN
- CROSS JOIN

### Possible Follow-up Questions

- Explain INNER JOIN.
- INNER JOIN vs LEFT JOIN?
- What is SELF JOIN?

---

## Q22. What is an INNER JOIN?

### Answer

INNER JOIN returns only records that have matching values
in both tables.

### Example

Students
    INNER JOIN
Courses

Only students having a matching course record are returned.

### SQL

SELECT *
FROM students s
INNER JOIN courses c
ON s.course_id = c.course_id;

### Possible Follow-up Questions

- INNER JOIN vs LEFT JOIN?
- What happens when there is no match?

---

## Q23. What is a LEFT JOIN?

### Answer

LEFT JOIN returns all records from the left table and the
matching records from the right table.

If there is no match, the right-side columns contain NULL.

### Example

All students should be displayed even if they have not been
assigned a course.

### SQL

SELECT *
FROM students s
LEFT JOIN courses c
ON s.course_id = c.course_id;

### Possible Follow-up Questions

- LEFT JOIN vs INNER JOIN?
- When would you use LEFT JOIN?

---

## Q24. What is an index?

### Answer

An index is a database structure that improves the speed of
data retrieval.

### Explanation

Without an index, the database may need to scan many rows.

With an index, it can locate matching records more efficiently.

### Example

CREATE INDEX idx_email
ON users(email);

### Important Point

Indexes improve read performance but can increase storage and
write overhead.

### Possible Follow-up Questions

- What is a clustered index?
- What is a composite index?
- Can too many indexes be harmful?

---

## Q25. What is a transaction?

### Answer

A transaction is a sequence of database operations treated as
a single logical unit of work.

### Example

Bank transfer:

1. Deduct money from Account A.
2. Add money to Account B.

Both operations should succeed together.

### Transaction Commands

COMMIT
ROLLBACK
SAVEPOINT

### Possible Follow-up Questions

- What are ACID properties?
- What is rollback?
- What happens if a transaction fails?