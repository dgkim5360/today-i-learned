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
