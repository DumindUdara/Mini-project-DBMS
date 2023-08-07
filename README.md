# Mini-project-DBMS
Hostel Room allocation system project

## INTODUCTION 
DATABASE CURD OPERATION 
CRUD stands for Create, Read (Retrieve), Update, and Delete, which are the fundamental operations used in database management to interact with data. These operations are essential for managing the data stored in a database. Here's a brief explanation of each CRUD operation.
I.	Create (C)
Create operation is used to add new data or records to the database. It involves inserting new rows into the tables. For example, when a new student registers, their information is added to the "student" table.
INSERT INTO table_name (column1, column2, ...) VALUES (value1, value2, ...);

II.	Read (R)
Read operation is used to retrieve data from the database. It involves querying the database to fetch specific records or information. 
For example, when a user wants to view all students in a particular department, a SELECT query is used to retrieve the data.
SELECT * FROM table_name WHERE condition;

III.	Update (U):
Update operation is used to modify existing data in the database. It involves changing the values of certain columns in the rows of a table. 
For example, when a student changes their phone number, the "Mob_no" field is updated in the "student" table.
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;

IV.	Delete (D)
Delete operation is used to remove data or records from the database. It involves deleting specific rows from the tables. 
For example, when a student graduates, their information can be removed from the "student" table.
DELETE FROM table_name WHERE condition;

truncate table_name WHERE condition;
	truncate query is recommended query greater than delete query in table. 

Delete Database: 
drop database Database_Name;
Let's focus on implementing a simple room management system using CRUD operations in the context of hostel management. This system will handle the basic functionalities of adding, viewing, updating, and deleting hostel room information and student details.

Section 02: QUERIES IN OUR PROJECT 
02.1: Database
02.1.1: Create Database:
CREATE DATABASE hostel_management_system_campus;
02.1.2: Use created database:
use hostel_management_system_campus;

02.2: Tables 
02.2.1: Hostel
02.2.1.1: Crate Query:
	Create Tables
CREATE TABLE hostel(
    Hostel_id int(10) NOT NULL AUTO_INCREMENT,
    Hostel_name varchar(255) NOT NULL,
    current_no_of_rooms varchar(255) DEFAULT NULL,
    No_of_rooms varchar(255) DEFAULT NULL,
    No_of_students varchar(255) DEFAULT NULL,
    CONSTRAINT PRIMARY KEY (Hostel_id)
);

02.2.1.2: Describe Query: 
describe hostel; --> to describe table
or
desc hostel; --> to describe table

 

02.2.1.3: Insert Query 
insert into hostel(Hostel_name,current_no_of_rooms,No_of_rooms,No_of_students) 
values('Boys Hostel-1','20','50','100');

insert into hostel(Hostel_name,current_no_of_rooms,No_of_rooms,No_of_students) values
('Boys Hostel-2','50','50','200'),
('Girls Hostel-1','10','90','20'),
('Girls Hostel-2','30','50','100'),
('Out side -1','20','50','100'),
('Out Side -2','20','50','100');

02.2.1.4: Select Query 
select * from hostel;

 




02.2.1.5: Update Query 
	We want to rename ‘Out side - 2’ to ‘Update Outside Hostel’.
UPDATE hostel SET Hostel_name = 'Update Outside Hostel' WHERE Hostel_id = 6;

 

02.2.2: Hostel Manager
02.2.2.1: Create Query:
CREATE TABLE hostel_manager (
    Hostel_man_id int(10) NOT NULL AUTO_INCREMENT,
    Username varchar(20) NOT NULL,
    Fname varchar(20) NOT NULL,
    Lname varchar(205) NOT NULL,
    Mob_no varchar(15) NOT NULL,
    Hostel_id int(10) NOT NULL,
    Pwd varchar(50) NOT NULL,
    Isadmin tinyint(1) DEFAULT '0',
    CONSTRAINT PRIMARY KEY (Hostel_man_id),
    CONSTRAINT UNIQUE (Username),
    CONSTRAINT FOREIGN KEY (Hostel_id) REFERENCES Hostel (Hostel_id)
) ;

 
02.2.2.2: Insert Query 
INSERT INTO hostel_manager (Username, Fname, Lname, Mob_no, Pwd, Isadmin)
VALUES ('Dumindu', 'Dumindu', 'Udara', '0750503932', '11', 1);

INSERT INTO hostel_manager (Username, Fname, Lname, Mob_no, Hostel_id, Pwd, Isadmin)
VALUES ('Oshadhi', 'Oshadhi', 'Wikramasinghe', '0750000932', 2, '110', 1),
       ('Gayantha', 'Gayantha', 'Iroshan', '0750500932', 3, '11', 1);


02.2.2.3: Select Query:
select * from hostel_manager;

 
02.2.2.4: Update Query :
We want to update Duminda’s user name, mobile number and password.
UPDATE hostel_manager SET Username = 'update Dumindu',Mob_no = '01700222576', Pwd = 'udaranew' WHERE hostel_man_id = 1; 







02.2.2.5: Delete Query 
I need to delete Gayantha in admin board.
DELETE FROM hostel_manager WHERE Username = 'Gayantha';


02.2.3: Room
02.2.3.1: Create Query 
CREATE TABLE room (
    Room_id int(10) NOT NULL AUTO_INCREMENT,
    Hostel_id int(10) NOT NULL,
    Room_No int(10) NOT NULL,
    Allocated tinyint(1) DEFAULT '0',
    PRIMARY KEY (Room_id),
    CONSTRAINT FOREIGN KEY (Hostel_id) REFERENCES Hostel (Hostel_id)
);








02.2.3.2: Insert Query 
INSERT INTO room (Hostel_id,Room_No,Allocated) VALUES ('1',1,1);

