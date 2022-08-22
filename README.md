# Revision-23-July-
MY SQL QUERIES + HOMEWORK OF 22 JULY 
//////FUNCTION//////PROCEDURE//////
Create procedure so that you dont have to write all the time select * from tb_name
DELIMITER &&
create procedure select_record()
BEGIN
     select * from bank_detail;
     END &&
     
call select_record() : This pull out all the record for you

//////select * from bank_detail where balance= (select max(balance) from bank_detail);
DELIMITER &&
create procedure select_bal_max()
BEGIN
select * from bank_detail where balance= (select max(balance) from bank_detail);
END && 
call select_bal_max() : To call details for max balance 
///select avg(balance) from bank_detail where job = 'admin.'/// 
DELIMITER &&
create procedure avg_admin_job()
BEGIN
select avg(balance) from bank_detail where job = 'admin.';
END &&

call avg_admin_job()
///Procedure in another way to use///

DELIMITER &&
create procedure avg_admin_job1(IN select_record varchar(30))
BEGIN
select avg(balance) from bank_detail where job = 'select_record';
END &&
///PROCEDURE WITH MULTIPLE RECORDS///
DELIMITER &&
create procedure sel_edujob1(in v1 varchar(30) , in v2 varchar(30))
BEGIN 
      select * from bank_detail where education = v1 and job = v2;
END&&
call sel_edujob1('tertiary','services') 
///VIEWS///    ///VIEWS///     ///VIEWS/// ///VIEWS///
///VIEWS/// ///VIEWS/// : A sorter version of data , a subset of data is called view. i.e. virtual table  for simplicity
create view bank_view as select age, job, marital, education from bank_detail;
select avg(marital) from bank_view where job = 'admin.'

////////////////////////////////////////////////////////////////////////
create view bank_housing as select loan, job from bank_detail;
select loan from bank_housing where loan = 'No'
//////REVISION -24 July 2022//////
create database dress
use dress

create table if not exists dress(
`Dress_ID` varchar(30),	
`Style`	varchar(30),	
`Price`	varchar(30),	
`Rating`	varchar(30),	
`Size`	varchar(30),	
`Season`	varchar(30),	
`NeckLine`	varchar(30),	
`SleeveLength` varchar(30),		
`waiseline`	varchar(30),	
`Material`	varchar(30),	
`FabricType`	varchar(30),	
`Decoration`	varchar(30),	
`Pattern Type` varchar(30),		
`Recommendation` varchar(30))	
select * from dress
///To load the whole data fast use load data infile process, keep data in C drive for ease loading///

LOAD DATA INFILE 'C:/AttributeDataSet.csv'
into table dress
FIELDS TERMINATED by ','
ENCLOSED BY'"'
lines terminated by '\n'
IGNORE 1 rows;
select * from dress;

///USE OF PRIMARY and FOREIGN KEYS///
Auto increment- That column will be not null and it should be unique if declared primary key.
create table if not exists test(
test_id int auto_increment,
test_name varchar(20),
test_mailid varchar(20),
test_address varchar(40),
primary key (test_id)) 
select * from test 
///For auto increment, you dont have to mention value during insert///
insert into test values(1,'sudhanshu','sudh@gmail','bangalore'), 
(2,'krish','krish@gmail','bangalore'),
(3,'hitesh','hitesh@gamil','bangalore'),
(4,'subahm','subahm@ineuron','jaipur')
select * from test
///Same data to clarify auto increment because earlier we had given values for test_id///
create table if not exists test2(
test_id int not null auto_increment,
test_name varchar(20),
test_mailid varchar(20),
test_address varchar(40),
primary key (test_id)) 
insert into test2(test_name, test_mailid, test_address) values('sudhanshu','sudh@gmail','bangalore'), 
('krish','krish@gmail','bangalore'),
('hitesh','hitesh@gamil','bangalore'),
('subahm','subahm@ineuron','jaipur')
///Note: To give mapping for auto increment , do mention insert into tb_name(v1,v2...vn) values(.....) to avoid auto increment confusion.///
///Note: always add primary key or any key to auto increment column///
select * from test2 
/// Now, auto increment will put 1,2,3,..... automatically now when given appropriate names to values of tb_names.///
///CONSTRAINT 'CHECK'///
create table if not exists test3(
test_id int ,
test_name varchar(20),
test_mailid varchar(20),
test_address varchar(40),
test_salary int check(test_salary > 10000))
insert into test3 values(1,'sudhanshu','sudh@gmail','bangalore',50000), 
(2,'krish','krish@gmail','bangalore',30000),
(3,'hitesh','hitesh@gamil','bangalore',111000),
(4,'subahm','subahm@ineuron','jaipur',20000)
///To change something in a table that existed/// Also,you want to put constraint to avoid -ve values///
alter table test3 add  check(test_id > 0)
///Insert -ve value to see result///
insert into test3 values(3,'sudhanshu','sudh@gmail','bangalore',50000)

