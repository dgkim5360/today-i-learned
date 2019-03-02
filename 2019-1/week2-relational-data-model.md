## Week 2 - Relational Data Model and the CREATE TABLE Statement

### Basics of Relational Databases

##### Definitions & Composition
Relational database = collection of tables
Table = heading (definition part) + body (content part)
Heading = table name + column names

##### Relationships or Connections

Rows in a table are usually related to rows in other tables
matching or identical values indicate relationships between tables

Matching values: crucial concept in relational databases (join)

##### Alternative Terminology

Table-Oriented | Set-Oriented | Record-Oriented
===============================================
Table          | Relation     | Record Type, File
Row            | Tuple        | Record
Column         | Attribute    | Field
===============================================
End users      | Academic     | Information systems
               | researchers  | professionals

### Integrity Rules
ensure an essential level of validity for rows stored in tables

##### Entity Integrity: Primary Keys
* Each table must have a column or combination of columns, known as the primary key
* PK must have unique values with no rows having a missing value
* Ensure traceable entities
  For auditing, security and communication reasons,
  it is important that business entities are easily traceable and unique

##### Referential Integrity: Foreign Keys
* Ensure the correctness in matching values
* Ensure valid references among tables

##### Oracle Relational Diagram


### Basic SQL CREATE TABLE Statement

```
CREATE TABLE <table-name> ( <column-list> <constraint-list> );
```

Comma (`;`) is required to terminate each column definition.

##### Common SQL Data Types
- CHAR(Max Length): 항상 Max Length 만큼을 저장, e.g. 국가코드
- VARCHAR(Max Length): 받는 만큼만 저장
- INTEGER
- FLOAT(Precision)
- DECIMAL(W, R): 금액처럼 정해진 범위가 있는 숫자
- DATE, TIME, TIMESTAMP / DATE ( storing date + time)  ... 표준적이지가 않다
