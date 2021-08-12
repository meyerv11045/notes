## Structured Query Language (SQL)
- Standardized language for interacting w/ RDBMS
- used to perform CRUD operations and other admin tasks(e.g user managment, security, backup, etc)
- SQL code on one RDBMS might not be portable to a different RDBMS b/c SQL implementations vary btw systems

## 4 Types of Languages in SQL:
1. **Data Query Language (DQL)**- queries the DB for stored info
3. **Data Definition Language (DDL)**- defines database schemas 
4. **Data Control Language (DCL)**- controls access to data in DB & manages users and permissions
5. **Data Manipulation Laguage (DML)**- inserts, updates, and deletes data from DB

## Keys 
- **Primary Key**- attribute that is unique for each row in the table
    - **Surrogate Key**- type of primary key that has no mapping to anything in the real world 
    - **Natural Key**- type of primary key that has a mapping to the real world (e.g. SSN)
- **Foreign Key**- stores the primary key of a row in another database table (Link to another table)
    - Can define relationships between tables or within a table
- **Composite Key**- type of primary key that is made up of two attributes
    - Used when either of the attributes on their own do not uniquely identify a row

## Datatypes 
```SQL
INT
DECIMAL(M,N)  -- m: total # digits, n: # digits after decimal place
VARCHAR(L)    -- String of text of max length L
BLOB          -- Binary large objects, stores large data like images
DATE          -- 'YYYY-MM-DD'
TIMESTAMP     -- 'YYYY-MM-DD HH:MM:SS'
```

## Functions
```SQL
--Find Num of Students
SELECT COUNT(student_id)
FROM students;

--Find Num of female student born after 1980
SELECT COUNT(student_id)
FROM students
WHERE sex = 'F' AND birth_date > '1981-01-01';

--Find avg male salary
SELECT AVG(salary)
FROM employees
WHERE sex = 'M';

--Find sum of all salaries
SELECT SUM(salary)
FROM employees;

--Find num of males & females
SELECT COUNT(sex), sex
FROM employe
GROUP BY sex; --Group By command used for aggregation
```

## Queries
```SQL
SELECT student.name AS forename, student.major
FROM student 
ORDER BY name DESC --Descending alphabetical order
LIMIT 20; --limits # of entries returned

-- Comparison Operators: <, >, <=, >=, =, AND, OR, <> (not equal to)
```

## Tables
```SQL
CREATE TABLE student (
  student_id INT AUTO_INCREMENT, -- you don't have to insert a primary key b/c its auto incremented
  name VARCHAR(20) UNIQUE, 
  major VARCHAR(20) DEFAULT 'undecided', 
  PRIMARY KEY(student_id)
);

-- Delete a Table
DROP TABLE student;

--Show the table schema
DESCRIBE student; 

-- Add & Drop Attributes
ALTER TABLE student ADD gpa DECIMAL(3,2);
ALTER TABLE student DROP COLUMN gpa;
```

## Insert, Update, Delete
``` sql
INSERT INTO student VALUES(1,'Jack','Biology');
INSERT INTO student(name) VALUES('Kate');  

UPDATE student
SET major = 'Computer Science and Engineering'
WHERE major = 'Computer Science' OR major = 'Computer Engineering';

DELETE FROM student
WHERE student_id > 100;
```