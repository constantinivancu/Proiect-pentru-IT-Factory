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

<ol type="a">
  
 <b>DDL (Data Definition Language)</b>
  The following instructions were written in the scope of <b>CREATING</b> the structure of the database (CREATE INSTRUCTIONS)
<li>CREATE DATABASE faculty;</li>
-- USE faculty;
-- CREATE TABLE Test (
coloana_A INT PRIMARY KEY,
coloana_B VARCHAR(20),
coloana_C INT
);
-- CREATE TABLE Departments (
    department_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    department_name VARCHAR(100),
    department_head VARCHAR(100),
    CONSTRAINT unique_department_head UNIQUE (department_head)
);

-- Create Professors table
CREATE TABLE Professors (
    professor_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    professor_name VARCHAR(100),
    professor_email VARCHAR(100),
    department_id INT,
    FOREIGN KEY (department_id) REFERENCES Departments(department_id)
);

-- Create Students table
CREATE TABLE Students (
    student_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    student_name VARCHAR(100),
    student_email VARCHAR(100),
    date_of_birth DATE
);

-- Create Objects (Courses) table
CREATE TABLE Objects (
    object_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    object_name VARCHAR(100),
    object_description TEXT
);

-- Create Grades table
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
);
-- Create Enrollments table
CREATE TABLE Enrollments (
    enrollment_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    student_id INT,
    object_id INT,
    enrollment_date DATE,
    completion_status VARCHAR(50),
    FOREIGN KEY (student_id) REFERENCES Students(student_id),
    FOREIGN KEY (object_id) REFERENCES Objects(object_id)
);

-- Create Assessments table
CREATE TABLE Assessments (
    assessment_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    object_id INT,
    assessment_name VARCHAR(100),
    assessment_date DATE,
    total_points DECIMAL(6, 2),
    FOREIGN KEY (object_id) REFERENCES Objects(object_id)
);

-- Create Scores table
CREATE TABLE Scores (
    score_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    assessment_id INT,
    student_id INT,
    score_value DECIMAL(5, 2),
    FOREIGN KEY (assessment_id) REFERENCES Assessments(assessment_id),
    FOREIGN KEY (student_id) REFERENCES Students(student_id)
);

  After the database and the tables have been created, a few <b>ALTER</b> instructions were written in order to update the structure of the database, as described below:

 **- schimbare nume tabela**                                                                       ALTER TABLE Test to Test1;</li>
 **- adaugare sau stergere coloana**                                                               ALTER TABLE Test1 ADD column coloana_D DATE;
                                                                                                   ALTER TABLE Test1 DROP column coloana E;
 **- redenumire coloana**                                                                          ALTER TABLE Test1 RENAME column coloana_A to XYZ;
 **- adaugare proprietati coloana (ex: adaugare auto-increment)**                                  ALTER TABLE Test1 column XYZ INT AUTO_INCREMENT;

  
  <li>DML (Data Manipulation Language)</li>

  In order to be able to use the database I populated the tables with various data necessary in order to perform queries and manipulate the data. 
  In the testing process, this necessary data is identified in the Test Design phase and created in the Test Implementation phase. 

  Below you can find all the insert instructions that were created in the scope of this project:

  **Inserati aici toate instructiunile de INSERT pe care le-ati scris. Incercati sa folositi atat insert pe toate coloanele (fara sa precizati pe ce coloane se face insert) cat si insert pe cateva coloane (care necesita mentionarea explicita a coloanelor pe care se face insert). De asemenea, incercati sa acoperiti situatia in care inserati mai multe randuri in acelasi timp**

  After the insert, in order to prepare the data to be better suited for the testing process, I updated some data in the following way:

  **Inserati aici toate instructiunile de UPDATE pe care le-ati scris folosind filtrarile necesare astfel incat sa actualizati doar datele de care aveti nevoie**


  <li>DQL (Data Query Language)</li>

After the testing process, I deleted the data that was no longer relevant in order to preserve the database clean: 

**Inserati aici toate instructiunile de DELETE pe care le-ati scris folosind filtrarile necesare astfel incat sa stergeti doar datele de care aveti nevoie**

In order to simulate various scenarios that might happen in real life I created the following queries that would cover multiple potential real-life situations:

**Inserati aici toate instructiunile de SELECT pe care le-ati scris folosind filtrarile necesare astfel incat sa extrageti doar datele de care aveti nevoie**
**Incercati sa acoperiti urmatoarele:**<br>
**- where**<br>
**- AND**<br>
**- OR**<br>
**- NOT**<br>
**- like**<br>
**- inner join**<br>
**- left join**<br>
**- OPTIONAL: right join**<br>
**- OPTIONAL: cross join**<br>
**- functii agregate**<br>
**- group by**<br>
**- having**<br>
**- OPTIONAL DAR RECOMANDAT: Subqueries - nu au fost in scopul cursului. Puteti sa consultati tutorialul [asta](https://www.techonthenet.com/mysql/subqueries.php) si daca nu intelegeti ceva contactati fie trainerul, fie coordonatorul de grupa**<br>

</ol>

<b>Conclusions</b>

**Inserati aici o concluzie cu privire la ceea ce ati lucrat, gen lucrurile pe care le-ati invatat, lessons learned, un rezumat asupra a ceea ce ati facut si orice alta informatie care vi se pare relevanta pentru o concluzie finala asupra a ceea ce ati lucrat**

</ol>