///Check condition if not satisfy in any table values, it will not insert and give you error- check constraint is violated///
create table if not exists test4(
test_id int ,
test_name varchar(20),
test_mailid varchar(20),
test_address varchar(40) check (test_address ='bangalore'),
test_salary int check(test_salary > 10000))
insert into test4 values(1,'sudhanshu','sudh@gmail','bangalore',50000), 
(2,'krish','krish@gmail','bangalore',30000),
(3,'hitesh','hitesh@gamil','bangalore',111000),
(4,'subahm','subahm@ineuron','bangalore',20000)
select *from test4 

///You had used Check Constraint, Increment Constraint and not null Constraint///
create table if not exists test6(
test_id int NOT NULL default 0,
test_name varchar(20),
test_mailid varchar(20),
test_address varchar(40) check (test_address ='bangalore'),
test_salary int check(test_salary > 10000)) 
select * from test6
insert into test6 (test_name, test_mailid, test_address, test_salary) values ('sudan','sudan@gmail','bangalore',50000)
create table if not exists test7(
test_id int NOT NULL default 0,
test_name varchar(20),
test_mailid varchar(20) unique,
test_address varchar(40) check (test_address ='bangalore'),
test_salary int check(test_salary > 10000)) 
select * from test7 

/////////////////TOTAL CONSTRAINTS AVAILABLE HERE//////////////////
1. Default: If you give value ,its good else it will start from 0
2. Not Null: You can't insert not null values.
3. Check: To check condition.
4. Auto Increment: To increment values by itself.
5. Unique: There can't be a duplicate record. 
6. Primary Key Constraint: See below.
7. Foreign Key Constraint:
//////USE OF PRIMARY and UNIQUE KEY//////
Primary key is unique. Only one column can be set primary to set a relation between 2 columns.
Unique key can be defined to many columns in a same table.
//////Create table with all constraints mentioned above//////
create table if not exists test8(
test_id int NOT NULL  auto_increment,
test_name varchar(20) NOT NULL default 'Unknown Person',
test_mailid varchar(20) unique NOT NULL,
test_address varchar(40) check (test_address ='bangalore') NOT NULL,
test_salary int check(test_salary > 10000) NOT NULL,
primary key (test_id)) 
select * from test8 
insert into test8 (test_id, test_name, test_mailid, test_address, test_salary) values(100,'sudhanshu','sudh@gmail','bangalore',50000)
insert into test8 (test_id, test_name, test_mailid, test_address, test_salary) values(2,'krish','krish@gmail','bangalore',30000)
insert into test8 (test_id, test_name, test_mailid, test_address, test_salary) values(101, 'hiten','hiten@gmil','bangalore',181000)
///Remember: Because of some error, the count no will change. Error will also take it as count (Eg:1,2(error) so next will automatically be 3)
