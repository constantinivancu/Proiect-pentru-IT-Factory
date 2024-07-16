<h1>Database Project for BDFC</h1>

The scope of this project is to use all the SQL knowledge gained throught the Software Testing course and apply them in practice.

Application under test: **BDFC**

Tools used: **MySQL Workbench**

Database description: **The purpose of this database is to manage the teaching activity within an imaginary faculty.**


**Database Schema**

You can find below the database schema that was generated through Reverse Engineer and which contains all the tables and the relationships between them.
  
<center><ul><img width="703" alt="BDFC_Reverse engineering" src="https://github.com/constantinivancu/Proiect-pentru-IT-Factory/assets/168174492/eed44531-e3b3-48ac-9bfa-f9c535826e62">
</ul></center></li><br>

The tables are connected in the following way:
<ol type="1">

<li>The first table is <b>Test</b>, and has the role of testing various DDL commands (ALTER, TRUNCATE, DROP, etc.)</li>
<li> Table <b>Departments</b> is connected with table <b>Professors</b> through a 1:n relationship which was implemented through Departments.
    department_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY as a primary key and Professors.department_id INT,
    FOREIGN KEY as a foreign key.</li>
<li> Table <b>Professors</b> is connected with table <b>Grades</b> through a 1:n relationship which was implemented through Professors.
    professor_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY as a primary key and Grades.professor_id INT FOREIGN KEY as a foreign key.</li>
<li> Table <b>Students</b> is connected with table <b>Grades</b> through a 1:n relationship which was implemented through Students.student_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY as a primary key and Grades.student_id INT FOREIGN KEY as a foreign key.</li>
<li> Table <b>Objects</b> is connected with table <b>Grades</b> through a 1:n relationship which was implemented through Objects.object_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY as a primary key and Grades.object_id INT FOREIGN KEY as a foreign key.</li>
 <li> Table <b>Students</b> is connected with table <b>Scores</b> through a 1:n relationship which was implemented through Students.student_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY as a primary key and Scores.student_id INT FOREIGN KEYas a foreign key.</li>
<li> Table <b>Students</b> is connected with table <b>Enrollments</b> through a 1:n relationship which was implemented through Students.student_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY as a primary key and Enrollments.student_id INT FOREIGN KEY as a foreign key.</li>
<li> Table <b>Objects</b> is connected with table <b>Enrollments</b> through a 1:n relationship which was implemented through Objects.object_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY as a primary key and Enrollments.object_id INT FOREIGN KEY as a foreign key.</li>
<li> Table <b>Objects</b> is connected with table <b>Assessments</b> through a 1:n relationship which was implemented through Objects.object_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY as a primary key and Assessments.object_id INT FOREIGN KEY as a foreign key.</li>
<li> Table <b>Assessments</b> is connected with table <b>Scores</b> through a 1:n relationship which was implemented through Assessments.assessment_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY as a primary key and Scores.assessment_id INT FOREIGN KEY as a foreign key.</li>

<br>
<b>Database Queries</b>


  
 <b>DDL (Data Definition Language)</b>
  The following instructions were written in the scope of <b>CREATING</b> the structure of the database (CREATE INSTRUCTIONS)
  <ol type="1">
<li>CREATE DATABASE faculty;</li>
<li>CREATE TABLE Test (
coloana_A INT PRIMARY KEY,
coloana_B VARCHAR(20),
coloana_C INT
);</li>
    
<li>CREATE TABLE Departments (
    department_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    department_name VARCHAR(100),
    department_head VARCHAR(100),
    CONSTRAINT unique_department_head UNIQUE (department_head)
);</li>

<li>Create Professors table
CREATE TABLE Professors (
    professor_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    professor_name VARCHAR(100),
    professor_email VARCHAR(100),
    department_id INT,
    FOREIGN KEY (department_id) REFERENCES Departments(department_id)
);</li>

<li>Create Students table
CREATE TABLE Students (
    student_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    student_name VARCHAR(100),
    student_email VARCHAR(100),
    date_of_birth DATE
);</li>

