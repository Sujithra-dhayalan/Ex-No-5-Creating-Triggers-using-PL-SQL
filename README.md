# Ex. No: 5 Creating Triggers using PL/SQL

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
### Create employee table

```
create table employee((empid NUMBER, empname VARCHAR(10), dept VARCHAR(10),salary NUMBER);
insert into employee values(1,'John','HR',50000);
insert into employee values(2,'joe','IT',60000);
insert into employee values(3,'Bob','Finance',55000);
```

### Create salary_log table

```
 create table salary_log(log_id NUMBER GENERATED ALWAYS AS IDENTITY, empid NUMBER,empname VARCHAR(10),old_salary NUMBER,new_salary NUMBER,update_date DATE);

Table created.

```

### PLSQL Trigger code
```
create or replace trigger log_salary_update
before update on employee 
for each row
declare
v_old_salary NUMBER;
v_new_salary NUMBER;
begin
v_old_salary:= :old.salary;
v_new_salary:= :new.salary;
if v_old_salary <> v_new_salary then
insert into salary_log (empid, empname, old_salary, new_salary, update_date)
values(:old.empid, :old.empname, v_old_salary, v_new_salary, sysdate);
end if;
end;
/

select * from salary_log;

no rows selected

update employee set salary = 65000 where empid = 2;

1 row updated.

select * from salary_log;
```

### Output:

![image](https://github.com/Sujithra-dhayalan/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/115523950/1461cf88-6818-40a0-97f5-46a8b075140a)


### Result:

Hence a trigger is created successfully using PL/SQL.

