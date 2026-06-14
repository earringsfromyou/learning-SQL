CREATE DATABASE COLLEGE;

USE COLLEGE;

CREATE TABLE Students(
student_id INT PRIMARY KEY,
name VARCHAR(50),
age INT NOT NULL,
city VARCHAR(50)
);

INSERT INTO Students
(student_id,name,age,city)
VALUE
(1, 'Ram', 18, 'Pokhara'),
(2, 'Sita', 20, 'Kathmandu'),
(3,'Hari', 22, 'Pokhara'),
(4, 'Gita', 19, 'Butwal'),
(5, 'Shyam', 21, 'Kathmandu');

SELECT * FROM Students;

SELECT name FROM Students;

SELECT * FROM Students WHERE (age>20);

SELECT * FROM Students WHERE (age<=19);

SELECT * FROM Students WHERE city IN('Kathmandu');

SELECT * FROM Students WHERE (age>18) AND city IN ('Kathmandu');

SELECT * FROM Students WHERE city IN('Pokhara','Butwal');

SELECT * FROM Students WHERE (age!=20);

SELECT * FROM Students WHERE age BETWEEN 19 AND 21;

SELECT * FROM Students WHERE city IN ('Kathmandu','Pokhara');

SELECT * FROM Students WHERE name LIKE 'S%';

SELECT * FROM Students WHERE name LIKE '%a';

SELECT * FROM Students WHERE name LIKE '%it%';

SELECT * FROM Students WHERE (age>18) AND city IN ('Kathmandu') AND name LIKE 'S%';

SELECT * FROM Students WHERE city IN ('Kathmandu','Pokhara') AND age BETWEEN 18 AND 21;

SELECT * FROM Students WHERE age>19 ORDER BY age  ASC LIMIT 3;

SELECT city,count(city) FROM Students GROUP BY city;

SELECT 
    city, AVG(age)
FROM
    Students
GROUP BY city
ORDER BY avg(age) ASC;

CREATE DATABASE IF NOT EXISTS CompanyDB;
USE CompanyDB;

CREATE TABLE Employees (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50) NOT NULL,
    dept VARCHAR(30) NOT NULL,
    salary INT CHECK (salary > 0)
);

INSERT INTO Employees (emp_id, emp_name, dept, salary) VALUES
(1, 'Ram', 'IT', 50000),
(2, 'Sita', 'HR', 40000),
(3, 'Hari', 'IT', 60000),
(4, 'Gita', 'Finance', 45000),
(5, 'Shyam', 'HR', 55000),
(6, 'Rita', 'IT', 70000),
(7, 'Nabin', 'Finance', 50000);

SELeCT * FROM Employees;

SELECt emp_name,salary From Employees;

SELECT * FROM Employees WHERE salary>50000;

SELECT * FROM Employees WHERE dept IN ('IT');

SELECT 
    *
FROM
    Employees
WHERE
    dept IN ('IT' , 'Finance');

SELECT 
	*
FROM 
	Employees 
ORDER BY 
	salary ASC;
    
SELECT 
	* 
FROM
	Employees
ORDER BY 
	salary DESC;
    
SELECT 
	*
FROM 
	Employees
ORDER BY
	SALARY DESC
LIMIT 3;
	
SELECT 
	*
FROM
	 EmployeeS
ORDER BY 
	salary ASC
LIMIT 1;

SELECT 
	COUNT(emp_id)
FROM 
	Employees;
    
SELECT 
    MAX(SALARY)
FROM
    EMPLOYEES;
    
SELECT
	MIN(salary)
FROM
	Employees;

SELECT
	AVG(salary)
FROM
	Employees;
    
SELECT 
    SUM(salary)
FROM
    Employees;
    
SELECT 
    dept, COUNT(dept)
FROM
    Employees
GROUP BY dept;

SELECT 
    dept, SUM(salary)
FROM
    Employees
GROUP BY dept;

SELECT 
	dept,MAX(dept)
FROM Employees
GROUP BY dept;

SELECT 
	dept,MIN(dept)
FROM Employees
GROUP BY dept;
    
SELECT 
    dept, COUNT(dept)
FROM
    Employees
GROUP BY dept 
ORDER BY count(dept) DESC;

SELECT 
	dept, SUM(salary)
FROM 
	Employees
GROUP BY
	dept
ORDER BY
	SUM(salary) DESC
LIMIT 1;
hi


