# Database Project for BDFC

The scope of this project is to use all the SQL knowledge gained throught the Software Testing course and apply them in practice.

# Application under test: **BDFC** 

### Tools used: MySQL Workbench

Database description: **The purpose of this database is to manage the teaching activity within an imaginary faculty.**


**Database Schema**

You can find below the database schema that was generated through Reverse Engineer and which contains all the tables and the relationships between them.
  
<center><ul><img width="703" alt="BDFC_Reverse engineering" src="https://github.com/constantinivancu/Proiect-pentru-IT-Factory/assets/168174492/eed44531-e3b3-48ac-9bfa-f9c535826e62">
</ul></center></li><br>

### The tables are connected in the following way:

I created a series of tables that I interconnected with secondary keys:

Table **Departments** is connected with table **Professors** through a 1:n relationship which was implemented through Departments.
    department_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY as a primary key and Professors.department_id INT,
    FOREIGN KEY as a foreign key.
Table **Professors** is connected with table **Grades** through a 1:n relationship which was implemented through Professors.