<li>Create Objects (Courses) table
CREATE TABLE Objects (
    object_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    object_name VARCHAR(100),
    object_description TEXT
);</li>

<li>Create Grades table
CREATE TABLE Grades (
    grade_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    student_id INT,
    object_id INT,
    professor_id INT,
    grade_value DECIMAL(4, 2),
    grade_date DATE,
    FOREIGN KEY (student_id) REFERENCES Students(student_id),
    FOREIGN KEY (professor_id) REFERENCES Professors(professor_id),
    FOREIGN KEY (object_id) REFERENCES Objects(object_id)
);</li>

<li>Create Enrollments table
CREATE TABLE Enrollments (
    enrollment_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    student_id INT,
    object_id INT,
    enrollment_date DATE,
    completion_status VARCHAR(50),
    FOREIGN KEY (student_id) REFERENCES Students(student_id),
    FOREIGN KEY (object_id) REFERENCES Objects(object_id)
);</li>

<li>Create Assessments table
CREATE TABLE Assessments (
    assessment_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    object_id INT,
    assessment_name VARCHAR(100),
    assessment_date DATE,
    total_points DECIMAL(6, 2),
    FOREIGN KEY (object_id) REFERENCES Objects(object_id)
);</li>

<li>Create Scores table
CREATE TABLE Scores (
    score_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    assessment_id INT,
    student_id INT,
    score_value DECIMAL(5, 2),
    FOREIGN KEY (assessment_id) REFERENCES Assessments(assessment_id),
    FOREIGN KEY (student_id) REFERENCES Students(student_id)
);</li>

  <br>After the database and the tables have been created, a few <b>ALTER</b> instructions were written in order to update the structure of the database, as described below:

 <b>schimbare nume tabela</b> 
 
 <li>ALTER TABLE Test to Test1;</li>
 
 <b>adaugare sau stergere coloana</b>
 
 <li>ALTER TABLE Test1 ADD column coloana_D DATE;</li>
 <li>ALTER TABLE Test1 DROP column coloana E;</li>
 
  <b>redenumire coloana</b>                                                                          
 <li>ALTER TABLE Test1 RENAME column coloana_A to XYZ;</li>
 
  <b>adaugare proprietati coloana (ex: adaugare auto-increment)</b>
  
 <li>ALTER TABLE Test1 column XYZ INT AUTO_INCREMENT;</li>
 
  <br>DML (Data Manipulation Language)

  In order to be able to use the database I populated the tables with various data necessary in order to perform queries and manipulate the data. 
  In the testing process, this necessary data is identified in the Test Design phase and created in the Test Implementation phase. 

  Below you can find all the insert instructions that were created in the scope of this project:
<ol type="1">
  
<b>Inserting Departaments</b>
  
<br><li>INSERT INTO Departments (department_id, department_name, department_head)
VALUES,

(1,' Departamentul de Informatică',' Alex Vasilescu'),\
(2,' Departamentul de Matematică',' Bianca Radulescu'),\
(3,' Departamentul de Fizică',' Elena Dobre'),\
(4,' Departamentul de Chimie',' Irina Tudor'),\
(5,' Departamentul de Biologie',' Roxana Popescu'),\
(6,' Departamentul de Inginerie',' Bianca Ionescu'),\
(7,' Departamentul de Economie',' Elena Stanciu'),\
(8,' Departamentul de Istorie',' Sorin Iancu'),\
(9,' Departamentul de Psihologie',' Roxana Florea'),\
(10,' Departamentul de Sociologie',' Roxana Marinescu');</li>

<b>Inserting Professors</b>

<br><li>INSERT INTO Professors (professor_id, professor_name, professor_email, department_id)
VALUES,

