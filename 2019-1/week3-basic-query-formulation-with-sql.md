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


### JOIN Operator
Builds a new table by combining rows
from two tables that match on a join condition

##### Unqualified Column
Unqualified means the column name alone without the table.
특정 Table에 종속되지 않는 column
e.g. PK, FK

##### EQUI-JOIN (Equality Join)
When the join condition involves equality.
The join columns have the same unqualified name.
Typically, the join columns are a combination of PK and FK.


### Using JOIN Operations in SQL SELECT Statements

##### Cross Product Style
```
SELECT OfferNo, CourseNo, FacFirstName, FacLastName
FROM Offering, Faculty
WHERE OffTerm = 'FALL'
    AND OffYear = 2016
    AND FacRank = 'ASST'
    AND CourseNo LIKE 'IS%'
    AND Faculty.FacNo = Offering.FacNo  -- JOIN condition!
;
```
- Easy to read
- Table order is not important (알아서 잘 해준다)
- Error-prone
- Not efficient

```
SELECT OfferNo, Offering.CourseNo, OffDays,
    CrsUnits, OffLocation, OffTime
FROM Faculty, Course, Offering
WHERE Faculty.FacNo = Offering.FacNo
    AND Offering.CourseNo = Course.CourseNo
    AND OffYear = 2016
    AND OffTerm = 'FALL'
    AND FacFirstName = 'LEONARD'
    AND FacLastName = 'VINCE'
;
```

##### JOIN Operator Style
```
SELECT OfferNo, CourseNo, FacFirstName, FacLastName
FROM Offering
INNER JOIN Faculty
ON Faculty.FacNo = Offering.CourseNo
WHERE OffTerm = 'FALL'
    AND OffYear = 2016
    AND FacRank = 'ASST'
    AND CourseNo LIKE 'IS%'
```
- Table order is not important, again

```
SELECT OfferNo, Offering.CourseNo, OffDays,
    CrsUnits, OffLocation, OffTime
FROM Offering
INNER JOIN Course
ON Offering.CourseNo = Course.CourseNo
INNER JOIN Faculty
ON Faculty.FacNo = Offering.FacNo
WHERE OffYear = 2016
    AND OffTerm = 'FALL'
    AND FacFirstName = 'LEONARD'
    AND FacLastName = 'VINCE'
;
```

* JOIN style에 관계없이 N개 테이블의 JOIN을 위해서는
  N-1 개의 JOIN condition이 필요하다.
* 이를 위반하게 되면 심각한 오류가 발생한다.
  - 정확하지 않은 결과
  - 높은 수준의 자원 소비

##### Name Qualification
어느 테이블에 속한 column인지 몰라서 혼란스럽지 않도록 표기
```
ON Faculty.FacNo = Offering.CourseNo
```

Required in JOIN operation
