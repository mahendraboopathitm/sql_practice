# Relational Database Basics
A relational database (RDB) is a collection of data organized into tables (relations). Each table consists of rows (records) and columns (attributes/fields).
## Table

Represents an entity (e.g., Employees, Students).
Each table has a unique name.
Columns define the type of data stored, and rows store the actual data.

<img width="1549" height="555" alt="image" src="https://github.com/user-attachments/assets/72655043-4cb4-44e1-95a1-043d3cac4ad8" />


## Primary Key (PK)

A column (or set of columns) that uniquely identifies each record in the table.
Cannot have NULL values.
<img width="1526" height="106" alt="image" src="https://github.com/user-attachments/assets/8ac4ec8e-9a53-4ae9-891d-c223a76be598" />

create table employees (
    id int primary key,
    name nvarchar(50),
    position nvarchar(50)
);

## Foreign Key (FK)

A column that links to the primary key of another table to maintain relationships.
Helps maintain referential integrity.
<img width="1409" height="164" alt="image" src="https://github.com/user-attachments/assets/2443a9c7-6407-4fa2-bedb-b9500dda4500" />

Example:

create table departments (
    dept_id int primary key,
    dept_name nvarchar(50)
);

create table employees (
    id int primary key,
    name nvarchar(50),
    dept_id int,
    foreign key (dept_id) references departments(dept_id)
);

Here, dept_id in employees references departments. Only valid department IDs can be inserted.

## Normalization

Process of organizing data to reduce redundancy.
1NF, 2NF, 3NF are common normalization forms.

# Database Management System (DBMS)

A DBMS is software used to store, retrieve, and manage data in databases.
## Functions of DBMS

Data Storage & Retrieval: Efficiently store large volumes of data and retrieve it using queries.
Security: Control user access with roles and permissions.
Backup & Recovery: Recover data after system failures.
Multi-user Access: Allow multiple users to access the same data simultaneously without conflicts.
## Types of DBMS

Relational (RDBMS) – SQL Server, MySQL, Oracle
NoSQL – MongoDB, Cassandra

# Basic SQL Syntax

SQL (Structured Query Language) is used to interact with relational databases.

Common SQL Commands
-- Switch database
use sql_practice;

-- List all tables
select table_name 
from information_schema.tables 
where table_type = 'base table';

-- View table data
select * from employees;

## DDL (Data Definition Language)

DDL commands define or modify the structure of the database and tables.
Commands

## CREATE

Create new tables or databases.

create table employees (
    id int primary key,
    name nvarchar(50),
    position nvarchar(50),
    salary int
);

<img width="1549" height="555" alt="image" src="https://github.com/user-attachments/assets/72655043-4cb4-44e1-95a1-043d3cac4ad8" />
## ALTER

Modify an existing table structure.

alter table employees
add dateofjoining date;


DROP

## Delete a table or database.

drop table employees;


## TRUNCATE

Remove all records from a table but keep its structure.
truncate table employees;



# DML (Data Manipulation Language)

DML commands manage the data inside tables.
Commands

## INSERT

insert into employees (id, name, position, salary, dateofjoining)
values (1, 'mahi', 'developer', 50000, '2025-10-22');

<img width="1495" height="478" alt="image" src="https://github.com/user-attachments/assets/511422dc-41dd-48b1-9273-00f78ef21d91" />

## UPDATE

update employees
set salary = 60000
where name = 'mahi';


## DELETE

delete from employees
where name = 'mahi';


## SELECT

select * from employees;
select name, salary from employees where salary > 40000;

<img width="1621" height="519" alt="image" src="https://github.com/user-attachments/assets/935dd575-bc3e-45ba-955f-d876d1e71dbc" />

# DCL (Data Control Language)

DCL commands control access and permissions in SQL Server.
Commands

## GRANT

grant select, insert on employees to user1;


## REVOKE

revoke insert on employees from user1;


## DROP USER

drop user user1;

# DQL (Data Query Language)

DQL is used to retrieve data from a database. It primarily involves the select statement, which allows users to query one or more tables, apply conditions, group data, and sort results.

##  Aggregating Data Using Functions

Aggregation functions perform calculations on multiple rows of a table and return a single value.

Common Aggregate Functions:

count() – returns the number of rows
sum() – returns the total sum of a numeric column
avg() – returns the average value
min() – returns the smallest value
max() – returns the largest value


select count(*) as total_employees,
       avg(salary) as average_salary,
       max(salary) as highest_salary,
       min(salary) as lowest_salary