(1,' Alex Vasilescu',' alex.vasilescu@facultate.ro',1),\
(2,' Bianca Radulescu',' bianca.radulescu@facultate.ro',2),\
(3,' Elena Dobre',' elena.dobre@facultate.ro',3),\
(4,' Irina Tudor',' irina.tudor@facultate.ro',4),\
(5,' Roxana Popescu',' roxana.popescu@facultate.ro',5),\
(6,' Bianca Ionescu',' bianca.ionescu@facultate.ro',6),\
(7,' Elena Stanciu',' elena.stanciu@facultate.ro',7),\
(8,' Sorin Iancu',' sorin.iancu@facultate.ro',8),\
(9,' Roxana Florea',' roxana.florea@facultate.ro',9),\
(10,' Roxana Marinescu',' roxana.marinescu@facultate.ro',10),\
(11,' Andrei Popa',' andrei.popa@facultate.ro',1),\
(12,' Maria Gheorghe',' maria.gheorghe@facultate.ro',2),\
(13,' Adrian Munteanu',' adrian.munteanu@facultate.ro',3),\
(14,' Ana Dumitrescu',' ana.dumitrescu@facultate.ro',4),\
(15,' Ion Stanescu',' ion.stanescu@facultate.ro',5),\
(16,' Gabriela Ionescu',' gabriela.ionescu@facultate.ro',6),\
(17,' Florin Radu',' florin.radu@facultate.ro',7),\
(18,' Elena Vasile',' elena.vasile@facultate.ro',8),\
(19,' Mihai Popescu',' mihai.popescu@facultate.ro',9),\
(20,' Roxana Petrescu',' roxana.petrescu@facultate.ro',10);</li>

<b>Inserting Students</b>

<br><li>INSERT INTO Students (student_id, student_name, student_email, date_of_birth)
VALUES,

