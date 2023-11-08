# Ex. No: 5 Creating Triggers using PL/SQL

### DATE: 01/09/2023

### AIM: To create a Trigger using PL/SQL.

### Steps:
1. Create employee table with following attributes (empid NUMBER, empname VARCHAR(10), dept VARCHAR(10),salary NUMBER);
2. Create salary_log table with following attributes (log_id NUMBER GENERATED ALWAYS AS IDENTITY, empid NUMBER,empname VARCHAR(10),old_salary NUMBER,new_salary NUMBER,update_date DATE);
3. Create a trigger named as log_salary-update.
4. Inside the trigger block, Insert the values into the salary_log table whenever the salary is updated.
5. End the trigger.
6. Update the salary of an employee in employee table.
7. Whenever a salary is updated for the employee it must be logged into the salary_log table with old salary and new salary.
8. Display the employee table, salary_log table.

### Program:
```sql
SQL> CREATE TABLE emp(empid number, empname varchar(10), dept varchar(10),salary number);
Table created.

SQL> CREATE TABLE salary_log (log_id NUMBER GENERATED ALWAYS AS IDENTITY, empid NUMBER, empname VARCHAR2(10), old_salary NUMBER, new_salary NUMBER, update_date DATE);
Table created.

-- Insert the values in the employee table
INSERT INTO emp(empid, empname, dept, salary)
values(1,'Krishna','Agri',70000);
INSERT INTO emp(empid, empname, dept, salary)
values(2,'Radha','Cyber',80000);
INSERT INTO emp(empid, empname, dept, salary)
values(3,'Balram','IT',50000);
```
### Create employee table

![exp5_DBMS-1](https://github.com/vijayarajv1704/Ex-5-Creating-Triggers-using-PL-SQL/assets/121303741/e92ee22b-7897-4c44-9fa3-7f8fdc259f3d)

### Create salary_log table

![exp5_DBMS-2](https://github.com/vijayarajv1704/Ex-5-Creating-Triggers-using-PL-SQL/assets/121303741/ca10a59f-ca6a-4524-9568-e16f6de04fed)


### PLSQL Trigger code
```sql
SQL> -- Create the trigger
SQL> CREATE OR REPLACE TRIGGER log_salary__update
  2  BEFORE UPDATE ON emp
  3  FOR EACH ROW
  4  BEGIN
  5    IF :OLD.salary != :NEW.salary THEN
  6      INSERT INTO salary_log (empid, empname, old_salary, new_salary, update_date)
  7      VALUES (:OLD.empid, :OLD.empname, :OLD.salary, :NEW.salary, SYSDATE);
  8    END IF;
  9  END;
 10  /
Trigger created.

SQL> -- Update the salary of an employee
SQL> UPDATE emp
  2  SET salary = 50000
  3  WHERE empid = 1;

1 row updated.

SQL> -- Display the employee table
SQL> SELECT * FROM emp;

SQL> -- Display the salary_log table
SQL> SELECT * FROM salary_log;
```
### Output:

![exp5_DBMS-3](https://github.com/vijayarajv1704/Ex-5-Creating-Triggers-using-PL-SQL/assets/121303741/b1897121-491c-49bf-9b15-da397a9e1a30)

### Result:
The program has been successfully implemented.
