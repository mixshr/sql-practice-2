# SQL PRACTICE

### SQL Practice №2 | Employee management

#### Relational shema
![Relation shema](https://upload.wikimedia.org/wikipedia/commons/thumb/3/36/Employees.png/300px-Employees.png)

#### The creation code
``` sql
CREATE TABLE Departments (
   Code INTEGER PRIMARY KEY NOT NULL,
   Name NVARCHAR NOT NULL ,
   Budget REAL NOT NULL 
);
 
 CREATE TABLE Employees (
   SSN INTEGER PRIMARY KEY NOT NULL,
   Name TEXT NOT NULL ,
   LastName VARCHAR NOT NULL ,--since question 2 asks about removing duplicate - text must be converted if the answer is using distinct
   Department INTEGER NOT NULL , 
   CONSTRAINT fk_Departments_Code FOREIGN KEY(Department) 
   REFERENCES Departments(Code)
);
```
#### Sample datase
``` sql
INSERT INTO Departments(Code,Name,Budget) VALUES(14,'IT',65000);
INSERT INTO Departments(Code,Name,Budget) VALUES(37,'Accounting',15000);
INSERT INTO Departments(Code,Name,Budget) VALUES(59,'Human Resources',240000);
INSERT INTO Departments(Code,Name,Budget) VALUES(77,'Research',55000);

INSERT INTO Employees(SSN,Name,LastName,Department) VALUES('123234877','Michael','Rogers',14);
INSERT INTO Employees(SSN,Name,LastName,Department) VALUES('152934485','Anand','Manikutty',14);
INSERT INTO Employees(SSN,Name,LastName,Department) VALUES('222364883','Carol','Smith',37);
INSERT INTO Employees(SSN,Name,LastName,Department) VALUES('326587417','Joe','Stevens',37);
INSERT INTO Employees(SSN,Name,LastName,Department) VALUES('332154719','Mary-Anne','Foster',14);
INSERT INTO Employees(SSN,Name,LastName,Department) VALUES('332569843','George','O''Donnell',77);
INSERT INTO Employees(SSN,Name,LastName,Department) VALUES('546523478','John','Doe',59);
INSERT INTO Employees(SSN,Name,LastName,Department) VALUES('631231482','David','Smith',77);
INSERT INTO Employees(SSN,Name,LastName,Department) VALUES('654873219','Zacary','Efron',59);
INSERT INTO Employees(SSN,Name,LastName,Department) VALUES('745685214','Eric','Goldsmith',59);
INSERT INTO Employees(SSN,Name,LastName,Department) VALUES('845657245','Elizabeth','Doe',14);
INSERT INTO Employees(SSN,Name,LastName,Department) VALUES('845657246','Kumar','Swamy',14);
```
#### Exercises
1. Select the last name of all employees.
2. Select the last name of all employees, without duplicates.
3. Select all the data of employees whose last name is "Smith".
4. Select all the data of employees whose last name is "Smith" or "Doe".
5. Select all the data of employees that work in department 14.
6. Select all the data of employees that work in department 37 or department 77.
7. Select all the data of employees whose last name begins with an "S".
8. Select the sum of all the departments' budgets.
9. Select the number of employees in each department (you only need to show the department code and the number of employees).
10. Select all the data of employees, including each employee's department's data.
11. Select the name and last name of each employee, along with the name and budget of the employee's department.
12. Select the name and last name of employees working for departments with a budget greater than $60,000.
13. Select the departments with a budget larger than the average budget of all the departments.
14. Select the names of departments with more than two employees.
15. Select the name and last name of employees working for departments with second lowest budget.
16. Add a new department called "Quality Assurance", with a budget of $40,000 and departmental code 11. Add an employee called "Mary Moore" in that department, with SSN 847-21-9811.
17. Reduce the budget of all departments by 10%.
18. Reassign all employees from the Research department (code 77) to the IT department (code 14).
19. Delete from the table all employees in the IT department (code 14).
20. Delete from the table all employees who work in departments with a budget greater than or equal to $60,000.
21. Delete from the table all employees.

``` sql
1. SELECT LastName FROM Employees;

2. SELECT DISTINCT LastName FROM Employees;

3. SELECT * FROM Employees WHERE LastName = 'Smith';

4. SELECT * FROM Employees WHERE LastName = 'Smith' OR LastName = 'Doe';

5. SELECT * FROM Employees WHERE Department = 14;

6. SELECT * FROM Employees WHERE Department = 37 OR Department = 77;

7. SELECT * FROM Employees WHERE LastName LIKE 'S%';

8. SELECT SUM(Budget) FROM Departments;

9. SELECT Department, COUNT(*) FROM Employees GROUP BY Department;

10. SELECT * FROM Employees E INNER JOIN Departments D ON E.Department = D.Code;

11. SELECT Employees.Name, LastName, Departments.Name AS DepartmentsName, Budget FROM Employees INNER JOIN Departments ON Employees.Department = Departments.Code;

12. SELECT Employees.Name, LastName FROM Employees INNER JOIN Departments ON Employees.Department = Departments.Code AND Departments.Budget > 60000;

13. SELECT * FROM Departments WHERE Budget > (SELECT AVG(Budget) FROM Departments);

14. SELECT D.Name FROM Departments D WHERE 2 < (SELECT COUNT(*) FROM Employees WHERE Department = D.Code);

15. SELECT Name FROM Departments  WHERE Code IN (SELECT Department FROM Employees GROUP BY Department HAVING COUNT(*) > 2);

16. SELECT e.Name, e.LastName FROM Employees e WHERE e.Department = (SELECT sub.Code FROM (SELECT * FROM Departments d ORDER BY d.budget LIMIT 2) sub ORDER BY budget DESC LIMIT 1);

17. INSERT INTO Departments VALUES ( 11 , 'Quality Assurance' , 40000);

18. INSERT INTO Employees VALUES ('847219811' , 'Mary' , 'Moore' , 11);

19. UPDATE Departments SET Budget = Budget * 0.9;

20. UPDATE Employees SET Department = 14 WHERE Department = 77;

21. DELETE FROM Employees WHERE Department = 14;

22. DELETE FROM Employees WHERE Department IN (SELECT Code FROM Departments WHERE Budget >= 60000);

23. DELETE FROM Employees;
```