(1,' Steven Ruiz ',' steven.ruiz@s.facultate.ro','1997-10-13'),\
(2,' Ernest Turner ',' ernest.turner@s.facultate.ro','2000-5-24'),\
(3,' Alicia Cain ',' alicia.cain@s.facultate.ro','2004-11-28'),\
(4,' Garrett Smith ',' garrett.smith@s.facultate.ro','2001-10-2'),\
(5,' William Villarreal ',' william.villarreal@s.facultate.ro','2002-3-5'),\
(6,' Kimberly Gilbert ',' kimberly.gilbert@s.facultate.ro','1997-8-1'),\
(7,' Emily Delgado ',' emily.delgado@s.facultate.ro','2003-10-15'),\
(8,' Natalie Brown ',' natalie.brown@s.facultate.ro','2000-9-26'),\
(9,' Gary Hull ',' gary.hull@s.facultate.ro','2000-4-13'),\
(10,' Deborah Yates ',' deborah.yates@s.facultate.ro','1995-10-1'),\
(11,' Emily Mooney ',' emily.mooney@s.facultate.ro','1996-3-12'),\
(12,' Daniel Foster ',' daniel.foster@s.facultate.ro','1997-7-20'),\
(13,' Laura Simmons ',' laura.simmons@s.facultate.ro','1998-8-18'),\
(14,' Samuel Adams ',' samuel.adams@s.facultate.ro','1999-4-22'),\
(15,' Jessica Howard ',' jessica.howard@s.facultate.ro','1996-7-9'),\
(16,' Robert Ferrell ',' robert.ferrell@s.facultate.ro','2000-4-9'),\
(17,' Sara Nguyen ',' sara.nguyen@s.facultate.ro','1997-4-3'),\
(18,' Michael Carter ',' michael.carter@s.facultate.ro','1998-12-6'),\
(19,' Jennifer Lee ',' jennifer.lee@s.facultate.ro','1999-2-19'),\
(20,' Christopher White ',' christopher.white@s.facultate.ro','1996-9-11'),\
(21,' Amanda Hall ',' amanda.hall@s.facultate.ro','1995-12-25'),\
(22,' Benjamin Scott ',' benjamin.scott@s.facultate.ro','1997-7-14'),\
(23,' Rachel Harris ',' rachel.harris@s.facultate.ro','1998-2-5'),\
(24,' Jonathan King ',' jonathan.king@s.facultate.ro','1999-9-17'),\
(25,' Megan Turner ',' megan.turner@s.facultate.ro','1996-6-4'),\
(26,' Brandon Martinez ',' brandon.martinez@s.facultate.ro','1997-3-21'),\
(27,' Lauren Adams ',' lauren.adams@s.facultate.ro','1998-11-8'),\
(28,' Kevin Johnson ',' kevin.johnson@s.facultate.ro','1995-1-16'),\
(29,' Stephanie Clark ',' stephanie.clark@s.facultate.ro','1996-7-23'),\
(30,' Timothy Lewis ',' timothy.lewis@s.facultate.ro','1999-8-30'),\
(31,' Victoria Moore ',' victoria.moore@s.facultate.ro','1995-10-27'),\
(32,' Nicholas Hall ',' nicholas.hall@s.facultate.ro','1998-5-2'),\
(33,' Emily Adams ',' emily.adams@s.facultate.ro','1997-9-4'),\
(34,' Jacob Garcia ',' jacob.garcia@s.facultate.ro','1996-11-26'),\
(35,' Olivia Rodriguez ',' olivia.rodriguez@s.facultate.ro','1999-9-13'),\
(36,' Ethan Wright ',' ethan.wright@s.facultate.ro','1996-10-3'),\
(37,' Isabella Perez ',' isabella.perez@s.facultate.ro','1997-8-18'),\
(38,' Alexander Turner ',' alexander.turner@s.facultate.ro','1995-7-1'),\
(39,' Sophia Adams ',' sophia.adams@s.facultate.ro','1998-4-22'),\
(40,' Thomas Miller ',' thomas.miller@s.facultate.ro','2002-1-11'),\
(41,' Albert Parker ',' albert.parker@s.facultate.ro','1995-3-2'),\
(42,' Amanda Galvan ',' amanda.galvan@s.facultate.ro','2003-10-11'),\
(43,' Debra Martin ',' debra.martin@s.facultate.ro','1996-9-30'),\
(44,' Gail Meza ',' gail.meza@s.facultate.ro','1997-8-18'),\
(45,' Ian Kirk ',' ian.kirk@s.facultate.ro','2000-1-16'),\
(46,' Harold Nicholson ',' harold.nicholson@s.facultate.ro','1998-2-5'),\
(47,' Steven Smith ',' steven.smith@s.facultate.ro','2003-5-27'),\
(48,' Jeremiah Carson ',' jeremiah.carson@s.facultate.ro','2002-6-30'),\
(49,' Christopher Miller ',' christopher.miller@s.facultate.ro','1996-4-21'),\
(50,' Joel Thomas ',' joel.thomas@s.facultate.ro','2001-7-2');

<b>Inserting Objects (Courses)</b>

<li>INSERT INTO Objects (object_id, object_name, object_description)
VALUES,
  
