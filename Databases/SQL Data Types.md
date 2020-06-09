## SQL Data Types

```SQL
-- DATATYPES
INT -- Whole Numbers
DECIMAL(M,N) -- Decimal Numbers: m is total # digits, n is # digits after decimal place
VARCHAR(L) -- String of text of max length L
BLOB --Binary large objects, stores large data (e.g. images, files)
DATE -- 'YYYY-MM-DD'
TIMESTAMP -- 'YYYY-MM-DD HH:MM:SS'
```

## SQL Functions
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

## SQL Queries
```SQL
SELECT student.name AS forename, student.major
FROM student 
ORDER BY name DESC --Descending alphabetical order
LIMIT 20; --limits # of entries returned

-- Comparison Operators: <, >, <=, >=, =, AND, OR, <> (not equal to)
```

## SQL Commands
```SQL
--Create a Table
CREATE TABLE student (
  student_id INT AUTO_INCREMENT, --Automatically increments the value of the primary key so you don't have to insert it
  name VARCHAR(20) UNIQUE, --Constraint on what can be entered into table 
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

--Show all elements in a table
SELECT * FROM student;

--Inserting Elements into a Table
INSERT INTO student VALUES(1,'Jack','Biology');
INSERT INTO student(name) VALUES('Kate'); -- Allows you to enter only specific attributes for a row 

-- Update Values for an Attribute
UPDATE student
SET major = 'Computer Science and Engineering'
WHERE major = 'Computer Science' OR major = 'Computer Engineering'; --Any conditional can be used here

--Delete rows 
DELETE FROM student
WHERE student_id > 100;
```