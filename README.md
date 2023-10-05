## Ex. No: 5 Creating Triggers using PL/SQL
## AIM:
To create a Trigger using PL/SQL.

## Steps:
1.Create employee table with following attributes (empid NUMBER, empname VARCHAR(10), dept VARCHAR(10),salary NUMBER);

2.Create salary_log table with following attributes (log_id NUMBER GENERATED ALWAYS AS IDENTITY, empid NUMBER,empname VARCHAR(10),old_salary NUMBER,new_salary NUMBER,update_date DATE);

3.Create a trigger named as log_salary-update.

4.Inside the trigger block, Insert the values into the salary_log table whenever the salary is updated.

5.End the trigger.

6.Update the salary of an employee in employee table.

7.Whenever a salary is updated for the employee it must be logged into the salary_log table with old salary and new salary.

8.Display the employee table, salary_log table.

## Program:

## Create employee table
## Query:
```
CREATE TABLE employee (empid INT PRIMARY KEY,empname VARCHAR(10),dept VARCHAR(10),salary DECIMAL(10, 2));

insert into employee values (1,'Abi','HR',35000);
insert into employee values (2,'Divya','TL',25000);

select * from employee;
```
## Table:
![image](https://github.com/Niroshassithanathan/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/121418437/94920838-edc5-4ad9-a9be-2528ba700eae)

## Create salary_log table
## Query:
```
CREATE TABLE salary_log (log_id INT AUTO_INCREMENT PRIMARY KEY,empid INT,empname VARCHAR(10),old_salary DECIMAL(10, 2),
new_salary DECIMAL(10, 2),update_date DATE);

desc salary_log;
```
## Table:
![image](https://github.com/Niroshassithanathan/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/121418437/61e8f38c-feef-4a99-bdbd-3abacbdefe0a)

## PLSQL Trigger code:
```
DELIMITER //
CREATE TRIGGER log_salary_update AFTER UPDATE ON employee FOR EACH ROW
BEGIN
  INSERT INTO salary_log (empid, empname, old_salary, new_salary, update_date) VALUES (OLD.empid, OLD.empname,
OLD.salary, NEW.salary, NOW());
END;
//
DELIMITER ;
```
## Output:
![image](https://github.com/Niroshassithanathan/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/121418437/186ccd94-c7ca-4de2-a27d-b09bfe8dcd08)

## Updated Tables:
## Query:
```
UPDATE employee SET salary = 50000 WHERE empid = 1;
UPDATE employee SET salary = 40000 WHERE empid = 2;

SELECT * FROM employee;
SELECT * FROM salary_log;
```
## Output:
![image](https://github.com/Niroshassithanathan/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/121418437/e974def6-ef09-456b-aa98-81d4e8cae9e0)

## Result:
Thus the program implemented successfully.