(1,'Generații și războaie culturale',' Lorem ipsum dolor sit amet, consectetur adipiscing elit'),\
(2,'Abandon–atașament-prevenție și intervenție-Consiliere',' Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua'),\
(3,'Abilitare,formare și supervizare a comportamentului terapeutic',' Ut enim ad minim veniam, quis nostrud exercitation ullamco'),\
(4,'Abordarea psihoterapeutică a cuplului',' Duis aute irure dolor in reprehenderit in voluptate velit esse'),\
(5,'Achiziţia şi procesarea semnalelor biomedicale',' Excepteur sint occaecat cupidatat non proident, sunt in culpa'),\
(6,'Achiziţii publice',' Lorem ipsum dolor sit amet, consectetur adipiscing elit'),\
(7,'Administrație publică',' Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua'),\
(8,'Alaturka şi alafranga: modernizarea Imperiului otoman în secolul al XIX-lea',' Ut enim ad minim veniam, quis nostrud exercitation ullamco'),\
(9,'Algebra liniara, geometrie analitica si diferentiala',' Duis aute irure dolor in reprehenderit in voluptate velit esse'),\
(10,'Analiza bazinelor de sedimentare',' Excepteur sint occaecat cupidatat non proident, sunt in culpa'),\
(11,'Biologie reproductivă in vitro',' Lorem ipsum dolor sit amet, consectetur adipiscing elit'),\
(12,'Biologie și etiopatogenie',' Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua'),\
(13,'Caracterizarea fasciculului laser',' Ut enim ad minim veniam, quis nostrud exercitation ullamco'),\
(14,'Climatologie urbană',' Duis aute irure dolor in reprehenderit in voluptate velit esse'),\
(15,'Comunicare instituțională eclezială',' Excepteur sint occaecat cupidatat non proident, sunt in culpa'),\
(16,'Cunoaşterea lui Dumnezeu în teologia ortodoxă contemporană',' Lorem ipsum dolor sit amet, consectetur adipiscing elit'),\
(17,'Dispersia poluanților in mediu',' Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua'),\
(18,'Drept procesual penal: Cooperarea judiciară internaţională în materie penală',' Ut enim ad minim veniam, quis nostrud exercitation ullamco'),\
(19,'Economie comportamentală',' Duis aute irure dolor in reprehenderit in voluptate velit esse'),\
(20,'Elemente de cataliză',' Excepteur sint occaecat cupidatat non proident, sunt in culpa'),\
(21,'Elemente de chimie pentru restaurare',' Lorem ipsum dolor sit amet, consectetur adipiscing elit'),\
(22,'Evaluarea performanței resurselor umane',' Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua'),\
(23,'Evoluția Chinei în relații internaționale',' Ut enim ad minim veniam, quis nostrud exercitation ullamco'),\
(24,'Formarea și evaluarea competențelor profesionale',' Duis aute irure dolor in reprehenderit in voluptate velit esse'),\
(25,'Fotogrametrie',' Excepteur sint occaecat cupidatat non proident, sunt in culpa'),\
(26,'Gândire critică în dezbaterile publice',' Lorem ipsum dolor sit amet, consectetur adipiscing elit'),\
(27,'Genetica comportamentului uman',' Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua'),\
(28,'Genetica cu elemente de genetica populațiilor',' Ut enim ad minim veniam, quis nostrud exercitation ullamco'),\
(29,'Genetică umană',' Duis aute irure dolor in reprehenderit in voluptate velit esse'),\
(30,'Limbajul simbolic creștin',' Excepteur sint occaecat cupidatat non proident, sunt in culpa');</li>
 
<b>Inserting Grades</b>

<li>INSERT INTO Grades (grade_id, student_id, object_id, professor_id, grade_value, grade_date)
VALUES,
  
(1, 1, 1, 1, 85.5, '2024-05-15'),\
(2, 1, 2, 2, 78.2, '2024-06-20'),\
(3, 2, 1, 1, 90.0, '2024-05-18'),\
(4, 2, 2, 2, 82.7, '2024-06-22'),\
(5, 3, 3, 3, 87.5, '2024-05-30'),\
(6, 3, 4, 4, 80.0, '2024-06-15'),\
(7, 4, 5, 5, 85.0, '2024-05-30'),\
(8, 4, 6, 6, 77.0, '2024-06-15'),\
(9, 5, 7, 7, 90.5, '2024-05-30'),\
(10, 5, 8, 8, 82.0, '2024-06-15'),\
(11, 6, 9, 9, 88.0, '2024-05-30'),\
(12, 6, 10, 10, 79.5, '2024-06-15');</li>

<b>Inserting Enrollments</b>

<li>INSERT INTO Enrollments (enrollment_id, student_id, object_id, enrollment_date, completion_status)
VALUES,
  
