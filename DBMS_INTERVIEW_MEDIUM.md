# DBMS — TECHNICAL INTERVIEW QUESTIONS
# MEDIUM SET — 25 QUESTIONS

---

## Q1. Explain the ACID properties of a transaction.

### Answer

ACID stands for:

A → Atomicity
C → Consistency
I → Isolation
D → Durability

### Explanation

Atomicity:
A transaction is completed fully or not at all.

Consistency:
A transaction takes the database from one valid state to
another valid state.

Isolation:
Concurrent transactions should not improperly interfere
with each other.

Durability:
Once a transaction is committed, its changes should survive
system failures.

### Example

In a bank transfer, both debit and credit operations must
be completed together.

### Possible Follow-up Questions

- Explain each property with an example.
- How is isolation implemented?
- What is durability?

---

## Q2. What is Atomicity?

### Answer

Atomicity means that all operations in a transaction either
succeed together or fail together.

### Example

Transfer ₹100:

1. Deduct ₹100 from A.
2. Add ₹100 to B.

If step 2 fails, step 1 must also be rolled back.

### Possible Follow-up Questions

- How is atomicity achieved?
- What is rollback?
- What happens after a transaction failure?

---

## Q3. What is Consistency?

### Answer

Consistency ensures that a transaction moves the database
from one valid state to another valid state while respecting
all defined constraints.

### Example

If an account balance cannot be negative, a transaction that
violates this rule should not be committed.

### Possible Follow-up Questions

- What are database constraints?
- How does a transaction maintain consistency?

---

## Q4. What is Isolation?

### Answer

Isolation ensures that concurrent transactions do not
incorrectly interfere with each other's intermediate states.

### Example

If two users update the same bank account simultaneously,
the database must ensure that the final result is correct.

### Possible Follow-up Questions

- What are isolation levels?
- What is dirty read?
- What is a lost update?

---

## Q5. What is Durability?

### Answer

Durability means that once a transaction is successfully
committed, its changes should remain stored even if a system
crash occurs afterward.

### Explanation

Databases typically use mechanisms such as transaction logs
and recovery systems to support durability.

### Possible Follow-up Questions

- What is a transaction log?
- How does recovery work?

---

## Q6. What is a deadlock?

### Answer

A deadlock occurs when two or more transactions wait for
resources held by each other and none of them can proceed.

### Example

Transaction T1 locks Resource A and waits for Resource B.

Transaction T2 locks Resource B and waits for Resource A.

T1
 ↓ waits for B

T2
 ↓ waits for A

Neither can continue.

### Possible Follow-up Questions

- How can deadlocks be prevented?
- How can deadlocks be detected?
- What is deadlock avoidance?

---

## Q7. What is a dirty read?

### Answer

A dirty read occurs when one transaction reads data that has
been modified by another transaction but has not yet been
committed.

### Example

T1 updates a balance.

T2 reads the new balance.

T1 rolls back.

T2 has read data that never became permanent.

### Possible Follow-up Questions

- Which isolation level prevents dirty reads?
- What is a non-repeatable read?

---

## Q8. What is a non-repeatable read?

### Answer

A non-repeatable read occurs when the same transaction reads
the same row twice and gets different values because another
transaction modified and committed the row between the reads.

### Example

T1 reads:

balance = 1000

T2 updates:

balance = 1500

T1 reads again:

balance = 1500

The same query produced different values.

### Possible Follow-up Questions

- Dirty read vs non-repeatable read?
- Which isolation level prevents it?

---

## Q9. What is a phantom read?

### Answer

A phantom read occurs when a transaction executes the same
range query twice and new or removed rows appear because
another transaction inserted or deleted matching rows.

### Example

T1:

SELECT * FROM employees
WHERE salary > 50000;

T2 inserts another employee with salary > 50000.

T1 executes the same query again and sees an additional row.

### Possible Follow-up Questions

- Phantom read vs non-repeatable read?
- Which isolation level prevents phantom reads?

---

## Q10. What are transaction isolation levels?

### Answer

Isolation levels define how much one transaction is isolated
from the effects of other concurrent transactions.

Common levels are:

1. Read Uncommitted
2. Read Committed
3. Repeatable Read
4. Serializable

### Explanation

Higher isolation generally provides stronger consistency but
can reduce concurrency.

### Possible Follow-up Questions

- Which level allows dirty reads?
- Which is the strongest isolation level?
- What is the default level in your database?

---

## Q11. What is normalization and why is it important?

### Answer

Normalization is the process of organizing database tables
to reduce redundancy and prevent data anomalies.

### Benefits

- Less duplicate data
- Better consistency
- Easier maintenance
- Improved data integrity

### Possible Follow-up Questions

- Explain 1NF, 2NF and 3NF.
- What are update anomalies?
- When would you denormalize?

---

## Q12. Explain First Normal Form (1NF).

### Answer

A table is in 1NF when each column contains atomic values
and there are no repeating groups.

### Example

Bad design:

student_id | phones
1          | 9876, 8765

Better design:

student_id | phone
1          | 9876
1          | 8765

### Possible Follow-up Questions

- What is atomicity in 1NF?
- What is 2NF?

---

## Q13. Explain Second Normal Form (2NF).

### Answer

A table is in 2NF when it is in 1NF and every non-key
attribute is fully dependent on the entire primary key.

