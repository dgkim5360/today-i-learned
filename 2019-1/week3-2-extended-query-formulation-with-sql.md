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
