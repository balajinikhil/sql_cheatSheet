DB - Organized collection of data stored in an electronic data
DBMS - system software for creating and managing db

File Server Architecture
	Server/Local file system

Client Server Architecture
	
Introdution to SQL
	Structered Query Language - helps communicate with DB
	
	1.Data Quwery Language -- select

	2.Data definition language -- createTable, AlterTable,DropTable

	3.Data Manipulation language -- Insert,Update,Delete

	4.Data Control language -- Grant,Revoke

Install
1.download developer edition
2.run.exe
3.select custom
4.choose location
5.click installation select standalone installation
6.performance installation - free edition -next- db engine services
7.Name the instance
8.mixed mode - enter password 
7.install

sql server management tool
1.install

Table
 A table is db object which has rows and columns
rows - records
columns - fields

fields- specific information about data in table
records - each induvidual entry of a table 

Creating A database: syntax

	create database test --new db
	use DatabaseName -- change db
	drop database DatabaseName --delete db

Datatypes in sql
	Particular type of data a column can hold

Different datatypes in sql

Number
1.bigint -- big range integers -9*10^18
2.init  -- medium range integers 2*10^9
3.smallint -- 32,768
4.tinyint -- 0 <==> 255
5.decimal(s,d) -- decimal values 
2 args size,digits after decimal point
12.50 - s=4, d=2

Character 
1.char(s) -1arg size of value fixed length data types  255
2.varchar(s) -  255
3.text - 65,535

Date and Time
date - yyyy-mm-dd
time - hh:mm:ss
year - yyyy

Constrains
1.not null -- field always contains value
2.default -- field contains default value
3.unique -- fields are unique
4.primary key -- notNull + unique

AUTO_INCREMENT //increases the field value by 1;

Create Table
1.Name the table
2.Define the columns
3.Assign data types of columns

Syntax of Create Table Statement	
	create table tableName(
	column1 type,
	
	primary key(columnName)
	);
	
	ex:
	create table testing(
	e_id int IDENTITY(1,1) not null,
	e_name varchar(20),
	e_role varchar(20),
	primary key (e_id));

Insert Query	
	insert into tableName values(column1Value,column2Value);

	INSERT INTO table_name (column1, column2, column3, ...)
	VALUES (value1, value2, value3, ...);
	
	ex-
	insert into testing values(
		2,'test1','tester'
		);
	INSERT INTO Customers (CustomerName, City, Country)
	VALUES ('Cardinal', 'Stavanger', 'Norway');

Select Syntax
	select column1,column2,....,columnN from table 
	ex-	select e_name from employees;
	select * from tableName //all data from table
	ex - select * from employees;

Select Distinct
	select distinct column1 from tableName //only values which are different
	ex - select distinct * from employee	

Where clause
	select * from tableName where columnName = 'value';
	ex - select * from employees where e_name = 'test1';	

	select * from tableName where columnVAl < value
	ex -select * from employees where e_age>25;
	
AND OR NOT operator
	select * from tableName where column1 = 'value1' AND column2 > value2
	ex-select * from employees where e_age >25 AND e_age<40;

	select * from tableName where column1 = 'value1 OR column2 > value2	
	ex- select * from employees where e_role = 'developer' OR e_role='HR';

	select * from tableName where not column1 ='value1'
	ex- select * from employees where not e_role = 'manager'
	
Like and Between
	like - operator is used to extract records where particular pattern is present

% - percent represents zero,one or multiple character
_ - underscore represents single character

select * from tableName where column LIKE 'val%';
ex-select * from employees where e_name LIKE 'tes%';

select * from testing where e_name LIKE 'val_'
ex-select * from employees where e_name LIKE 'test_'

Between operator
	select values within range
	select * from tableName column BETWEEN value1 AND value2
	ex- select * from employees where e_age between 25 AND 50;

Functions
MIN()
MAX()
COUNT()
SUM()
AVG()

	MIN() -smallest value of column - 
	select min(column1) from tableName;
	ex - select min(e_age) from employees;	

	MAX() - largest value in column
	select max(column1) from tableName'
	ex-select max(e_age) from employees;	

	COUNT() - number of rows that match specified critera
	select count(*) from tableName where column1='value';
	ex- select count(*) from employees where e_age<50;
	//total no. of data matching critera

	SUM() - total sum of numeric column
	select sum(column) from tableName;
	select sum(e_age) from employees;
	
	AVG() - average value of numeric value
	select avg(column) from tableName;
	select avg(e_age) from employees ;
		

String Functions

LTRIM() - remove blank spaces on left side -- '      value'
	select ltrim('     value');
	ex - select ltrim(e_name) from employees;

LOWER() - convert all character to lowercase
	select lower('VALUE')
	ex - select lower(e_role) from employees;

UPPER() -all characters to uppercase 
	select upper('value');
	ex- select upper(e_name) from employees;

REVERSE() - all characters to reverse order
	select revers('value')
	ex -select reverse(e_gender) from employees;	

SUBSTRING() - extract certain part
	select substring('value', indexOfString, indexValueOfStart, lengthOfSubString)
	ex-select SUBSTRING(e_name,2,4) from employees;

ORDER BY 
	sort data in ascending or desceding order - default ascending
	select * from tableName order by column --ascending order
	ex - select * from employees order by e_age; 
	select * from tableName order by column DESC -- descending order
	ex - select * from employees order by e_age desc

TOP clause
	used to fetch the top N records
	select TOP 3 * from tableName
	select TOP 3 * from tableName order by column DESC
GROUP BY 
	is used to get aggregate result with respect to a group
	select avg(column1), column2 from tableName GROUP BY colmn2;
	select avg(e_age),e_gender from employees group by e_gender;
	
	ex-
	select avg(e_age)as avg_age,e_role from employees group by e_role;
	select avg(e_salary) as avg_salary ,e_gender from employee group by e_gender order by avg_salary DESC;

