## Week 4 - ERD Rules and Problem Solving

### Basic Diagram Rules

##### Diagram Rules

- Computer 언어의 syntax error와 같은 맥락
- Completeness rules ensure no missing specifications

##### Completeness Rules
- Primary Key Rule: All entity types have a PK (direct or indirect).
- Naming Rule: All entity types, relationships, and attributes have a name.
- Cardinality Rule: Cardinality is specified in both directions for each relationship.
- Entity Participate Rule (optional): All entity types participate in at least one relationship.

##### Issues on PK Rule
- Simple in most cases
- Subtle for some weak entity types
  - e.g., weak entity type with only one 1-M identifying relationship
  - Then, this must have a local key + borrowed PK from the parent entity type
  - Violation of PK Rule if local key is missing
