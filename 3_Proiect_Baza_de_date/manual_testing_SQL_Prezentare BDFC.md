# Database Project for BDFC

The scope of this project is to use all the SQL knowledge gained throught the Software Testing course and apply them in practice.

## Application under test: **BDFC** 

### Tools used: MySQL Workbench

Database description: **The purpose of this database is to manage the teaching activity within an imaginary faculty.**


## Database Schema

You can find below the database schema that was generated through Reverse Engineer and which contains all the tables and the relationships between them.

![BDFC](https://github.com/constantinivancu/Proiect-pentru-IT-Factory/blob/main/3_Proiect_Baza_de_date/BDFC_Reverse%20engineering.png)


### The tables are connected in the following way:
1. Table **Departments** is connected with table **Professors** through a 1:n relationship which was implemented through Departments.
    department_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY as a primary key and Professors.department_id INT,
    FOREIGN KEY as a foreign key.
2. Table **Professors** is connected with table **Grades** through a 1:n relationship which was implemented through Professors.
    professor_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY as a primary key and Grades.professor_id INT FOREIGN KEY as a foreign key.</li>
3. Table **Students** is connected with table **Grades** through a 1:n relationship which was implemented through Students.student_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY as a primary key and Grades.student_id INT FOREIGN KEY as a foreign key.</li>
4. Table **Objects** is connected with table **Grades** through a 1:n relationship which was implemented through Objects.object_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY as a primary key and Grades.object_id INT FOREIGN KEY as a foreign key.</li>
5. Table **Students** is connected with table **Scores** through a 1:n relationship which was implemented through Students.student_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY as a primary key and Scores.student_id INT FOREIGN KEYas a foreign key.</li>
6. Table **Students** is connected with table **Enrollments** through a 1:n relationship which was implemented through Students.student_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY as a primary key and Enrollments.student_id INT FOREIGN KEY as a foreign key.</li>
7. Table **Objects** is connected with table **Enrollments** through a 1:n relationship which was implemented through Objects.object_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY as a primary key and Enrollments.object_id INT FOREIGN KEY as a foreign key.</li>
8. Table **Objects** is connected with table **Assessments** through a 1:n relationship which was implemented through Objects.object_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY as a primary key and Assessments.object_id INT FOREIGN KEY as a foreign key.</li>
9. Table **Assessments** is connected with table **Scores** through a 1:n relationship which was implemented through Assessments.assessment_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY as a primary key and Scores.assessment_id INT FOREIGN KEY as a foreign key.</li>

## Database Queries
 
 ### DDL (Data Definition Language)
  The following instructions were written in the scope of **CREATING** the structure of the database (CREATE INSTRUCTIONS)
  
  ### Create database *faculty*
``CREATE DATABASE faculty;``
  ### Create table *Departments*  
``CREATE TABLE Departments (
    department_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    department_name VARCHAR(100),
    department_head VARCHAR(100),
    CONSTRAINT unique_department_head UNIQUE (department_head)
);``
### Create *Professors* table
``CREATE TABLE Professors (
    professor_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    professor_name VARCHAR(100),
    professor_email VARCHAR(100),
    department_id INT,
    FOREIGN KEY (department_id) REFERENCES Departments(department_id)
);``
### Create *Students* table
``CREATE TABLE Students (
    student_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    student_name VARCHAR(100),
    student_email VARCHAR(100),
    date_of_birth DATE
);``
Create *Objects (Courses)* table
``CREATE TABLE Objects (
    object_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    object_name VARCHAR(100),
    object_description TEXT
);``

### Create *Grades* table
``CREATE TABLE Grades (
    grade_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    student_id INT,
    object_id INT,
    professor_id INT,
    grade_value DECIMAL(4, 2),
    grade_date DATE,
    FOREIGN KEY (student_id) REFERENCES Students(student_id),
    FOREIGN KEY (professor_id) REFERENCES Professors(professor_id),
    FOREIGN KEY (object_id) REFERENCES Objects(object_id)
);``

### Create *Enrollments* table
``CREATE TABLE Enrollments (
    enrollment_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    student_id INT,
    object_id INT,
    enrollment_date DATE,
    completion_status VARCHAR(50),
    FOREIGN KEY (student_id) REFERENCES Students(student_id),
    FOREIGN KEY (object_id) REFERENCES Objects(object_id)
);``

### Create *Assessments* table
``CREATE TABLE Assessments (
    assessment_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    object_id INT,
    assessment_name VARCHAR(100),
    assessment_date DATE,
    total_points DECIMAL(6, 2),
    FOREIGN KEY (object_id) REFERENCES Objects(object_id)
);``

### Create *Scores* table
``CREATE TABLE Scores (
    score_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    assessment_id INT,
    student_id INT,
    score_value DECIMAL(5, 2),
    FOREIGN KEY (assessment_id) REFERENCES Assessments(assessment_id),
    FOREIGN KEY (student_id) REFERENCES Students(student_id)
);``

  ### After the database and the tables have been created, a few **ALTER** instructions were written in order to update the structure of the database, as described below:  
  
- **Adding the date_of_birth column to professors table**
 ``ALTER TABLE professors ADD column date_of_birth DATE;``  
- **Change the name of the professors column to teachers** 
 ``ALTER TABLE professors RENAME  to `teachers`;``  
- **Renaming the date_of_birth column to zi de nastere**
``ALTER TABLE professors RENAME column `date_of_birth` to `zi de nastere`;``  
- **Delete a column**
``ALTER TABLE professors DROP column `zi de nastere`;``

  
## DML (Data Manipulation Language)

 > In order to be able to use the database I populated the tables with various data necessary in order to perform queries and manipulate the data. 
  In the testing process, this necessary data is identified in the Test Design phase and created in the Test Implementation phase. 
  Below you can find all the insert instructions that were created in the scope of this project:

  
### Inserting Departaments
  
``INSERT INTO Departments (department_id, department_name, department_head)
VALUES,  
(1,' Departamentul de Informatică',' Alex Vasilescu'),  
(2,' Departamentul de Matematică',' Bianca Radulescu'),  
(3,' Departamentul de Fizică',' Elena Dobre'),  
(4,' Departamentul de Chimie',' Irina Tudor'),  
(5,' Departamentul de Biologie',' Roxana Popescu'),  
(6,' Departamentul de Inginerie',' Bianca Ionescu'),  
(7,' Departamentul de Economie',' Elena Stanciu'),  
(8,' Departamentul de Istorie',' Sorin Iancu'),  
(9,' Departamentul de Psihologie',' Roxana Florea'),  
(10,' Departamentul de Sociologie',' Roxana Marinescu');``
  

### Inserting Professors

``INSERT INTO Professors (professor_id, professor_name, professor_email, department_id)
VALUES,
(1,' Alex Vasilescu',' alex.vasilescu@facultate.ro',1),
(2,' Bianca Radulescu',' bianca.radulescu@facultate.ro',2),
(3,' Elena Dobre',' elena.dobre@facultate.ro',3),
(4,' Irina Tudor',' irina.tudor@facultate.ro',4),
(5,' Roxana Popescu',' roxana.popescu@facultate.ro',5),
(6,' Bianca Ionescu',' bianca.ionescu@facultate.ro',6),
(7,' Elena Stanciu',' elena.stanciu@facultate.ro',7),
(8,' Sorin Iancu',' sorin.iancu@facultate.ro',8),
(9,' Roxana Florea',' roxana.florea@facultate.ro',9),
(10,' Roxana Marinescu',' roxana.marinescu@facultate.ro',10),
(11,' Andrei Popa',' andrei.popa@facultate.ro',1),
(12,' Maria Gheorghe',' maria.gheorghe@facultate.ro',2),
(13,' Adrian Munteanu',' adrian.munteanu@facultate.ro',3),
(14,' Ana Dumitrescu',' ana.dumitrescu@facultate.ro',4),
(15,' Ion Stanescu',' ion.stanescu@facultate.ro',5),
(16,' Gabriela Ionescu',' gabriela.ionescu@facultate.ro',6),
(17,' Florin Radu',' florin.radu@facultate.ro',7),
(18,' Elena Vasile',' elena.vasile@facultate.ro',8),
(19,' Mihai Popescu',' mihai.popescu@facultate.ro',9),
(20,' Roxana Petrescu',' roxana.petrescu@facultate.ro',10);``

### Insert professor
``INSERT INTO Professors (professor_id, professor_name, professor_email, date_of_birth, department_id)
VALUES (21,'Tudor Vianu', 'tudor.vianu@facultate.ro','1898-01-08',1);``

### Inserting Students

``INSERT INTO Students (student_id, student_name, student_email, date_of_birth)
VALUES,
(1,' Steven Ruiz ',' steven.ruiz@s.facultate.ro','1997-10-13'),
(2,' Ernest Turner ',' ernest.turner@s.facultate.ro','2000-5-24'),
(3,' Alicia Cain ',' alicia.cain@s.facultate.ro','2004-11-28'),
(4,' Garrett Smith ',' garrett.smith@s.facultate.ro','2001-10-2'),
(5,' William Villarreal ',' william.villarreal@s.facultate.ro','2002-3-5'),
(6,' Kimberly Gilbert ',' kimberly.gilbert@s.facultate.ro','1997-8-1'),
(7,' Emily Delgado ',' emily.delgado@s.facultate.ro','2003-10-15'),
(8,' Natalie Brown ',' natalie.brown@s.facultate.ro','2000-9-26'),
(9,' Gary Hull ',' gary.hull@s.facultate.ro','2000-4-13'),
(10,' Deborah Yates ',' deborah.yates@s.facultate.ro','1995-10-1'),
(11,' Emily Mooney ',' emily.mooney@s.facultate.ro','1996-3-12'),
(12,' Daniel Foster ',' daniel.foster@s.facultate.ro','1997-7-20'),
(13,' Laura Simmons ',' laura.simmons@s.facultate.ro','1998-8-18'),
(14,' Samuel Adams ',' samuel.adams@s.facultate.ro','1999-4-22'),
(15,' Jessica Howard ',' jessica.howard@s.facultate.ro','1996-7-9'),
(16,' Robert Ferrell ',' robert.ferrell@s.facultate.ro','2000-4-9'),
(17,' Sara Nguyen ',' sara.nguyen@s.facultate.ro','1997-4-3'),
(18,' Michael Carter ',' michael.carter@s.facultate.ro','1998-12-6'),
(19,' Jennifer Lee ',' jennifer.lee@s.facultate.ro','1999-2-19'),
(20,' Christopher White ',' christopher.white@s.facultate.ro','1996-9-11'),
(21,' Amanda Hall ',' amanda.hall@s.facultate.ro','1995-12-25'),
(22,' Benjamin Scott ',' benjamin.scott@s.facultate.ro','1997-7-14'),
(23,' Rachel Harris ',' rachel.harris@s.facultate.ro','1998-2-5'),
(24,' Jonathan King ',' jonathan.king@s.facultate.ro','1999-9-17'),
(25,' Megan Turner ',' megan.turner@s.facultate.ro','1996-6-4'),
(26,' Brandon Martinez ',' brandon.martinez@s.facultate.ro','1997-3-21'),
(27,' Lauren Adams ',' lauren.adams@s.facultate.ro','1998-11-8'),
(28,' Kevin Johnson ',' kevin.johnson@s.facultate.ro','1995-1-16'),
(29,' Stephanie Clark ',' stephanie.clark@s.facultate.ro','1996-7-23'),
(30,' Timothy Lewis ',' timothy.lewis@s.facultate.ro','1999-8-30'),
(31,' Victoria Moore ',' victoria.moore@s.facultate.ro','1995-10-27'),
(32,' Nicholas Hall ',' nicholas.hall@s.facultate.ro','1998-5-2'),
(33,' Emily Adams ',' emily.adams@s.facultate.ro','1997-9-4'),
(34,' Jacob Garcia ',' jacob.garcia@s.facultate.ro','1996-11-26'),
(35,' Olivia Rodriguez ',' olivia.rodriguez@s.facultate.ro','1999-9-13'),
(36,' Ethan Wright ',' ethan.wright@s.facultate.ro','1996-10-3'),
(37,' Isabella Perez ',' isabella.perez@s.facultate.ro','1997-8-18'),
(38,' Alexander Turner ',' alexander.turner@s.facultate.ro','1995-7-1'),
(39,' Sophia Adams ',' sophia.adams@s.facultate.ro','1998-4-22'),
(40,' Thomas Miller ',' thomas.miller@s.facultate.ro','2002-1-11'),
(41,' Albert Parker ',' albert.parker@s.facultate.ro','1995-3-2'),
(42,' Amanda Galvan ',' amanda.galvan@s.facultate.ro','2003-10-11'),
(43,' Debra Martin ',' debra.martin@s.facultate.ro','1996-9-30'),
(44,' Gail Meza ',' gail.meza@s.facultate.ro','1997-8-18'),
(45,' Ian Kirk ',' ian.kirk@s.facultate.ro','2000-1-16'),
(46,' Harold Nicholson ',' harold.nicholson@s.facultate.ro','1998-2-5'),
(47,' Steven Smith ',' steven.smith@s.facultate.ro','2003-5-27'),
(48,' Jeremiah Carson ',' jeremiah.carson@s.facultate.ro','2002-6-30'),
(49,' Christopher Miller ',' christopher.miller@s.facultate.ro','1996-4-21'),
(50,' Joel Thomas ',' joel.thomas@s.facultate.ro','2001-7-2');``

### Inserting Objects (Courses)

``INSERT INTO Objects (object_id, object_name, object_description)
VALUES,
(1,'Generații și războaie culturale',' Lorem ipsum dolor sit amet, consectetur adipiscing elit'),
(2,'Abandon–atașament-prevenție și intervenție-Consiliere',' Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua'),
(3,'Abilitare,formare și supervizare a comportamentului terapeutic',' Ut enim ad minim veniam, quis nostrud exercitation ullamco'),
(4,'Abordarea psihoterapeutică a cuplului',' Duis aute irure dolor in reprehenderit in voluptate velit esse'),
(5,'Achiziţia şi procesarea semnalelor biomedicale',' Excepteur sint occaecat cupidatat non proident, sunt in culpa'),
(6,'Achiziţii publice',' Lorem ipsum dolor sit amet, consectetur adipiscing elit'),
(7,'Administrație publică',' Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua'),
(8,'Alaturka şi alafranga: modernizarea Imperiului otoman în secolul al XIX-lea',' Ut enim ad minim veniam, quis nostrud exercitation ullamco'),
(9,'Algebra liniara, geometrie analitica si diferentiala',' Duis aute irure dolor in reprehenderit in voluptate velit esse'),
(10,'Analiza bazinelor de sedimentare',' Excepteur sint occaecat cupidatat non proident, sunt in culpa'),
(11,'Biologie reproductivă in vitro',' Lorem ipsum dolor sit amet, consectetur adipiscing elit'),
(12,'Biologie și etiopatogenie',' Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua'),
(13,'Caracterizarea fasciculului laser',' Ut enim ad minim veniam, quis nostrud exercitation ullamco'),
(14,'Climatologie urbană',' Duis aute irure dolor in reprehenderit in voluptate velit esse'),
(15,'Comunicare instituțională eclezială',' Excepteur sint occaecat cupidatat non proident, sunt in culpa'),
(16,'Cunoaşterea lui Dumnezeu în teologia ortodoxă contemporană',' Lorem ipsum dolor sit amet, consectetur adipiscing elit'),
(17,'Dispersia poluanților in mediu',' Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua'),
(18,'Drept procesual penal: Cooperarea judiciară internaţională în materie penală',' Ut enim ad minim veniam, quis nostrud exercitation ullamco'),
(19,'Economie comportamentală',' Duis aute irure dolor in reprehenderit in voluptate velit esse'),
(20,'Elemente de cataliză',' Excepteur sint occaecat cupidatat non proident, sunt in culpa'),
(21,'Elemente de chimie pentru restaurare',' Lorem ipsum dolor sit amet, consectetur adipiscing elit'),
(22,'Evaluarea performanței resurselor umane',' Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua'),
(23,'Evoluția Chinei în relații internaționale',' Ut enim ad minim veniam, quis nostrud exercitation ullamco'),
(24,'Formarea și evaluarea competențelor profesionale',' Duis aute irure dolor in reprehenderit in voluptate velit esse'),
(25,'Fotogrametrie',' Excepteur sint occaecat cupidatat non proident, sunt in culpa'),
(26,'Gândire critică în dezbaterile publice',' Lorem ipsum dolor sit amet, consectetur adipiscing elit'),
(27,'Genetica comportamentului uman',' Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua'),
(28,'Genetica cu elemente de genetica populațiilor',' Ut enim ad minim veniam, quis nostrud exercitation ullamco'),
(29,'Genetică umană',' Duis aute irure dolor in reprehenderit in voluptate velit esse'),
(30,'Limbajul simbolic creștin',' Excepteur sint occaecat cupidatat non proident, sunt in culpa');``
 
### Inserting Grades

``INSERT INTO Grades (grade_id, student_id, object_id, professor_id, grade_value, grade_date)
VALUES,
(1, 1, 1, 1, 85.5, '2024-05-15'),
(2, 1, 2, 2, 78.2, '2024-06-20'),
(3, 2, 1, 1, 90.0, '2024-05-18'),
(4, 2, 2, 2, 82.7, '2024-06-22'),
(5, 3, 3, 3, 87.5, '2024-05-30'),
(6, 3, 4, 4, 80.0, '2024-06-15'),
(7, 4, 5, 5, 85.0, '2024-05-30'),
(8, 4, 6, 6, 77.0, '2024-06-15'),
(9, 5, 7, 7, 90.5, '2024-05-30'),
(10, 5, 8, 8, 82.0, '2024-06-15'),
(11, 6, 9, 9, 88.0, '2024-05-30'),
(12, 6, 10, 10, 79.5, '2024-06-15');``

### Inserting Enrollments

``INSERT INTO Enrollments (enrollment_id, student_id, object_id, enrollment_date, completion_status)
VALUES,
(1, 1, 1, '2024-01-10', 'completed'),
(2, 1, 2, '2024-01-15', 'in progress'),
(3, 2, 1, '2024-01-12', 'completed'),
(4, 2, 2, '2024-01-20', 'in progress'),
(5, 3, 3, '2024-02-01', 'completed'),
(6, 3, 4, '2024-02-05', 'in progress',
(7, 4, 5, '2024-02-10', 'completed'),
(8, 4, 6, '2024-02-15', 'in progress'),
(9, 5, 7, '2024-02-20', 'completed'),
(10, 5, 8,'2024-02-25','in progress'),
(11, 6, 9,'2024-03-01', 'completed'),
(12, 6, 10,'2024-03-05', 'in progress',
(13, 7, 1, '2024-03-10', 'completed'),
(14, 7, 2, '2024-03-15', 'in progress',
(15, 8, 3, '2024-03-20', 'completed'),
(16, 8, 4, '2024-03-25', 'in progress');``

### Inserting Assessments

``INSERT INTO Assessments (assessment_id, object_id, assessment_name, assessment_date, total_points)
VALUES,
(1, 1, 'Midterm Exam', '2023-03-01', 100),
(2, 1, 'Final Exam', '2023-05-01', 150),
(3, 2, 'Quiz 1', '2023-03-05', 50),
(4, 2, 'Final Exam', '2023-06-01', 150),
(5, 3, 'Test Intermediar', '2024-03-15', 100),
(6, 3, 'Examen Final', '2024-05-25', 150),
(7, 4, 'Proiect de Curs', '2024-04-10', 50),
(8, 4, 'Examen Final', '2024-06-10', 150),
(9, 5, 'Test de Semestru', '2024-03-20', 100),
(10, 5, 'Examen Final', '2024-05-30', 150),
(11, 6, 'Evaluare Practica', '2024-04-15', 50),
(12, 6, 'Examen Final', '2024-06-15', 150);``
       
### Inserting Scores

``INSERT INTO Scores (score_id, assessment_id, student_id, score_value)
VALUES,
(1, 1, 1, 88),
(2, 2, 1, 83),
(3, 3, 2, 92),
(4, 4, 2, 80),
(5, 5, 3, 85),
(6, 6, 3, 90),
(7, 7, 4, 78),
(8, 8, 4, 82),
(9, 9, 5, 88),
(10, 10, 5, 84),
(11, 11, 6, 75),
(12, 12, 6, 80),
(13, 5, 7, 92),
(14, 6, 7, 95),
(15, 7, 8, 81),
(16, 8, 8, 83);``

After the insert, in order to prepare the data to be better suited for the testing process, I updated some data in the following way:
UPDATE departments SET department_name = 'Departamentul de Informatică' WHERE department_id = 1;


## DQL (Data Query Language)

In order to simulate various scenarios that might happen in real life I created the following queries that would cover multiple potential real-life situations:   
``SELECT * FROM departments;``  
``SELECT department_name, department_head FROM departments;``        
``SELECT * FROM Students;``  
``SELECT * FROM Professors;``  
``SELECT * FROM Objects;``  
``SELECT * FROM Grades;``  
``SELECT * FROM Enrollments;``  
``SELECT * FROM Assessments;``  
``SELECT * FROM Scores;``  
``SELECT student_name, date_of_birth FROM Students;``   
``SELECT professor_name, department_id FROM Professors;``  
``SELECT object_name, object_description FROM Objects;``  
``SELECT grade_value, grade_date FROM Grades;``  
``SELECT student_id, object_id, enrollment_date FROM Enrollments;``  
``SELECT assessment_name, assessment_date, total_points FROM Assessments;``  
``SELECT assessment_id, student_id, score_value FROM Scores;``

### Select students with a specific name
``SELECT * FROM Students WHERE student_name =' ' Albert Parker ';``

### Select professors from a specific department
``SELECT * FROM Professors WHERE department_id = 1;``

### Select grades higher than 80
``SELECT * FROM Grades WHERE grade_value > 80;``

### Select assessments with 'Final' in the name
``SELECT * FROM Assessments WHERE assessment_name LIKE '%Final%';``

### Select enrollments completed in 2024 
``SELECT * FROM Enrollments WHERE completion_status = 'completed' AND enrollment_date >= '2024-01-01' AND enrollment_date < '2024-12-31';``  
``SELECT * FROM Enrollments WHERE completion_status = 'in progress' AND (enrollment_date >= '2024-01-01' OR enrollment_date < '2024-12-31');`` 

### Count number of students
``SELECT COUNT(*) AS total_students FROM Students;``

### Calculate average grade value 
``SELECT AVG(grade_value) AS average_grade FROM Grades;``

### Find maximum score value in assessments
``SELECT MAX(score_value) AS max_score FROM Scores;``

### Calculate total points for all assessments in an object
``SELECT object_id, SUM(total_points) AS total_points FROM Assessments GROUP BY object_id;``

### Inner Join: Get student names and their grades
``SELECT s.student_name, g.grade_value
FROM Students s
INNER JOIN Grades g ON s.student_id = g.student_id;``

### Left Join: Get all students and their grades (including students without grades)
``SELECT s.student_name, COALESCE(g.grade_value, 'N/A') AS grade_value
FROM Students s
LEFT JOIN Grades g ON s.student_id = g.student_id;``

### Right Join: Get all grades and their corresponding students (including grades without students)
``SELECT COALESCE(s.student_name, 'N/A') AS student_name, g.grade_value
FROM Students s
RIGHT JOIN Grades g ON s.student_id = g.student_id;``

### Order students by date of birth, oldest first
``SELECT * FROM Students ORDER BY date_of_birth ASC;``

### Order grades by grade value, highest first
``SELECT * FROM Grades ORDER BY grade_value DESC;``

### Limit the number of results returned
``SELECT * FROM Objects LIMIT 10;``

### Order by assessment date and limit results
``SELECT * FROM Assessments ORDER BY assessment_date DESC LIMIT 5;``

### Select students enrolled in both 'Generații și războaie culturale' and 'Abandon–atașament-prevenție și intervenție-Consiliere' 
``SELECT s.student_name, o.object_name
FROM Students AS s
INNER JOIN Enrollments AS e 
ON s.student_id = e.student_id
JOIN Objects AS o ON e.object_id = o.object_id
WHERE o.object_name IN ('Generații și războaie culturale', 'Abandon–atașament-prevenție și intervenție-Consiliere');``

### Select students who scored above 80 in 'Examen Final ' or 'Proiect de curs 1'
``SELECT s.student_name, a.assessment_name, sc.score_value
FROM Students s
JOIN Scores sc ON s.student_id = sc.student_id
JOIN Assessments a ON sc.assessment_id = a.assessment_id
WHERE a.assessment_name IN ('Examen Final', 'Proiect de Curs') AND sc.score_value > 80;``

### Subquery to find the students with the highest grade
``SELECT student_id, student_name
FROM Students
WHERE student_id IN (
    SELECT student_id
    FROM Grades
    WHERE grade_value = (SELECT MAX(grade_value) FROM Grades)
);``

### Subquery to calculate the average score by object
``SELECT object_name, AVG(score_value) AS average_score
FROM Objects
JOIN Assessments ON Objects.object_id = Assessments.object_id
JOIN Scores ON Assessments.assessment_id = Scores.assessment_id
GROUP BY Objects.object_id, object_name
ORDER BY average_score DESC;``

## Conclusions
I created a database for an imaginary college where I learned to create tables, populate them with data, make connections between tables, update some information, delete some data and return the data both at once and with various filters.
