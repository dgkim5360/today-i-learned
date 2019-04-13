## Week 6 - Schema Conversion

### Goals and Steps of Logical Database Design

##### Managing Redundancy
Is the main theme of the logical DB design.

- Identify possible redundancy
- Eliminate unwanted redundancy
- Support organizational policies
- Update orientation

##### Logical Database Design Phases

- Convert: ERD to initial table design
- Specify: Redundancy constraints
- Normalize: Eliminate unwanted redundancies
- Refine: Unqiueness constraints, other constraints


### Conversion Rules

##### Entity Type Rule: Entity type => Table
- PK of entity type => PK of table (unless weak)
- Attributes of entity type => Columns in table

##### 1-M Relationship Rule: Relationship => FK
- FK should be placed in a child table

##### M-M Relationship Rule: Relationship => Combined PK
- Attributes in M-M relationship => Columns in table

##### Identification Dependency Rule
- Add components to PK of table

##### Exercise

![](images/conversion-rules-1.png)

![](images/conversion-rules-2.png)

![](images/conversion-rules-3.png)
