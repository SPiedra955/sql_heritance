# Table of contents
 * [**SQL inheritance**](#sql-inheritance)
    * [**Inheritance**](#inheritance)
 * [**Activity**](#activity)
    * [**Data insertion**](#data-insertion)
    * [**Querys**](#querys)

# SQL inheritance
### Inheritance

Inheritance in SQL is a concept that allows you to create a hierarchy relationship between tables, where a child table inherits properties and characteristics from a parent table. This is achieved by creating secondary tables that contain specific additional columns, but also include the columns of the primary table.

The following task consist in created your own example of inheritance and show how it works.

# Activity

Suppose you want to model a database of people with different roles, such as students and teachers. You want students and teachers to inherit basic properties from the main table "People".

Here is the database script using inheritance:

````
CREATE DATABASE inheritance;

-- Create the table for people
CREATE TABLE people (
  person_id SERIAL PRIMARY KEY,
  name VARCHAR(50),
  age INTEGER
);

-- Create the table for students
CREATE TABLE students (
  student_id SERIAL PRIMARY KEY,
  course VARCHAR(50),
  FOREIGN KEY (student_id) REFERENCES people (person_id)
) INHERITS (people);

-- Create the table for teachers
CREATE TABLE teachers (
  teacher_id SERIAL PRIMARY KEY,
  department VARCHAR(50),
  FOREIGN KEY (teacher_id) REFERENCES people (person_id)
) INHERITS (people);

````

In this example, the table "People" is the main table containing the properties common to all persons, such as ID, name, age and address. Then, two additional tables are created: ````"Students"```` and ````"Teachers"````. These tables inherit the column "id" from the main table using a FOREIGN KEY.

The ````"Students"```` table has additional properties such as "course", while the ````"Teachers"```` table has an additional property called "department". By using inheritance, you can store data specific to each type of person in separate tables, but maintain an inheritance relationship between them using the "id" column that refers to the main table.

### Data insertion 

````
-- Insert data into the people table 
INSERT INTO people (name, age) VALUES ('John Drink', 25);

-- Insert data into the students table
INSERT INTO students (course) VALUES ('Computer Science');

-- Insert data into the teachers table
INSERT INTO teachers (department) VALUES ('Mathematics');
````

### Querys

* Retrieving data:

````
select * from people;
 person_id |   name   | age
-----------+----------+-----
         1 | John Doe |  25
         2 |          |
         3 |          |
(3 rows)

select * from students;
 person_id | name | age | student_id |      course
-----------+------+-----+------------+------------------
         2 |      |     |          1 | Computer Science
(1 row)

select * from teachers;
 person_id | name | age | teacher_id | department
-----------+------+-----+------------+-------------
         3 |      |     |          1 | Mathematics
(1 row)

````

* Manipulating data:

````
 UPDATE people SET name = 'Michael Owen', age = 35 WHERE person_id = 2;
 UPDATE people SET name = 'Connor Al-Hain', age = 45 WHERE person_id = 3;
 ````

* As a result the child table inherits the data from the parent.

````
select * from people;
 person_id |      name      | age
-----------+----------------+-----
         1 | John Doe       |  25
         2 | Michael Owen   |  35
         3 | Connor Al-Hain |  45
(3 rows)

select * from students;
 person_id |     name     | age | student_id |      course
-----------+--------------+-----+------------+------------------
         2 | Michael Owen |  35 |          1 | Computer Science
(1 row)

select * from teachers;
 person_id |      name      | age | teacher_id | department
-----------+----------------+-----+------------+-------------
         3 | Connor Al-Hain |  45 |          1 | Mathematics
(1 row)
````