2NF mainly matters when a table has a composite key.

### Example

If the key is:

(student_id, course_id)

and student_name depends only on student_id, then there is
a partial dependency.

### Possible Follow-up Questions

- What is partial dependency?
- Explain 3NF.

---

## Q14. Explain Third Normal Form (3NF).

### Answer

A table is in 3NF when it is in 2NF and has no transitive
dependency of non-key attributes on the primary key.

### Example

Student:

student_id
department_id
department_name

department_name depends on department_id rather than directly
on student_id.

This can be separated into another table.

### Possible Follow-up Questions

- What is transitive dependency?
- 2NF vs 3NF?
- What is BCNF?

---

## Q15. What is denormalization?

### Answer

Denormalization is intentionally introducing some redundancy
into a database to improve read performance or simplify
queries.

### Example

Instead of joining several tables repeatedly, frequently
used information may be stored together.

### Advantage

Faster reads in some workloads.

### Disadvantage

More redundancy and greater risk of inconsistent data.

### Possible Follow-up Questions

- When would you denormalize?
- Normalization vs denormalization?
- Does denormalization always improve performance?

---

## Q16. What is a composite key?

### Answer

A composite key consists of two or more columns that together
uniquely identify a record.

### Example

Student_Course:

student_id
course_id

The combination:

(student_id, course_id)

can uniquely identify an enrollment.

### Possible Follow-up Questions

- Why use composite keys?
- Composite key vs surrogate key?
- Can a foreign key reference a composite key?

---

## Q17. What is a self join?

### Answer

A self join is a join where a table is joined with itself.

### Example

An Employee table may contain:

employee_id
name
manager_id

To find each employee's manager, the Employee table can be
joined with itself.

### SQL

SELECT e.name, m.name
FROM employees e
JOIN employees m
ON e.manager_id = m.employee_id;

### Possible Follow-up Questions

- Give a real-world use case.
- Can a self join be an outer join?

---

## Q18. What is a subquery?

### Answer

A subquery is a query nested inside another SQL query.

### Example

SELECT name
FROM employees
WHERE salary >
(
    SELECT AVG(salary)
    FROM employees
);

### Explanation

The inner query calculates the average salary and the outer
query finds employees earning more than that average.

### Possible Follow-up Questions

- Subquery vs JOIN?
- What is a correlated subquery?
- Which is generally faster?

---

## Q19. What is a correlated subquery?

### Answer

A correlated subquery is a subquery that depends on a value
from the outer query and is logically evaluated for each
relevant outer row.

### Example

SELECT e.name
FROM employees e
WHERE salary >
(
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);

### Possible Follow-up Questions

- Correlated vs non-correlated subquery?
- Can a correlated subquery be optimized?

---

## Q20. What is the difference between WHERE and HAVING?

### Answer

WHERE filters individual rows before grouping.

HAVING filters groups after GROUP BY is applied.

### Example

WHERE:

SELECT *
FROM employees
WHERE salary > 50000;

HAVING:

SELECT department_id, AVG(salary)
FROM employees
GROUP BY department_id
HAVING AVG(salary) > 50000;

### Possible Follow-up Questions

- Can WHERE be used with aggregate functions?
- WHERE vs HAVING performance?

---

## Q21. What is GROUP BY?

### Answer

GROUP BY groups rows that have the same values in specified
columns so aggregate functions can be applied to each group.

### Example

SELECT department_id, AVG(salary)
FROM employees
GROUP BY department_id;

### Explanation

This calculates the average salary for each department.

### Possible Follow-up Questions

- GROUP BY vs ORDER BY?
- Can GROUP BY use multiple columns?
- What is HAVING?

---

## Q22. What are aggregate functions?

### Answer

Aggregate functions perform calculations on multiple rows
and return a single result per group.

### Common Functions

COUNT()
SUM()
AVG()
MIN()
MAX()

### Example

SELECT AVG(salary)
FROM employees;

### Possible Follow-up Questions

- COUNT(*) vs COUNT(column)?
- Can aggregate functions be used with GROUP BY?

---

## Q23. What is the difference between DELETE, TRUNCATE and DROP?

### Answer

DELETE removes selected rows and can use a WHERE condition.

TRUNCATE removes all rows from a table.

DROP removes the table structure itself.

### Example

DELETE:

DELETE FROM students
WHERE id = 10;

TRUNCATE:

TRUNCATE TABLE students;

DROP:

DROP TABLE students;

### Possible Follow-up Questions

- Which is faster?
- Can DELETE be rolled back?
- What happens to indexes?

---

## Q24. What is a view?

### Answer

A view is a virtual table based on the result of a SQL query.

### Example

CREATE VIEW employee_details AS
SELECT name, salary
FROM employees;

### Benefits

- Simplifies complex queries
- Provides controlled access
- Hides unnecessary columns
- Improves query abstraction

### Possible Follow-up Questions

- Is a view physically stored?
- What is a materialized view?
- Can we update a view?

---

## Q25. What is a stored procedure?

### Answer

A stored procedure is a pre-defined set of SQL statements
stored in the database that can be executed when required.

### Benefits

- Reusable database logic
- Centralized processing
- Can reduce repeated application-side logic
- Can improve security in some designs

### Possible Follow-up Questions

- Stored procedure vs function?
- What are the disadvantages?
- When should business logic stay in the application?
