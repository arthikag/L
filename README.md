1.
CONCEPTUAL DATABASE DESIGN USING E-R DIAGRAM
The main elements of an ERD are:
● Entities - entity,weak,associative
● Relationships - strong,weak
● Attributes - attr,key,multi-val,derived
ENTITY
RELATIONSHIP TYPES:
1. Unary Relationship-Relationship between single entity
2. Binary Relationship-Relationship between two entity
3. Ternary Relationship-Relationship between three entity
ATTRIBUTE TYPES:
1. Simple- An attribute cannot be further subdivided(Eg:Reg no)
2. Composite-An attribute can be further
subdivided(Eg:Name---Firstname,Middlename,Lastname)
3. Single valued-An attribute has only one value(Eg:Reg No)
4. Multi valued-An attribute has more than one value(Eg:Phone Number)
5. Stored - An attribute's value cannot be determined from the values of other
attributes(Eg:Date of Birth)
6. Derived- An attribute's value can be determined from the values of other
attributes(Eg:Age which is derived from Date of Birth)
7. Descriptive- Attributes of the relationship is called descriptive attribute.( Eg:
employee works for department.
CONSTRAINTS TYPES:
1. Mapping Cardinalities
2. Participation Cardinalities

2.
IMPLEMENTATION OF SQL COMMANDS
DDL
1. Create
2. Desc
3. Alter (add, modify)
4. Truncate
5. Drop

DML
1. insert
2. select
3. update
4. delete
5. rename

DCL
1. grant
CREATE USER user_name@localhost IDENTIFIED BY 'PASSWORD';
GRANT privileges_names ON object TO user;
REVOKE privileges_names ON object FROM user;
			Grant select, update , insert on employees to departments with grant option;
			Revoke select, update , insert on employees from departments;
2. revoke

TCL
1. commit
2. save point
3. roll back

3.
INTEGRITY CONSTRAINT
a) Domain Integrity- Not Null constraint, Check Constraint
 Create table cust(custid number(6) not null, name char(10));
 Alter table cust modify (name not null);

 Create table student (regno number (6), mark number (3) constraint b check (mark &gt;=0
and mark <=100));
 Alter table student add constraint b2 check (length(regno<=4));
b) Entity Integrity - (ukc,pkc)
Create table cust(custid number(6) constraint uni unique, name char(10));
Alter table cust add(constraint c unique(custid));

Create table stud(regno number(6) constraint primary key, name char(20));

c) Referential Integrity - (fk,rk)
PRIMARY KEY TABLE:
CREATE TABLE product( product_id number(5) CONSTRAINT pd_id_pk PRIMARY KEY,
product_name char(20),supplier_name char(20),unit_price number(10));
FOREIGN KEY TABLE:
CREATE TABLE order_items
( order_id number(5) CONSTRAINT od_id_pk PRIMARY KEY,
product_id number(5) CONSTRAINT pd_id_fk REFERENCES,
product(product_id),
product_name char(20),
supplier_name char(20),
unit_price number(10));

4.
INBUILT FUNCTIONS
1. Mathematical functions
2. Character functions
3. Conversion Function
4. Group Function (Aggregate function)
5. Miscellaneous Function
6. Special Function
1.   SQL> select abs(-34) from dual;
2.   SQL> select ceil(50.8) from dual;
3.   SQL> select rtrim('computer','r') from dual;
4.   SQL> select lpad('oracle',9,'*') from dual;
5.   SQL> select substr('indian',1,5) from dual;
6.   SQL>select add_months('18-may-06') from dual;
7.   SQL> select last_day('18-may-06') from dual;
8.   SQL> select min(salary) from employee7;
9.   SQL> select avg(salary) from employee7;
10. SQL> select uid from dual;

1.For a discount of  25.5% being offered on all FMCG item’s unit price, display item code existing unit price as “Old Price” and discounted  price as “New Price”. Round off the discounted price to two decimal values.
Select itemcode,price,round(price - price*0.255,2) as "New Price" from item where itemtype = 'FMCG'

2.Retrieve the employee id, employee name of billing staff and the retail outlet where they work. Perform a case insensitive search
Select empid, empname ,worksin from employee where lower(designation) = 'billing staff'

3.Retrieve the order id, order status and payment mode of all the orders. Display ‘Payment yet not done’ when payment mode has NULL value.
Select orderid, status, nvl(paymentmode,'Payment yet not done')from orderstatus

4.Retrieve the description of items which have more than 15 characters
select description from item where length(description) > 15

5.Display numeric part of supplier id
Select substr(supplierid,2,5) from supplier

6.Retrieve the order id and the number of days between order date and payment
date for all orders
SELECT abs(to_date(orderdate,'mm/dd/yyyy')-to_date(paymentdate,'mm/dd/yyyy')) FROM orderstatus

7. Retrieve the order id and the number of  months between  order date and payment date for all orders
SELECT abs(MONTHS_BETWEEN(TO_DATE(orderdate,'MM-DD-YYYY'),TO_DATE(paymentdate,'MM-DD-YYYY') )) "Months" FROM orderstatus

8.Display current date and current date as ‘Mon/DD/YYYY Day’
select SYSDATE,to_char(SYSDATE,'mm/dd/yyyy,Day') from dual

5.
SIMPLE QUERIES
mysql-create.txt
source /home/skcet/Desktop/mysql-create.txt
mysql-data.txt
mysql-drop-tables.txt

