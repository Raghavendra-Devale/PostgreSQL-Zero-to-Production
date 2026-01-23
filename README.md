
---
# 📚 PostgreSQL Zero → Production → Interview Syllabus (with PL/pgSQL)

This repository documents my structured learning of PostgreSQL from first principles to real-world backend and full-stack usage, with a focus on Java/Spring applications and production systems.

---

## Learning Progress

- [ ] What is Data
- [ ] What is a Database
- [ ] RDBMS Basics
- [ ] PostgreSQL Introduction
- [ ] Schema Design
- [ ] SQL Fundamentals
- [ ] Joins
- [ ] Indexes
- [ ] Transactions
- [ ] Query Optimization
- [ ] EXPLAIN / EXPLAIN ANALYZE
- [ ] Pagination
- [ ] PL/pgSQL
- [ ] PostgreSQL with Java & Spring
- [ ] Production & Interview Prep


## 0. Foundations (Absolute Zero)

* What is Data
* What is a Database
* File system vs Database
* Persistence and durability
* Role of database in full-stack systems
* OLTP vs OLAP (high level)

---

## 1. Relational Database Concepts (RDBMS)

* What is an RDBMS
* Tables, rows, columns
* Primary keys
* Foreign keys
* Relationships (1–1, 1–many, many–many)
* Referential integrity
* NULL vs NOT NULL

---

## 2. PostgreSQL Introduction

* What is PostgreSQL
* PostgreSQL architecture (high level)
* Client–server model
* PostgreSQL vs MySQL vs Oracle (overview)
* PostgreSQL data consistency guarantees

---

## 3. Schema Design & Data Modeling (CRITICAL)

* Identifying entities and attributes
* Choosing correct data types
* Normalization (1NF, 2NF, 3NF)
* Denormalization (when and why)
* Designing schemas for real applications
* Constraints:

  * PRIMARY KEY
  * FOREIGN KEY
  * UNIQUE
  * NOT NULL
  * CHECK
* Naming conventions
* Schema evolution & migrations

---

## 4. SQL Fundamentals

* SELECT, INSERT, UPDATE, DELETE
* WHERE clause
* ORDER BY
* LIMIT / OFFSET
* DISTINCT
* Aliases
* Expressions and operators

---

## 5. Joins & Relationships

* INNER JOIN
* LEFT JOIN
* RIGHT JOIN
* FULL JOIN
* Self joins
* Joining multiple tables
* Join vs subquery
* Common join pitfalls
* N+1 query problem

---

## 6. Aggregations & Grouping

* COUNT, SUM, AVG, MIN, MAX
* GROUP BY
* HAVING
* Aggregations with joins
* Real reporting queries

---

## 7. Indexes & Performance Basics

* What is an index
* How indexes work (B-Tree concept)
* Single-column indexes
* Composite indexes
* Unique indexes
* Index selectivity
* When indexes help
* When indexes hurt
* Index maintenance cost

---

## 8. Transactions & Concurrency

* What is a transaction
* ACID properties
* BEGIN, COMMIT, ROLLBACK
* Auto-commit behavior
* Transaction isolation levels
* Read phenomena (dirty read, non-repeatable read, phantom read)
* Locks (row-level, table-level)
* Deadlocks and avoidance

---

## 9. Query Optimization

* How PostgreSQL executes queries (high level)
* Cost-based optimizer
* Sequential scan vs index scan
* Common slow query causes
* Avoiding full table scans
* Optimizing joins
* Reducing data scanned

---

## 10. EXPLAIN & EXPLAIN ANALYZE

* What EXPLAIN does
* Reading execution plans
* Understanding:

  * Seq Scan
  * Index Scan
  * Nested Loop
  * Hash Join
* Using EXPLAIN ANALYZE in debugging
* Identifying bottlenecks

---

## 11. Pagination Strategies

* OFFSET–LIMIT pagination
* Problems with OFFSET
* Keyset (cursor-based) pagination
* Pagination with indexes
* Pagination in REST APIs

---

## 12. PL/pgSQL (PostgreSQL Procedural Language)

* What PL/pgSQL is
* PL/pgSQL vs SQL
* Functions vs Procedures
* Variables and data types
* Control structures:

  * IF / ELSE
  * CASE
  * LOOP / WHILE / FOR
* Exception handling
* Returning scalar values
* Returning tables (SETOF)
* Using functions in queries
* Performance implications of PL/pgSQL
* When to use logic in DB vs backend
* Common PL/pgSQL anti-patterns

---

## 13. Advanced PostgreSQL Features (Backend-Focused)

* Views
* Materialized views
* Functions & stored procedures (usage patterns)
* Triggers (high-level awareness)
* Sequences & auto-increment
* JSON / JSONB
* Basic full-text search

---

## 14. PostgreSQL with Java & Spring

* JDBC fundamentals
* Prepared statements
* Calling database functions from Java
* Connection pooling (HikariCP)
* Transaction management in Spring
* Spring Data JPA vs JDBC
* Native queries vs ORM queries
* Handling large result sets

---

## 15. Production & Real-World Considerations

* Connection limits
* Query timeouts
* Index strategy in production
* Schema migrations (Flyway / Liquibase concept)
* Handling data growth
* Backups & restores (conceptual)
* Read replicas (high level)

---

## 16. Common Mistakes & Anti-Patterns

* Over-indexing
* Under-indexing
* Business logic inside DB
* Excessive triggers
* Chatty database access
* Blind trust in ORM

---

## 17. Interview Preparation

* PostgreSQL vs PL/SQL vs PL/pgSQL (explicit clarity)
* Schema design interview questions
* Query optimization questions
* Transaction & isolation questions
* PL/pgSQL interview questions
* Real-world debugging scenarios

---

## 18. Practice & Validation

* Writing production-style SQL
* LeetCode SQL problems
* Schema design exercises
* Explaining execution plans verbally
* Mock interview explanations

---
