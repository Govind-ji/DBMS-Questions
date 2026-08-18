# DBMS — TECHNICAL INTERVIEW QUESTIONS
# HARD SET — 25 QUESTIONS

---

## Q1. How does a database index work internally?

### Answer

An index is a separate data structure that stores indexed
values along with references to the corresponding table rows.

Many relational databases use B-tree or B+ tree structures
for common indexes.

### Explanation

Without an index:

Query
    ↓
Scan many rows
    ↓
Find matching rows

With an index:

Query
    ↓
Index
    ↓
Locate matching entries
    ↓
Access required rows

### Important Point

Indexes improve read performance but require additional storage
and can make INSERT, UPDATE, and DELETE operations more
expensive.

### Possible Follow-up Questions

- B-tree vs B+ tree?
- What is an index scan?
- What is a covering index?

---

## Q2. What is a clustered index?

### Answer

A clustered index determines how table data is physically or
logically organized according to the indexed key, depending
on the database implementation.

Because the table data itself is closely associated with the
clustered ordering, there is generally a limitation on having
multiple clustered organizations for the same table.

### Explanation

A clustered index can be very useful for range queries.

### Example

Searching:

WHERE employee_id BETWEEN 100 AND 200

can benefit when the data is organized efficiently around
employee_id.

### Possible Follow-up Questions

- Clustered vs non-clustered index?
- Can a table have multiple clustered indexes?
- How does PostgreSQL implement indexes differently?

---

## Q3. What is a non-clustered index?

### Answer

A non-clustered index is a separate structure that stores
indexed values and references to the corresponding table data.

### Explanation

The table's physical organization does not necessarily follow
the order of the non-clustered index.

### Example

A users table may have separate indexes on:

email
username
created_at

### Possible Follow-up Questions

- Clustered vs non-clustered?
- Can multiple non-clustered indexes exist?
- What is a covering index?

---

## Q4. What is a composite index?

### Answer

A composite index is an index created on multiple columns.

### Example

CREATE INDEX idx_employee_dept_salary
ON employees(department_id, salary);

### Explanation

The order of columns in a composite index matters.

An index on:

(department_id, salary)

is not equivalent to:

(salary, department_id)

for every query pattern.

### Possible Follow-up Questions

- How does column order matter?
- What is the leftmost-prefix principle?
- When should you create a composite index?

---

## Q5. What is a covering index?

### Answer

A covering index contains all the columns required by a query,
allowing the database to obtain the required information from
the index without accessing the underlying table in some
database systems and query plans.

### Example

Query:

SELECT name, salary
FROM employees
WHERE department_id = 10;

An index containing department_id, name, and salary may be able
to satisfy the query efficiently.

### Possible Follow-up Questions

- Does every covering index improve performance?
- What is an index-only scan?
- What is the storage cost?

---

## Q6. What is a query execution plan?

### Answer

A query execution plan describes how the database intends to
execute a SQL query.

### Explanation

The database optimizer may choose operations such as:

- Sequential scan
- Index scan
- Join
- Sort
- Aggregate
- Hash operation

### Example

EXPLAIN
SELECT *
FROM employees
WHERE department_id = 10;

The output helps analyze how the database executes the query.

### Possible Follow-up Questions

- What is EXPLAIN ANALYZE?
- How do you optimize a slow query?
- What is a sequential scan?

---

## Q7. How would you optimize a slow SQL query?

### Answer

I would first inspect the execution plan and identify the
bottleneck.

### Steps

1. Analyze the query.
2. Run EXPLAIN or equivalent.
3. Check indexes.
4. Check join conditions.
5. Reduce unnecessary columns.
6. Reduce unnecessary rows.
7. Check filtering.
8. Review database statistics.
9. Consider query restructuring.
10. Re-test performance.

### Example

Instead of:

SELECT *

I would select only required columns when appropriate.

### Possible Follow-up Questions

- What is EXPLAIN ANALYZE?
- When can an index make a query slower?
- How do you optimize JOINs?

---

## Q8. Why might a database ignore an index?

### Answer

A database optimizer may choose not to use an index when it
estimates that another execution strategy will be cheaper.

### Possible Reasons

- Too many matching rows
- Poor selectivity
- Small table
- Function applied to indexed column
- Type mismatch
- Outdated statistics
- Query structure
- Cost of random table access