select * from departments where location_id=1700;
select * from employees where department_id <> 8;
select * from employees where salary>10000 order by salary desc;
select * from employees where first_name like "Da%";
select * from employees where salary between 2500 and 2900;
select * from employees where job_id=9 and salary>5000;
select * from employees where job_id in(8,9,10) order by job_id;
select * from departments where departmnet_name='Marketing';

7.
SQL Join statement is used to combine data or rows from two or more tables based on a common field between them. Different types of Joins are as follows: 

INNER JOIN
LEFT JOIN
RIGHT JOIN
FULL JOIN
1. .Perform Cross JOIN on item and Retailstock. Write the Difference between Cross Join and
Inner Join
select * from item cross join retailstock
2. Display name and salary of the employees,who are drwing salary more than 2000. Along with
that display the department names in which they are working.Solve this using INNER JOIN
Select ename,sal,dname from emp inner join dept on emp.deptno=dept.deptno and
emp.sal&gt;2000

3. Display the name of employees and their department names who are managers.Solve this using
INNER JOIN.
Select ename,dname from emp inner join dept on emp.deptno=dept.deptno and
emp.job=&#39;MANAGER&#39;

4. Display itemcode,description of all items of type ‘FMCG’ along with outwardqty and
reatiloutletid where the items have been moved. Solve this using Left outer join.
Select outwardqty,retailoutletid,item.itemcode,description from item left outer join
outwarditem on item.itemcode=outwarditem.itemcode and item.itemtype = &#39;FMCG&#39;

5. For each employee,identify the vehicle owned by them. Displayename and vehicleid for the
same. Display name of employees even if they don’t own any vehicle. Solve this using Left outer
join.
Select ename,vehicleid from emp left outer join empvehicle on
emp.empno=empvehicle.empno

6. For each employee, identify the vehicle owned by them. Displayename and vehiclename for
the same. Display name of employees even if they don’t own any vehicle. Solve this using Left
outer join.
Select ename,vehiclename from emp left outer join empvehicle on emp.empno =
empvehicle.empno left outer join vehicle on empvehicle.vehicleid=vehicle.vehicleid

7. For every retail outlet, identify the employees working in it.. Display
empid,empname,retailoutletid and their retailoutletlocation.Solve this using Right outer join.
Select empid,empname,retailoutletid,retailoutletlocation from employee right outer join
retailoutlet on worksin = retailoutletid

8. Retrieve employee name,designation and email id of those employees who work in the same
retail outlet where George works. Do not display the record of George in the result.
select e1.empname,e1.designation,e1.emailid from employee e1 inner join employee e2 on
e1.worksin=e2.worksin and e2.empname = &#39;George&#39; and e1.empname &lt;&gt; &#39;George&#39;

8.
To perform VIEW the following commands are executed:
1. Create view
2. Inserting Rows into a View
3. Deleting Rows from a View
4. Update View
5. Delete View
VIEWS ANDJOINS
1.Create a relation instructor with following fields instructor_idnumber,name varchar2(10), dept_name varchar2(10),tot_cred number(10)
create table instructor (inst_idnumber,name varchar2(10),dept_name varchar2(10),tot_cred number)

2.Insert 5 values into the instructor relation. Create a view in the name of faculty by having the fields instructor_id,name,dept_name from the instructor table.
insert into instructor values(101,'Kavi','CSE',10);
insert into instructor values(102,'Ravi','IT',15);
insert into instructor values(103,'Swetha','EEE',13);
insert into instructor values(104,'Kumar','ECE',16);
insert into instructor values(105,'Sruthi','CSE',16);	
create view faculty as select inst_id,name,dept_name from instructor;

3.Retrieve the record from both instructor and faculty relation
select * from faculty;
select * from instructor;

4.Delete a record from faculty relation having dept_name as IT
delete from faculty where dept_name='IT';

5.Retrieve the record from both instructor and faculty relation
select * from faculty;
select * from instructor;

6.Create a view in the name of dept_faculty(d_name,f_name) as select dept_name,name from instructor.
create view Dept_faculty(d_name,f_name)as select dept_name,name from instructor;

7.Retrieve the records from dept_faculty
select * from dept_faculty;

8.Insert values into the view relation dept_faculty . Retrieve the records from dept_faculty
insert into dept_faculty values('E&I','Rekha');

9.Retrieve the record from both instructor and faculty relation
select * from faculty;
select * from instructor;

10.Update the name=’arun’ from faculty relation whose dept_name=’ECE’
update faculty set name='Arun' where dept_name='ECE';
select * from faculty;

11.Retrieve the record from instructor, faculty&dept_faculty relation
select * from instructor;
select * from faculty;
select * from dept_faculty;

9.
Practice of named PL/SQL blocks ( Procedure, Function)
To implement the various procedures and functions like,
1. IN parameter
2. OUT parameter
3. IN OUT parameter
1. IN: It specifies that a value for the argument must be specified when calling the
procedure ie., used to pass values to a sub-program. This is the default parameter.

2. OUT: It specifies that the procedure passes a value for this argument back to it’s
calling environment after execution ie. used to return values to a caller of the sub-
program.
3. IN OUT: It specifies that a value for the argument must be specified when calling the
procedure and that procedure passes a value for this argument back to it’s calling
environment
after execution.

create or replace function &lt;function name&gt; (argument in datatype,……) return datatype
{is,as}
variable declaration;
constant declaration;
begin
PL/SQL subprogram body;
exception
exception PL/SQL block;
end;