from employees; 

<img width="1620" height="757" alt="image" src="https://github.com/user-attachments/assets/9675693a-6ba8-4b22-afa5-f04a17dbd361" />

## Grouping Data with group by

The group by clause groups rows that have the same values into summary rows.

Example:

select department, avg(salary) as average_salary
from employees
group by department;

## Filtering Aggregated Data with having

The having clause filters results after grouping (unlike where, which filters before grouping).

Example:

select department, avg(salary) as average_salary
from employees
group by department
having avg(salary) > 50000;

## Sorting Results with order by

The order by clause sorts the output in ascending (asc) or descending (desc) order.

Example:

select employee_name, salary
from employees
order by salary desc;

 # TCL (Transaction Control Language)


TCL commands manage transactions in a database. They ensure data integrity and allow users to commit or rollback changes.

## commit

Saves all changes made during the current transaction permanently to the database.

Example:

insert into employees values (101, 'John', 50000, 'HR');
commit;

## rollback

Undoes changes made in the current transaction that have not yet been committed.

Example:

delete from employees where department = 'HR';
rollback;


(→ The deleted data will be restored.)

## savepoint

Sets a point within a transaction to which you can later roll back.

Example:

save transaction point1;
update employees set salary = salary + 1000;
rollback transaction point1;
commit;

# Constraints

Definition:
Constraints are rules applied to table columns to maintain data accuracy and integrity. They prevent invalid data from being inserted into tables.

## primary key

Ensures each record in a table is unique and not null.
Each table can have only one primary key.

Example:

create table students (
    student_id int primary key,
    student_name varchar(50)
);

## foreign key

Establishes a relationship between two tables.
A foreign key in one table points to a primary key in another.

Example:

create table orders (
    order_id int primary key,
    student_id int foreign key references students(student_id)
);

## unique

Ensures that all values in a column are unique but allows one null.

Example:

create table users (
    user_id int primary key,
    email varchar(100) unique
);

## check

Defines a condition each row must satisfy.

Example:

create table employees (
    emp_id int primary key,
    salary int check (salary > 0)
);

## not null

Ensures that a column cannot contain null values.

Example:

create table customers (
    customer_id int primary key,
    customer_name varchar(100) not null
);


# joins:
## database and table creation:
<img width="1596" height="742" alt="image" src="https://github.com/user-attachments/assets/7b1ab497-078c-4e8c-9c8a-70887fa67e0b" />

<img width="1574" height="743" alt="image" src="https://github.com/user-attachments/assets/cabd9109-b5bf-42fa-bd07-9c7a68bbef3f" />

<img width="1418" height="473" alt="image" src="https://github.com/user-attachments/assets/a6ed51ea-7d81-4dc5-892c-9dbf2940a5ce" />



##  INNER JOIN

 Combines rows from both tables where there is a matching dept_id in both.


 <img width="1587" height="365" alt="image" src="https://github.com/user-attachments/assets/82952b20-cc08-4dde-a2d9-528c87e0a35d" />

 ## left join

 Retrieving all records from the left table and matching records from the right table.

 <img width="1619" height="428" alt="image" src="https://github.com/user-attachments/assets/ec6e7c0f-6b8d-45fb-84df-eee7e25790fe" />


 ## right join:

 Retrieving all records from the right table and matching records from the left table.

 <img width="1613" height="395" alt="image" src="https://github.com/user-attachments/assets/ae059023-34fa-4725-9f57-26b3fb6bb453" />

 ## outer join

 Retrieving all records when there is a match in either the left or right table.

 <img width="1614" height="370" alt="image" src="https://github.com/user-attachments/assets/7dcbb9de-ba39-4c4d-93fb-17e05a0378ce" />


 ## cross join

 Producing the Cartesian product of two tables.

<img width="1607" height="677" alt="image" src="https://github.com/user-attachments/assets/97630096-913f-450b-8382-0d844d600d0c" />


# sql aggregate function:

AVG,SUM,MIN,MAX,COUNT

<img width="1606" height="534" alt="image" src="https://github.com/user-attachments/assets/65c01621-f8da-4ac7-81f1-e1aaf3552ca8" />

<img width="1605" height="368" alt="image" src="https://github.com/user-attachments/assets/f95f9891-0ffd-49a1-93e9-5c6eb68e3cf9" />

<img width="1603" height="590" alt="image" src="https://github.com/user-attachments/assets/002a1bc2-7ad3-4fa4-86e2-ce0c38fd7df4" />


