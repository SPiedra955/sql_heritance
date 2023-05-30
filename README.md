# SQL inheritance
### Inheritance

Inheritance in SQL is a concept that allows you to create a hierarchy relationship between tables, where a child table inherits properties and characteristics from a parent table. This is achieved by creating secondary tables that contain specific additional columns, but also include the columns of the primary table.

The following task consist in created your own example of inheritance and show how it works.

# Activity

Suppose you want to model a database of people with different roles, such as students and teachers. You want students and teachers to inherit basic properties from the main table "People".

Here is the database script using inheritance:

````
CREATE TABLE People (
  id INT PRIMARY KEY,
  name VARCHAR(100),
  age INT,
  address VARCHAR(255)
);

CREATE TABLE Students (
  id INT PRIMARY KEY,
  enrolment VARCHAR(10),
  FOREIGN KEY (id) REFERENCES People (id)

CREATE TABLE Teachers (
  id INT PRIMARY KEY,
  especiality VARCHAR(50),
  FOREIGN KEY (id) REFERENCES People(id)
);
````
In this example, the table "Persons" is the main table containing the properties common to all persons, such as ID, name, age and address. Then, two additional tables are created: ````"Students"```` and ````"Teachers"````. These tables inherit the column "id" from the main table using a FOREIGN KEY.

The ````"Students"```` table has additional properties such as "enrolment", while the ````"Teachers"```` table has an additional property called "speciality". By using inheritance, you can store data specific to each type of person in separate tables, but maintain an inheritance relationship between them using the "id" column that refers to the main table.

### Data insertion 

````
-- Table People 
INSERT INTO People (id, name, age, address) VALUES (1, 'Juan Pérez', 25, 'Calle Principal 123');
INSERT INTO People (id, name, age, address) VALUES (2, 'Andrés Parra', 22, 'Calle London 18');
INSERT INTO People (id, name, age, address) VALUES (3, 'Ana Lopéz', 20, 'Calle Guillem III');
INSERT INTO People (id, name, age, address) VALUES (4, 'José Manuel', 20, 'Calle Colom II');
INSERT INTO People (id, name, age, address) VALUES (5, 'Pep Font', 40, 'Calle Piu 9');
INSERT INTO People (id, name, age, address) VALUES (6, 'Abel Munt', 30, 'Calle Rojo 5');

-- Table Students
INSERT INTO Students (id, enrolment) VALUES (1, '20210001');
INSERT INTO Students (id, enrolment) VALUES (2, '21217981');
INSERT INTO Students (id, enrolment) VALUES (3, '20125481');
INSERT INTO Students (id, enrolment) VALUES (4, '23817471');

-- Table Teachers
INSERT INTO Teachers(id, speciality) VALUES (5, 'Mathematics');
INSERT INTO Teachers(id, speciality) VALUES (6, 'History');
````
### Querys

* Obtain all students with their personal information:

````
SELECT People.id, People.name, People.age, People.address, Students.enrolment FROM People INNER JOIN Students ON People.id = Students.id;
````
### Result 

````
 id |     name     | age |       address       | enrolment
----+--------------+-----+---------------------+-----------
  1 | Juan Pérez   |  25 | Calle Principal 123 | 20210001
  2 | Andrés Parra |  22 | Calle London 18     | 21217981
  3 | Ana Lopéz    |  20 | Calle Guillem III   | 20125481
  4 | José Manuel  |  20 | Calle Colom II      | 23817471
(4 rows)
````

* Get all teachers with their personal information:

````
SELECT People.id, People.name, People.age, People.address, Teachers.speciality FROM People INNER JOIN Teachers ON People.id = Teachers.id;
````

### Result

````
 id |    name    | age |       address       |   speciality
----+------------+-----+---------------------+----------------
  1 | Juan Pérez |  25 | Calle Principal 123 | Administration
  5 | Pep Font   |  40 | Calle Piu 9         | Mathematics
  6 | Abel Munt  |  30 | Calle Rojo 5        | History
(3 rows)
````
* SQL query that returns the names of the persons in both tables "Students" and "Teachers".

````
SELECT * FROM People 
INNER JOIN Students ON People.id = Students.id 
INNER JOIN Teachers ON People.id = Teachers.id;
````

### Result

````
 id |    name    | age |       address       | id | enrolment | id |   speciality
----+------------+-----+---------------------+----+-----------+----+----------------
  1 | Juan Pérez |  25 | Calle Principal 123 |  1 | 20210001  |  1 | Administration
(1 row)
````
