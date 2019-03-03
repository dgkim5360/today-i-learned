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
| Statement | Statement Type |
| --------- | -------------- |
| CREATE TABLE | Definition, Control |
| CREATE VIEW | Definition |
| CREATE TYPE | Definition |
| SELECT | Manipulation |
| INSERT | Manipulation |
| UPDATE | Manipulation |
| DELETE | Manipulation |
| COMMIT | Manipulation |
| ROLLBACK | Manipulation |
| CREATE TRIGGER | Control, Manipulation |
| GRANT | Control |
| REVOKE | Control |

##### Weakness: Lack of Conformance Testing
표준화가 엉망이다 맨이야: Higher switching cost


### SELECT Statement Introduction

```
SELECT <list of column expression>
FROM <list of tables and JOIN operations>
WHERE <list of logical expressions for rows>
ORDER BY <list of sorting specifications>
```

##### Additional Keywords
- `AND`, `OR`
- `DISTINCT`: Remove duplicated rows
- `AS`: Rename a column
- `LIKE`: Inexact string matching
  `DATE` 타입에는 쓰지 말자: Treat date columns as numeric, not text!
- `BETWEEN ... AND ...`
- `IS NULL`: Testing the lack of a value

##### Portability Issue
the SELECT statements are not portable across Oracle and MySQL
because of the different date functions in the two DBMS's.
- Oracle: `to_char`, `to_number`
- MySQL: `date_format`