# sql clause:

## having,group by,order by

<img width="1593" height="616" alt="image" src="https://github.com/user-attachments/assets/7c64cd61-091a-43dd-8caa-c007c54ac0bc" />

<img width="1614" height="414" alt="image" src="https://github.com/user-attachments/assets/e2f6f611-11ad-47f9-9e20-6640d0fdff4f" />

<img width="1584" height="755" alt="image" src="https://github.com/user-attachments/assets/b7b74c2e-88ad-41ad-ae05-dbdcb90ee836" />

# operators:

## arithmtic operator:

<img width="1606" height="692" alt="image" src="https://github.com/user-attachments/assets/7718da41-7e88-4718-965d-21c1fb427a30" />

## comparision operator:

<img width="1613" height="604" alt="image" src="https://github.com/user-attachments/assets/0c326534-18a4-402d-a6f5-263f6b513f57" />


## logical operator:

<img width="1620" height="598" alt="image" src="https://github.com/user-attachments/assets/0c3651be-c935-4a5a-a218-ed3e9c904c70" />

## string comparator operator:

<img width="1611" height="381" alt="image" src="https://github.com/user-attachments/assets/6e5da58b-1f14-40f5-997d-fbb9ac6317d0" />


# Procedure:

## CREATE PROCEDURE

Used to create a stored procedure — a reusable block of SQL code that can take input parameters, execute queries, and return results.
 
<img width="1610" height="544" alt="image" src="https://github.com/user-attachments/assets/7d2749c7-87a1-4649-bf25-f26c646f4426" />

## ALTER PROCEDURE

Used to modify an existing stored procedure (change logic, parameters, etc.).


<img width="1614" height="589" alt="image" src="https://github.com/user-attachments/assets/7fdd490e-2c2e-40f4-8e3f-7cd5edb9d2b9" />

 
##  DROP PROCEDURE

Used to delete an existing stored procedure from the database.

<img width="1613" height="356" alt="image" src="https://github.com/user-attachments/assets/fc6eaa66-10b2-4b51-8c1b-069c94de72ff" />

##  EXECUTE (or EXEC)

Used to run (execute) a stored procedure.

<img width="1606" height="788" alt="image" src="https://github.com/user-attachments/assets/ec49c6be-5d4f-4dc6-8f2e-887f13e68721" />
# Subquery

A Subquery is a query inside another query.
It is used when you need to use the result of one query as input for another.

## Example 1: Find employees earning more than the average salary

<img width="1617" height="502" alt="image" src="https://github.com/user-attachments/assets/cdcc26ff-c819-4972-991a-a46b3c4bcade" />

## Find the students who scored above the average marks in any course.

<img width="1615" height="663" alt="image" src="https://github.com/user-attachments/assets/0af48b68-4210-4f94-9e14-90f65903ec0d" />

# common table expressions:

## CTE (Common Table Expression)

A CTE (Common Table Expression) is a temporary result set that you can reference within a single SQL statement.
It makes complex queries easier to read, organize, and reuse.

## Find the average marks of students in each department using a CTE.

<img width="1615" height="639" alt="image" src="https://github.com/user-attachments/assets/8110c5fb-1082-4d3e-a7ea-db792fa54569" />

The CTE named DeptAvg first calculates the average marks of each department.
Then the main query joins that result with the Departments table to display the department name and its average marks.

## List students and their total marks in all courses, but only include those who scored above 250 total.

<img width="1618" height="634" alt="image" src="https://github.com/user-attachments/assets/c8c65062-d6f4-4200-bab3-4610b3bd42b5" />


The CTE (StudentTotal) calculates total marks for each student.
The main query filters only those with total marks greater than 150.

# views:

A View is a virtual table based on the result of an SQL query.
It doesn’t store data physically — it just stores the query definition.
You can query a view just like a real table.

 ## CREATE VIEW: Creating views for simplified querying

## Example 1: Creating a View

<img width="1590" height="495" alt="image" src="https://github.com/user-attachments/assets/42699878-ddff-40e7-89c0-eb3866a7ebab" />

<img width="1618" height="623" alt="image" src="https://github.com/user-attachments/assets/5a789d5b-1862-452a-8d32-65c0bb793374" />

## DROP VIEW: Removing views

If you no longer need a view, you can delete it using the DROP VIEW command.


<img width="1616" height="317" alt="image" src="https://github.com/user-attachments/assets/be1c82ed-2e22-485d-8919-f693ef66c909" />