INSERT INTO room (Hostel_id,Room_No,Allocated) VALUES ('1',11,1), 
('1',10,1), ('1',19,1), ('1',22,1), ('1',44,1), ('1',9,1), ('1',12,1);

INSERT INTO room (Hostel_id,Room_No,Allocated) VALUES ('2',2,1), ('2',10,1), ('2',55,1);

02.2.3.3: Select Query 
select * from room;

 
02.2.3.4: Update and Delete Query:
I want to update Room number 12 to 99 and delete Room id 11 row. 
Update 
UPDATE room SET Room_No = '99' WHERE Room_id = 8;
Delete 
DELETE FROM room WHERE Room_id = 11;

 


02.2.4: Furniture 
02.2.4.1: Create Query:
CREATE TABLE furniture (
  Furniture_id int(100) NOT NULL AUTO_INCREMENT,
      Furniture_type varchar(255) NOT NULL,
      Hostel_id int(10) NOT NULL,
      Room_id int(10) DEFAULT NULL,
      PRIMARY KEY (Furniture_id),
      CONSTRAINT FOREIGN KEY (Room_id) REFERENCES Room (Room_id),
      CONSTRAINT FOREIGN KEY (Hostel_id) REFERENCES Hostel (Hostel_id)
);

 
02.2.4.2: Insert Query 
INSERT INTO furniture (Furniture_type,Hostel_id,Room_id) VALUES ('Chair',1,10);
INSERT INTO furniture (Furniture_type,Hostel_id,Room_id) VALUES ('Bed',2,2),('Chair',2,10),('Table',2,55);

02.2.4.3: Select Query
  




02.2.5: Student
02.2.5.1: Create Query:
CREATE TABLE student (
    Student_id varchar(20) NOT NULL,
    Fname varchar(60) NOT NULL,
    Lname varchar(60) NOT NULL,
    Mob_no varchar(15) NOT NULL,
    Dept varchar(10) NOT NULL,
    Year_of_study varchar(10) NOT NULL,
    Pwd varchar(20) NOT NULL,
    Hostel_id int(10) DEFAULT NULL,
    Room_id int(10) DEFAULT NULL,
    PRIMARY KEY (Student_id),
    CONSTRAINT FOREIGN KEY (Hostel_id) REFERENCES Hostel (Hostel_id),
    CONSTRAINT FOREIGN KEY (Room_id) REFERENCES Room (Room_id)
);










02.2.5.2: Insert Query 
INSERT INTO student 
VALUES ('AA1010', 'Test_1', 'Test_01', '07854543632', 'Engineering', '2025', '00' , 1,11);

INSERT INTO student (Student_id, Fname, Lname, Mob_no, Dept, Year_of_study, Pwd, Hostel_id, Room_id)
VALUES('AA1011', 'Test_2', 'Test_02', '07754543632', 'Engineering', '2025', '001', 1, 10),
      ('AA1022', 'Test_3', 'Test_03', '0794543632', 'IT', '2024', '99', 1, 9),
      ('AA1033', 'Test_4', 'Test_04', '01154543632', 'Music', '2023', '400', 2, 10),
      ('AA1000', 'Test_5', 'Test_05', '07855543632', 'IT', '2025', '500', 2, 55),
      ('AAB2020', 'Test_6', 'Test_06', '07654543632', 'Agri', '2025', 'xx0', 1, 44);


02.2.5.3: Select Query  

02.2.5.4: Update and Delete Query 
I want to update student id of Test_6 and AA1000 student remove the table. 
UPDATE student SET Student_id = 'UPDATE2020' WHERE Fname = 'Test_6';

DELETE FROM student WHERE Student_id = 'AA1000';









02.2.6: Message
02.2.6.1: Create Query:
CREATE TABLE message(
    msg_id int(10) NOT NULL AUTO_INCREMENT,
    sender_id varchar(20) DEFAULT NULL,
    receiver_id varchar(40) DEFAULT NULL,
    hostel_id int(10) DEFAULT NULL,
    subject_h varchar(255) DEFAULT NULL,
    message varchar(255) DEFAULT NULL,
    msg_date varchar(60) DEFAULT NULL,
    msg_time varchar(60) DEFAULT NULL,
    CONSTRAINT PRIMARY KEY (msg_id),
    CONSTRAINT FOREIGN KEY (hostel_id) REFERENCES Hostel (Hostel_id)
);

 

02.2.6.2: Insert Query
INSERT INTO message (sender_id, receiver_id, hostel_id, subject_h, message, msg_date, msg_time)
VALUES ('text@gmail.com', 'admin@gmail.com', 2, 'Change my Room', 'I want to go to the outside hostel', '2023-07-06', '8.00 am');



02.2.7: Visitor 
02.2.7.1: Crate Query 
CREATE TABLE visitor (
    visitor_id INT(10) NOT NULL AUTO_INCREMENT,
    in_time VARCHAR(5) DEFAULT NULL,
    out_time VARCHAR(5) DEFAULT NULL,
    date VARCHAR(30) DEFAULT NULL,
    v_name VARCHAR(69) NOT NULL,
    Student_id VARCHAR(20) NOT NULL,
    PRIMARY KEY (visitor_id),
    CONSTRAINT FOREIGN KEY (Student_id) REFERENCES student (Student_id)
);

 

02.2.7.2: Insert Query 
INSERT INTO visitor (in_time, out_time, date, v_name, Student_id) 
VALUES ('9.00','12.00','2023-03-2','Kaplana','AA1022');

INSERT INTO visitor (in_time, out_time, date, v_name, Student_id) 
VALUES ('3.00','5.00','2023-03-4','Surani','AA1033');

02.2.7.3: Select Query 
 


