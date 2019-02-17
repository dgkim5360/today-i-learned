## Week 1 - Introduction to Databases and DBMSs

이 강의에서는 DB를 Business 관점에서 보는 문맥에서의 DB로 한정한다.

### Database Characteristics
따라서 여기서는 Business 관점에서 보는 DB의 특성이다.

* Persistency: 오래 잘 보관되어야 한다.
* Inter-related: 아이템 간의 관계성이 저장되어야 한다.
* Shared: 동시에 다수의 사용자가 접근하고 사용할 수 있어야 한다.

### Organization Roles
DB를 사용하는 여러 역할들
* Functional Departments
  * Indirect User: DB로부터 추출되어 정리된 데이터를 받아보는 사람
  * Parameteric User: 특정 parameter를 요청하여 데이터를 받아보는 사람
  * Power User: 본인이 직접 SQL을 능숙하게 사용하여 복잡한 데이터를 추출할 수 있는 사람
* Information Technology
  * Data Specialist: DBA
  * Developer: 우리들
  * Management: DB 개발을 관리하는 사람

당신은 DB와 관련해서 어떤 분야에서 일하고 싶은 것인지 잘 생각해보랍니다.
people skills and interaction vs. technical skills and tasks

### DBMS Overview and Database Definition Feature
DBMS는 다음과 같은 일을 할 수 있어야 한다.
* Data Acquisition
* Dissemination
* Storage
* Maintenance
* Retrieval
* Formatting

DB의 종류
* Enterprise DBMS: Oracle, IBM, Microsoft, SAP, Teradata, MySQL 등
* Desktop DBMS: MS Access
* Embedded DBMS: Mobile 시장이 성장하면서 대두됨

DB의 정의: Desktop Application인 Spread Sheet, Word Processor와 어떻게 다른가
* __Planning is essential__
* Table과 Releationship
* SQL (Structured Query Language) 및 GUI

### Non-Procedural Access

Non-procedural Access가 뭐냐?
* Computing skill이 부족한 사람도 DB에 query를 무사히 날릴 수 있게 하는 개념
* 무엇을 가져올 지에 집중하지, 어떻게 가져올 지에 집중하지 않도록 함
* 특히 반복문의 개념이 없어서 길면서도 복잡한 코드를 짤 수 없도록 함
100배의 생산성 증가를 가져온 개념

Procedural Language Interface: Non-procedural Access만으로 힘들 때
* Batch Processing
* Customization / Automation
* Performance 향상