(1, 1, 1, '2024-01-10', 'completed'),\
(2, 1, 2, '2024-01-15', 'completed'),\
(3, 2, 1, '2024-01-12', 'completed'),\
(4, 2, 2, '2024-01-20', 'completed'),\
(5, 3, 3, '2024-02-01', 'completed'),\
(6, 3, 4, '2024-02-05', 'completed'),\
(7, 4, 5, '2024-02-10', 'completed'),\
(8, 4, 6, '2024-02-15', 'completed'),\
(9, 5, 7, '2024-02-20', 'completed'),\
(10, 5, 8, '2024-02-25', 'completed'),\
(11, 6, 9, '2024-03-01', 'completed'),\
(12, 6, 10, '2024-03-05', 'completed'),\
(13, 7, 1, '2024-03-10', 'completed'),\
(14, 7, 2, '2024-03-15', 'completed'),\
(15, 8, 3, '2024-03-20', 'completed'),\
(16, 8, 4, '2024-03-25', 'completed');</li>

<b>Inserting Assessments</b>

<li>INSERT INTO Assessments (assessment_id, object_id, assessment_name, assessment_date, total_points)
VALUES,
  
(1, 1, 'Midterm Exam', '2023-03-01', 100),\
(2, 1, 'Final Exam', '2023-05-01', 150),\
(3, 2, 'Quiz 1', '2023-03-05', 50),\
(4, 2, 'Final Exam', '2023-06-01', 150),\
(5, 3, 'Test Intermediar', '2024-03-15', 100),\
(6, 3, 'Examen Final', '2024-05-25', 150),\
(7, 4, 'Proiect de Curs', '2024-04-10', 50),\
(8, 4, 'Examen Final', '2024-06-10', 150),\
(9, 5, 'Test de Semestru', '2024-03-20', 100),\
(10, 5, 'Examen Final', '2024-05-30', 150),\
(11, 6, 'Evaluare Practica', '2024-04-15', 50),\
(12, 6, 'Examen Final', '2024-06-15', 150);</li>
       
<b>Inserting Scores</b>

<li>INSERT INTO Scores (score_id, assessment_id, student_id, score_value)
VALUES,
  
(1, 1, 1, 88),\
(2, 2, 1, 83),\
(3, 3, 2, 92),\
(4, 4, 2, 80),\
(5, 5, 3, 85),\
(6, 6, 3, 90),\
(7, 7, 4, 78),\
(8, 8, 4, 82),\
(9, 9, 5, 88),\
(10, 10, 5, 84),\
(11, 11, 6, 75),\
(12, 12, 6, 80),\
(13, 5, 7, 92),\
(14, 6, 7, 95),\
(15, 7, 8, 81),\
(16, 8, 8, 83);</li>

After the insert, in order to prepare the data to be better suited for the testing process, I updated some data in the following way:

UPDATE departments SET department_name = 'departament test' WHERE department_id = 1;
UPDATE departments SET department_name = 'Departamentul de Informatică' WHERE department_id = 1;


<b>DQL (Data Query Language)</b>

After the testing process, I deleted the data that was no longer relevant in order to preserve the database clean: 

DELETE from Test1 WHERE coloana_D='2024-07-09';
DROP TABLE Test1;

In order to simulate various scenarios that might happen in real life I created the following queries that would cover multiple potential real-life situations:

<ol type="1">

SELECT * FROM departments;\
SELECT department_name, department_head FROM departments;       
SELECT * FROM Students;\
SELECT * FROM Professors;\
SELECT * FROM Objects;\
SELECT * FROM Grades;\
SELECT * FROM Enrollments;\
SELECT * FROM Assessments;\
SELECT * FROM Scores;\
SELECT student_name, date_of_birth FROM Students;\
SELECT professor_name, department_id FROM Professors;\
SELECT object_name, object_description FROM Objects;\
SELECT grade_value, grade_date FROM Grades;\
SELECT student_id, object_id, enrollment_date FROM Enrollments;\
SELECT assessment_name, assessment_date, total_points FROM Assessments;\
SELECT assessment_id, student_id, score_value FROM Scores;

<b>Select students with a specific name</b>

SELECT * FROM Students WHERE student_name =' ' Albert Parker ';

<b>Select professors from a specific department</b>

SELECT * FROM Professors WHERE department_id = 1;

