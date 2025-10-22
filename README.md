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








