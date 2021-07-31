# SQL
---

### Structured Query Language (SQL)
- Standardized language for interacting w/ RDBMS
- used to perform CRUD operations and other admin tasks(e.g user managment, security, backup, etc)
- SQL code on one RDBMS might not be portable to a different RDBMS b/c SQL implementations vary btw systems
---
### 4 Types of Languages in SQL:
1. **Data Query Language (DQL)**- queries the DB for stored info
3. **Data Definition Language (DDL)**- defines database schemas 
4. **Data Control Language (DCL)**- controls access to data in DB & manages users and permissions
5. **Data Manipulation Laguage (DML)**- inserts, updates, and deletes data from DB
---
### Database Queries
- Requests made to RDBMS for specific info
- Become more complex as DB's structure grows 

---
## Keys 
---
**Primary Key**- attribute that is unique for each row in the table

**Surrogate Key**- type of primary key that has no mapping to anything in the real world 

**Natural Key**- type of primary key that has a mapping to the real world (e.g. SSN)

**Foreign Key**- stores the primary key of a row in another database table (Link to another table)
  - Defines relationships btw two tables
    - Can define relationships w/in a table using foreign keys
  - Can have multiple foreign keys in a table
  
**Composite Key**- type of primary key that is made up of two attributes
  - Used when either of the attributes on their own do not uniquely identify a row
