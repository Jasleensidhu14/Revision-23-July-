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
