## Week 3 - Basic Query Formulation with SQL

### SQL Overview

##### SQL: Structured Query Language
A computer language containing statements for database
- definition: create objects (e.g. tables)
- control: ensure proper usage of database (e.g. row integrity, security)
- and manipulation: retrieve or change rows

##### 2 Contexts in Usage
- Stand-alone context: Workbench에서 직접 실행
- Embedded context: Django가 query를 요청하고, Django가 결과를 받아준다

##### Major SQL Statements
Statement      | Statement Type
===============================
CREATE TABLE   | Definition, Control
CREATE VIEW    | Definition
CREATE TYPE    | Definition
SELECT         | Manipulation
INSERT         | Manipulation
UPDATE         | Manipulation
DELETE         | Manipulation
COMMIT         | Manipulation
ROLLBACK       | Manipulation
CREATE TRIGGER | Control, Manipulation
GRANT          | Control
REVOKE         | Control

##### Weakness: Lack of Conformance Testing
표준화가 엉망이다 맨이야
Higher switching cost
