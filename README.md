# Relational Database Basics
A relational database (RDB) is a collection of data organized into tables (relations). Each table consists of rows (records) and columns (attributes/fields).
## Table

Represents an entity (e.g., Employees, Students).
Each table has a unique name.
Columns define the type of data stored, and rows store the actual data.

## Primary Key (PK)

A column (or set of columns) that uniquely identifies each record in the table.
Cannot have NULL values.

create table employees (
    id int primary key,
    name nvarchar(50),
    position nvarchar(50)
);

## Foreign Key (FK)

A column that links to the primary key of another table to maintain relationships.
Helps maintain referential integrity.

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