<b>Select grades higher than 80</b>

SELECT * FROM Grades WHERE grade_value > 80;

<b>Select assessments with 'Final' in the name</b>

SELECT * FROM Assessments WHERE assessment_name LIKE '%Final%';

<b> Select enrollments completed in 2024 </b>

SELECT * FROM Enrollments WHERE completion_status = 'completed' AND enrollment_date >= '2024-01-01' AND enrollment_date < '2024-12-01';\
SELECT * FROM Enrollments WHERE completion_status = 'completed' AND enrollment_date >= '2024-01-01' OR enrollment_date < '2024-12-01';

<b> Count number of students </b>

SELECT COUNT(*) AS total_students FROM Students;

<b> Calculate average grade value </b>

SELECT AVG(grade_value) AS average_grade FROM Grades;

<b> Find maximum score value in assessments </b>

SELECT MAX(score_value) AS max_score FROM Scores;

<b> Calculate total points for all assessments in an object </b>

SELECT object_id, SUM(total_points) AS total_points FROM Assessments GROUP BY object_id;

<b> Inner Join: Get student names and their grades </b>

SELECT s.student_name, g.grade_value
FROM Students s
INNER JOIN Grades g ON s.student_id = g.student_id;

<b> Left Join: Get all students and their grades (including students without grades) </b>

SELECT s.student_name, COALESCE(g.grade_value, 'N/A') AS grade_value
FROM Students s
LEFT JOIN Grades g ON s.student_id = g.student_id;

<b>Right Join: Get all grades and their corresponding students (including grades without students)</b>

SELECT COALESCE(s.student_name, 'N/A') AS student_name, g.grade_value
FROM Students s
RIGHT JOIN Grades g ON s.student_id = g.student_id;

<b>Order students by date of birth, oldest first</b>

SELECT * FROM Students ORDER BY date_of_birth ASC;

<b> Order grades by grade value, highest first </b>

SELECT * FROM Grades ORDER BY grade_value DESC;

<b> Limit the number of results returned </b>

SELECT * FROM Objects LIMIT 10;

<b> Order by assessment date and limit results</b>

SELECT * FROM Assessments ORDER BY assessment_date DESC LIMIT 5;

<b> Select students enrolled in both 'Generații și războaie culturale' and 'Abandon–atașament-prevenție și intervenție-Consiliere' </b>

SELECT s.student_name, o.object_name
FROM Students s
JOIN Enrollments e ON s.student_id = e.student_id
JOIN Objects o ON e.object_id = o.object_id
WHERE o.object_name IN ('Generații și războaie culturale', 'Abandon–atașament-prevenție și intervenție-Consiliere')
GROUP BY s.student_name
HAVING COUNT(DISTINCT o.object_id) = 2;

<b> Select students who scored above 80 in 'Examen Final ' or 'Proiect de curs 1'
SELECT s.student_name, a.assessment_name, sc.score_value
FROM Students s
JOIN Scores sc ON s.student_id = sc.student_id
JOIN Assessments a ON sc.assessment_id = a.assessment_id
WHERE a.assessment_name IN ('Examen Final', 'Proiect de Curs') AND sc.score_value > 80;

<b> subquery to find the students with the highest grade </b>

SELECT student_id, student_name
FROM Students
WHERE student_id IN (
    SELECT student_id
    FROM Grades
    WHERE grade_value = (SELECT MAX(grade_value) FROM Grades)
);

<b> subquery to calculate the average score by object </b>

SELECT object_name, AVG(score_value) AS average_score
FROM Objects
JOIN Assessments ON Objects.object_id = Assessments.object_id
JOIN Scores ON Assessments.assessment_id = Scores.assessment_id
GROUP BY Objects.object_id, object_name
ORDER BY average_score DESC;


</ol>

<b>Conclusions</b>
I created a database for an imaginary college where I learned to create tables, populate them with data, make connections between tables, update some information, delete some data and return the data both at once and with various filters.

</ol>
