## Week 3 - Extended Query Formulation with SQL

### Query Formulation Guidelines

##### Query Formulation Process
- Problem Statement
- Database Representation (words -> database diagram)
- Database Language Statement

##### Efficiency Considerations
- Little concern for efficiency (thx to intelligent SQL compiler)
- Correct and non-redundant solution
  - No extra table
  - No unnecessary grouping
  - No missing join conditions


### Multiple Table Problems

##### Example 1: 3 Tables

```
SELECT
    OfferNo,
    Offering.CourseNo,
    CrsUnits,
    OffDays,
    OffLocations,
    OffTime
FROM Faculty, Course, Offering
WHERE Faculty.FacNo = Offering.FacNo
    AND Offering.CourseNo = Course.CourseNo
    AND OffYear = 2016
    AND OffTerm = 'FALL'
    AND FacFirstName = 'LEONARD'
    AND FacLastName = 'VINCE'
;
```

##### Example 2: 4 Tables

```
SELECT
    Offering.OfferNo,
    Offering.CourseNo,
    OffDays,
    OffLocations,
    OffTime
    FacFirstName,
    FacLastName
FROM Faculty, Offering, Enrollment, Student
WHERE Offering.OfferNo = Enrollment.OfferNo
    AND Student.StdNo = Enrollment.StdNo
    AND Faculty.FacNo = Offering.FacNo
    AND OffYear = 2017
    AND OffTerm = 'SPRING'
    AND FacFirstName = 'BOB'
    AND FacLastName = 'NORBERT'
;
```

- Have a mental image of the query formulation process
- Use critical questions for converting a problem statement into a database representation


### Problems Involving Joins and Grouping

##### Example 1: Joins and Summarization

```
SELECT Offering.OfferNo,
    COUNT(*) AS NumStudents,
    AVG(StdPGA) as AvgGPA
FROM Enrollment, Offering, Student
WHERE Offering.OfferNo = Enrollment.OfferNo
    AND Student.StdNo = Enrollment.StdNo
    AND OffYear = 2017
GROUP BY Offering.OfferNo
HAVING AVG(StdGPA) > 3.3
;
```

##### Example 2: Multiple Column Grouping

```
SELECT CourseNo, Enrollment.OfferNo, COUNT(*) AS NumStudents
FROM Offering, Enrollment
WHERE Offering.OfferNo = Enrollment.OfferNo
    AND OffYear = 2017
    AND OffTerm = 'SPRING'
GROUP BY Enrollment.OfferNo, CourseNo
;
```


### SQL SET Operators

##### Union Compatibility
UNION compatibility means that each table must have the same number of columns and
each corresponding column must have a compatible data type.
- Requirement for the traditional set operators
- Strong requirement
  - Same number of columns
  - Each corresponding column is compatible
  - Positional correspondence
- Apply to similar tables by removing columns first

##### Reality & Limitation & Use Cases
In practice, compatible data types mean the corresponding columns have the same
data type, except perhaps for the length specification.

In contrast, the joint operator involves a condition usuaully on a single column from each table
Compared to the join operator, the set operators are not widely used.

The UNION operator can be used to combine tables
distributed over multiple locations.

##### Example

```
SELECT
    FacNo AS PerNo,
    FacFirstName AS FirstName,
    FacLastName AS LastName,
    FacCity as City,
    FacState as State
    FROM Faculty
UNION
SELECT
    StdNo AS PerNo,
    StdFirstName AS FirstName,
    StdLastName AS LastName,
    StdCity AS City,
    StdState AS State
FROM Student
;
```

`INTERSECT`, `MINUS`도 있다
- Oracle only
- Also requires Uion compatibility
- `MINUS` 대신 SQL standard에서는 `EXCEPT`


### SQL Modification Statements

##### INSERT

```
INSERT INTO Student
(
    StdNo, StdFirstName, StdLastName,
    StdCity, StdState, StdZip,
    StdClass, StdMajor, StdGPA
)
VALUES
(
    '999-99-9999', 'JOE', 'STUDENT',
    'SEATAC', 'WA', '98042-1121',
    'FR', 'IS', 0.0
)
;
```

Specifying the followings is not standard across DBMSs
- the format of constant values
- null values

##### UPDATE

```
UPDATE Student
SET
(
    StdMajor = 'ACCT',
    StdClass = 'SO'
)
WHERE
    StdFirstName = 'JOE'
    AND StdLastName = 'STUDENT'
;
```

Changing PK values should be avoided if possible since
- update rules on reference rows may not allow the operation.
- it is complex for a parent table if related child rows exist.

##### DELETE

```
DELETE FROM Student
WHERE
    StdFirstName = 'JOE'
    AND StdLastName = 'STUDENT'
;
```

The DELETE statement is subject to the rules on referenced rows.
- e.g., a student row cannot be deleted if related enrollment rows exists
  and deletion action is restrict.
- Typically rows in a child table should be deleted
  before associated rows in a parent table.


### Query Formulation Errors

##### Impact of Errors
1. Syntax Error
- No execution, compiler가 실행 전에 잡아줌
- Sometimes confusing message
- e.g.
  - Misspelled keyword
  - Missing table
  - Unqualified column name

여기서부터는 compiler가 못 잡아서 실행되는 에러
2. Redundancy
- Execution with correct rows
- Excessive resource usage
- e.g.
  - Extra table
  - Unneeded GROUP BY clause

3. Semantic
- Execution with incorrect rows
- Sometimes excessive resource usage
- e.g.
  - Missing join or row condition, SERIOUS ERROR!
  - Missing parentheses

##### Poor Coding Practices
- Mixed join styles
- Incompatible constant
- `LIKE` operator in date comparison
- Poor clause alignment
- Incompatible constant
- `LIKE` operator without pattern matching characters

##### Summary
- The most serious error: Missing join conditions
- The most subtle error: semantic error
  that generates anticipated rows in the result
- DB error로 일자리를 잃을 수도 있단다
  