### Example

If 90% of rows match a condition, scanning the table may be
cheaper than using an index.

### Possible Follow-up Questions

- What is selectivity?
- How do statistics affect query planning?
- How do you investigate this?

---

## Q9. What is database normalization up to BCNF?

### Answer

Normalization organizes tables to reduce redundancy and
dependency problems.

### 1NF

Atomic values.

### 2NF

1NF + no partial dependency on a composite key.

### 3NF

2NF + no transitive dependency of non-key attributes.

### BCNF

For every non-trivial functional dependency:

X → Y

X must be a super key.

### Possible Follow-up Questions

- 3NF vs BCNF?
- Give an example where 3NF is not BCNF.
- Why can BCNF sometimes be difficult to achieve?

---

## Q10. What is a functional dependency?

### Answer

A functional dependency describes a relationship where one
attribute determines another.

It is represented as:

X → Y

meaning the value of X determines the value of Y.

### Example

student_id → student_name

If student_id uniquely identifies a student, then the
student_id determines the student's name.

### Possible Follow-up Questions

- What is a partial dependency?
- What is a transitive dependency?
- How is functional dependency used in normalization?

---

## Q11. What is a transaction schedule?

### Answer

A transaction schedule describes the order in which operations
from multiple transactions are executed.

### Example

T1: Read A
T2: Read A
T1: Write A
T2: Write A

The order can affect the final result.

### Possible Follow-up Questions

- What is serial schedule?
- What is concurrent schedule?
- What is serializability?

---

## Q12. What is serializability?

### Answer

Serializability is a property that ensures the result of a
concurrent transaction schedule is equivalent to some valid
serial execution of those transactions.

### Explanation

Concurrent execution:

T1 + T2

should produce a result equivalent to some serial order:

T1 → T2

or:

T2 → T1

### Possible Follow-up Questions

- What is conflict serializability?
- What is view serializability?
- Why is serializability important?

---

## Q13. What is conflict serializability?

### Answer

A schedule is conflict-serializable if it can be transformed
into a serial schedule by swapping non-conflicting operations.

### Explanation

Two operations conflict when:

- They belong to different transactions.
- They access the same data item.
- At least one operation is a write.

### Possible Follow-up Questions

- How do you test conflict serializability?
- What is a precedence graph?
- What does a cycle mean?

---

## Q14. What is a precedence graph?

### Answer

A precedence graph is a directed graph used to analyze
conflict serializability.

### Explanation

Each transaction is represented as a node.

An edge:

T1 → T2

means an operation of T1 must occur before a conflicting
operation of T2.

### Important Rule

If the graph contains a cycle, the schedule is not
conflict-serializable.

### Possible Follow-up Questions

- How do you construct the graph?
- What does an edge represent?
- What does a cycle indicate?

---

## Q15. Explain two-phase locking (2PL).

### Answer

Two-phase locking is a concurrency-control protocol in which
a transaction has two phases:

1. Growing phase
2. Shrinking phase

### Growing Phase

The transaction can acquire locks but cannot release them.

### Shrinking Phase

The transaction can release locks but cannot acquire new ones.

### Explanation

2PL helps ensure conflict serializability.

### Possible Follow-up Questions

- What is strict 2PL?
- What is shared lock?
- What is exclusive lock?
- Can 2PL cause deadlocks?

---

## Q16. What is a shared lock and exclusive lock?

### Answer

A shared lock allows multiple transactions to read a resource
but prevents conflicting writes.

An exclusive lock allows a transaction to modify the resource
and prevents other conflicting access.

### Example

Shared lock:

T1 → Read
T2 → Read

Both can potentially read.

Exclusive lock:

T1 → Write

Other conflicting operations must wait.

### Possible Follow-up Questions

- Shared vs exclusive lock?
- What is lock compatibility?
- What is lock escalation?

---

## Q17. What is deadlock and how can it be handled?

### Answer

A deadlock occurs when transactions wait indefinitely for
resources locked by each other.

### Example

T1 holds A and waits for B.

T2 holds B and waits for A.

### Handling Techniques

- Deadlock prevention
- Deadlock avoidance
- Deadlock detection
- Timeout
- Transaction rollback

### Possible Follow-up Questions

- What are the four necessary conditions for deadlock?
- What is wait-for graph?
- How do databases detect deadlocks?

