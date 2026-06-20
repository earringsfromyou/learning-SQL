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

SELECT dept,count(dept)
FROM 
	Employees
GROUP BY dept
HAVING count(dept)>2
;

SET SQL_SAFE_UPDATES=0;

UPDATE Employees
SET salary=55000
WHERE emp_name ="Ram";

UPDATE Employees
SET dept = 'Finance'
WHERE emp_name='sita';

UPDATE Employees
SET salary=48000
WHERE emp_id=4;

UPDATE Employees
SET emp_name='Ritu'
WHERE emp_name='Rita';

UPDATE Employees
SET salary=salary+5000
WHERE dept = 'IT';

UPDATE Employees
SET salary =salary+(0.1*salary)
WHERE dept ='HR';

UPDATE Employees
SET dept='Accounts'
WHERE dept='Finance';

UPDATE Employees
SET salary=salary+3000
WHERE salary<50000;

UPDATE Employees
SET salary=salary+(0.05*salary);

UPDATE Employees
SET dept='Senior IT'
WHERE salary>60000;

UPDATE Employees
SET salary=50000
WHERE salary<(
	SELECT ag FROM(
    SELECT AVG(salarY) AS ag
    FROM EMPLOYEES)AS TEMP
);

UPDATE Employees
SET emp_name='Top Performer'
WHERE salary=(
	SELECT mx FROM(SELECT MAX(salary)AS mx
    FROM Employees )AS temp
);
SELECT *
FROM Employees;

-- PRACTICING DELETE COMMAND;

CREATE TABLE Books (
    book_id INT PRIMARY KEY,
    title VARCHAR(100),
    author VARCHAR(50),
    genre VARCHAR(30),
    price DECIMAL(8,2)
);

INSERT INTO Books(book_id,title,author,genre,price) VALUES
(1, 'The Alchemist', 'Paulo Coelho', 'Fiction', 15.99),
(2, 'Clean Code', 'Robert Martin', 'Programming', 45.00),
(3, 'Atomic Habits', 'James Clear', 'Self Help', 20.50),
(4, 'The Pragmatic Programmer', 'Andrew Hunt', 'Programming', 50.00),
(5, 'Rich Dad Poor Dad', 'Robert Kiyosaki', 'Finance', 18.75),
(6, 'Think and Grow Rich', 'Napoleon Hill', 'Finance', 12.50),
(7, 'Deep Work', 'Cal Newport', 'Productivity', 22.00),
(8, 'Python Crash Course', 'Eric Matthes', 'Programming', 35.00);

SELECT *
FROM Books;

DELETE FROM Books
WHERE book_id = 5;

DELETE FROM Books
WHERE title='Deep Work';

DELETE FROM Books 
WHERE genre='Finance';

DELETE FROM Books
WHERE price <20;

DELETE FROM Books
WHERE author ='Paulo Coelho';

DELETE FROM Books
WHERE genre='Programming';

DELETE FROM Books
WHERE title LIKE 'THE%';

DELETE FROM Books
WHERE book_id BETWEEN 2 and 5;

DELETE FROM Books
WHERE price=(
SELECT max_price FROM (SELECT MAX(PRICE) AS max_price FROM Books)AS temp
);

DELETE FROM Books
WHERE price = (SELECT min_price 
	FROM (SELECT  MIN(price) AS min_price FROM Books)AS temp
);

DELETE FROM Books
WHERE genre != 'Programming';

DELETE FROM Books
WHERE price>(
	SELECT avg_price FROM(SELECT AVG(price) AS avg_price FROM Books) AS temp
);

DELETE FROM Books
WHERE author LIKE '%Hill' OR author LIKE '%Clear';

DELETE FROM Books
WHERE price = (SELECT MAX(price) FROM Books);

DELETE FROM Books
WHERE price = (SELECT MIN(price)FROM Books);

DELETE FROM Books
WHERE genre =(
SELECT genre_name  
FROM (SELECT genre AS genre_name
	FROM Books
	GROUP BY genre
	ORDER BY count(*) DESC
	LIMIT 1)AS temp
);

DELETE FROM Books
WHERE price NOT IN (
SELECT price 
FROM (
	SELECT price 
    FROM Books
    ORDER BY price DESC
    LIMIT 2
)AS temp
);

DELETE FROM Books 
WHERE price NOT IN (
SELECT min_price
FROM(
	SELECT price AS min_price 
    FROM Books
    ORDER BY price ASC 
    LIMIT 3)AS temp
);