Having Clause
	having clause is used in combination with group by to impose conditions on groups
	select column1, avg(column2) as new_name_column from tableNamw group by columnName having avg(column2) > value;	
	select e_gender, avg(e_salary) as average_salary from employee group by e_gender having avg(e_salary) > 10000;

UPDATE
	update is mostly used to modifiy the existing records in a table
	update tableName set col1=val1, col2=val2,....coln=valn where col = val ;	
	ex-
	update employee set e_age = 28 where e_id=5


DELETE 
	used to delete to existing data from table
	delete from tableName where column = value;
	ex-
	delete from employee where e_id=7;
	
TRUNCATE 
	delete all data in table, structure of table remains same
	truncate table tableName;
	ex-
	truncate table employee;

INNER JOIN 
	inner join returns records that have matching values in both the tables. It is also known as simple join.
	select tableName.columnName, tableName.columnName2, select tableName2.columnName1, tableName2.columnName2 from tableName INNER JOIN tableName2 ON (condition) tableName.col1 = tableName2.col1

LEFT JOIN 
	returns all the records from left table and matched records from right table
	select table1.col1, table1.col2..., table1.coln, table2.col1.....table2.coln from table1 LEFT JOIN table2 ON table1.col1 = table.col1

RIGHT JOIN 
	all records from right table and matched records from left table
	select table1.coln, table2.coln from table1 RIGHT JOIN table2
 	ON table1.col1 = table2.col1;

FULL JOIN
	returns all records from left and right table;
	select table1.coln table2.coln from table1 FULL JOIN table2
	ON table1.col1 = table2.col2;

UPDATE USING JOIN
	update table1. 
	set col1 = col+1
	from table1
	join table2 on table1.col2 = table2.col2;
	where table2.col1 = 'value';
	
DELETE USING JOIN
	delete table1
	from table1
	join table2 on table1.col1 = table2.col2;
	where table2.col1 = 'value';

UNION OPERATOR
	union operator is used to combine the result-set of two or more 	SELECT statement
	
	select * from table1 
	union 
	select * from table2

UNION ALL OPERATORS
	all the rows from both tables including duplicate values
	
	select * from table1 
	union all
	select * from table2

	select * from employee 
	union
	select * from ex_employee;

EXCEPT OPERATOR
	combines two select statements and returns unique records from left query which are not part of the right query
	
	select * from table1 
	except 
	select * from table2

	select * from employee 
	except
	select * from ex_employee;

INTERSECT OPERATOR
	returns values which are common to both tables
	
	select * from table1
	intersect
	select * from table2
	
	select * from employee 
	intersect	
	select * from ex_employee;

VIEWS 
	views is a virutal table based on sql query// used for restricted table view
	create view viewName as 
	select * from table 
	where col = val
	
	create view employee_view as 
	select * from employee where e_gender = 'female'

DROP VIEW SYNTAX
	drop view viewName	
	
	drop view employee_view;

ALTER TABLE
	add column to exisiting table

	alter table tableName 
	ADD colName dataType;

DROP COLUMN
	remove column form existing table
	
	alter table tableName;
	DROP COLUMN colName;

	alter table employee
	drop column e_salary;

MERGE 
	insert update and delete in one statement
	requires 2 tables source table and target table 
	source table contains changes we need to apply to target table
	joins source and target table
	
	merge targetTable as T 
	using sourceTable as S
	ON [condition] T.col1 = S.col1; 
	when matched 
		then update set T.col1 = S.col1
	when not matched by target
		then insert (col1,...,coln)
		values (val1,...,valn)
	when not matched by source
		then delete;

TYPES OF FUNCTIONS 
1.SCALAR VALUED FUNCTION
2.TABLE VALUED FUNCTION

SCALAR VALUED FUNCTION
	returns a scalar value
	
	create a function function_name(@num as int)
	RETURNS int
	AS
	BEGIN
	
	
	RETURN(@num +5)
	end

	select dbo.function_name(val)

TABLE VALUED FUNCTION
	return a table
	
	create function function_name(@parma as varchar(20))
	returns table
	as 
	return (select * from tableName where col1 = @param)
	
	select * from dbo.function_name('value1')
	
	ex-
	create function selectgender(@gender as varchar(20))
	returns table
	as 
	return(select * from employee  where e_gender = @gender);

	select * from dbo.selectgender('female');

TEMPORARY TABLE
	created in tempDB and deleted as soon as the session is terminated

	create table #table_name( col_name datatype, col2_name datatype	);
	
CASE STATEMENT
	case statement helps in multi way decision making
	
	SELECT	
	CASE 
	WHEN condition1 THEN result1
	WHEN condition2 THEN result2
	ELSE result
	END
	
	select *, grade = case
	when e_salary < 100 then 'c'
	else 'D'
	end
	from employee[tableName]
	
	select *, grade = 
	case
	when e_age<15000 then 'C'
	when e_age >24 then 'A'
	else 'A'
	end
	from employee;
	go

IIF function is an alternative for case statement
	select
	iif(10>20, 'returns value inside this quote if true','returns value inside this quote if true')

	select e_id,e_name,e_age
	iif(e_age>30, 'old employee', 'young employee') as 	employee_generation from employee

STORED PROCEDURE IN SQL	
	stored procedure is a prepared sql code which can be saved and reused
	
	create procedure nameOfProcuder
	as
	select e_age from employee
	go

	exec nameOfProcedure


STORED PROCEDURE WITH PARAMETER SYNTAX
	
	create procedure name @param datatype
	as
	select * from tableName where col1=@param
	go
	
	exec name @param='val'

EXCEPTION HANDLING