---

## Q18. What are the four necessary conditions for deadlock?

### Answer

The four Coffman conditions are:

1. Mutual exclusion
2. Hold and wait
3. No preemption
4. Circular wait

### Explanation

A deadlock can occur when all four conditions exist
simultaneously.

### Possible Follow-up Questions

- How can each condition be prevented?
- Which condition is easiest to break?
- How does a database detect circular wait?

---

## Q19. Explain MVCC.

### Answer

MVCC stands for Multi-Version Concurrency Control.

It allows transactions to work with different versions of
data so that readers and writers can often operate concurrently
with less blocking.

### Explanation

Instead of every reader waiting for a writer, the database can
provide a suitable committed version of the data.

### Example

T1 reads an older consistent version while T2 updates a newer
version.

### Possible Follow-up Questions

- Which databases use MVCC?
- How does PostgreSQL use MVCC?
- MVCC vs locking?

---

## Q20. What is a database transaction log?

### Answer

A transaction log records information about database changes
and transactions so the database can support recovery after
failures.

### Explanation

A simplified idea is:

Transaction
    ↓
Log Changes
    ↓
Commit
    ↓
Persistent State

If a crash occurs, the database can use recovery mechanisms
based on the log.

### Possible Follow-up Questions

- What is Write-Ahead Logging?
- How does recovery work?
- What is redo and undo?

---

## Q21. What is Write-Ahead Logging (WAL)?

### Answer

Write-Ahead Logging means the required log information is
written to durable storage before the corresponding database
changes are considered safely persisted.

### Explanation

The principle is:

Log first
    ↓
Data change

This allows recovery mechanisms to determine what changes
need to be redone or undone after a failure.

### Possible Follow-up Questions

- Why is WAL important?
- How does PostgreSQL use WAL?
- What are redo and undo operations?

---

## Q22. What is database replication?

### Answer

Database replication means maintaining copies of database
data on multiple servers.

### Example

Primary Database
    ↓
Replica 1
    ↓
Replica 2

### Benefits

- High availability
- Read scaling
- Disaster recovery
- Fault tolerance

### Possible Follow-up Questions

- Synchronous vs asynchronous replication?
- Primary vs replica?
- What happens if the primary fails?

---

## Q23. What is sharding?

### Answer

Sharding is the process of distributing database data across
multiple independent database servers or partitions.

### Example

Users with IDs 1–1,000,000
    ↓
Shard 1

Users with IDs 1,000,001–2,000,000
    ↓
Shard 2

### Benefits

- Horizontal scalability
- Distribution of workload
- Handling very large datasets

### Challenges

- Cross-shard queries
- Data distribution
- Rebalancing
- Transactions across shards

### Possible Follow-up Questions

- Sharding vs replication?
- What is a shard key?
- What makes a good shard key?

---

## Q24. What is CAP theorem?

### Answer

CAP theorem states that a distributed data system cannot
simultaneously guarantee all three of the following during
a network partition:

C → Consistency
A → Availability
P → Partition tolerance

### Explanation

During a network partition, a distributed system generally
has to choose between stronger consistency and availability.

### Important Point

Partition tolerance is generally required in distributed
systems because network failures can occur.

### Possible Follow-up Questions

- CP vs AP?
- Give examples.
- Is CAP applicable to every database?

---

## Q25. How would you design a database for an interview system
like Aarambh?

### Answer

I would separate the major entities and define clear
relationships between them.

### Possible Tables

Users
    ↓
Candidates
    ↓
Interviews
    ↓
Questions
    ↓
Answers
    ↓
Evaluations

Additional tables could include:

- Roles
- JobDescriptions
- Skills
- InterviewSessions
- InterviewResults

### Example Relationships

One candidate
    ↓
Many interviews

One interview
    ↓
Many questions

One question
    ↓
One or more candidate answers

One answer
    ↓
One evaluation

### Explanation

I would use primary keys and foreign keys to maintain
relationships and indexes on frequently queried columns.

I would normalize the transactional data initially and
denormalize only where performance requirements justify it.

### Possible Follow-up Questions

- What would be the primary keys?
- What would be the foreign keys?
- How would you index the tables?
- How would you handle many-to-many relationships?
- How would you scale the database?
- Would you use SQL or NoSQL?