**My SQL**      
Mysql is an opensource/commercial database management system,used to handle databases on backend server.      

*Installation*      
```bash
sudo apt-get update      
sudo apt-get install mysql-server mysql-workbench-community     
```

*mysql uninstall:*    
```bash
sudo apt-get remove --purge mysql-server mysql-client mysql-common -y      
sudo apt-get autoremove -y    
sudo apt-get autoclean     
rm -rf /etc/mysql    
```

*RESET Password Of MYSQL*
```bash
mysql -V
# Stop the server
sudo /etc/init.d/mysql stop
# creating a temporary directory for mysql process
sudo mkdir /var/run/mysqld
# giving current user access to this folder
sudo chown mysql /var/run/mysqld
# bypassing permission to access mysql server
sudo mysqld_safe --skip-grant-tables&
# starting mysql with root permissions,doesn't ask for any password
sudo mysql --user=root mysql
# Inside mysql accessing root account,removing password
mysql>UPDATE mysql.user SET authentication_string=null WHERE User='root';
# removing any extra permissions
mysql>flush privileges;
# adding new password to root user
mysql>ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'your_password_here';
# removing existing privileges
mysql>flush privileges;
# close the mysql shell
mysql>exit
# killing all mysql instances
sudo killall -u mysql
# starting mysql service
sudo /etc/init.d/mysql start
# can now access the mysql shell with above set password
sudo mysql -p -u root
```


**SQL**     
SQL stands for Structured/Standard Query Language.    
* SQL is structured as it uses tables and relations between them.
* But SQL has been implemented by many Database Engines in different ways it can also be Standard Query Language,as all these engines follow a standard guide line to implement.  
* When we want to do any of the **CRUD** operations on a database we use Queries of certain Syntax
* Most SQL Engines support same syntax, with some engines adding extra keywords.   
* SQL is case insensitive and ignores extra whitespace.
* Each query/statement needs to be terminated with a semicolon.
* It is convention to use all sql queries in UPPERCASE. 

```sql
select * from customers;
SeLect *
      FROm 
        customers;
SELECT * FROM customers;
sELeCT * frOM customers;
-- all above commands perform same task,sql ignores case and whitespaces
```

**comments**          
Comments are ignored by sql engine and are only to used for developer convenience.      
* The most common use is to remove sql code,for debugging.            
* Another use is to define why we are coding in this specific manner.         

```sql
-- is used to give comments
```

**Order**       
SQL is CASE Insensitive,but the order of commands matter,if the order is messed up the engine will not run the query.   


1. **USE** Keyword is used to select and use a database.      
```sql
USE databasename;
```

2. **SELECT** Keyword is used to select columns from a table.         
   * we can specify the order,arrangement,calculation of columns to display,take data from.
```sql
SELECT column(s) FROM tablename;
```

3. **AS** Keyword is used to give an *alias* for a column name/table name.              
    ```sql
    SELECT column_name * 2 AS DoubleRate
    -- here we are multiplying a columns value by 2 and renaming the column as Doublerate,
    -- If we don't rename the new column will have the name column_name * 2.
    FROM tablename;
    ```             

4. **DISTINCT** Keyword is used to select only unique results of a query,used after select keyword.     
```sql
SELECT DISTINCT column_name 
from table_name;
```

5. **WHERE** Keyword is used to select columns only when given condition is met.                
   * *Comparision operators* To perform a where condition we can use these opeartors.   
    * *<*: less than
    * *>*: greater than
    * *=*: equal than
    * *!=* / <>: not equal to
    * <=: less than or equal to
    * \>=: greater than or equal to
    * **BETWEEN**: the values are between two end points,range is inclusive
    * **IN**: the value is in a certain group of values.Often used as shorthand for multiple OR statements.
```sql
SELECT * 
FROM table_name
WHERE condition;
WHERE columnname=1;
WHERE columnname<1;
WHERE columnname>1;
WHERE columnname<=1;
WHERE columnname>=1;
WHERE columnname!=1;
WHERE columnname<>1;
WHERE columnname BETWEEN 1 AND 10;
WHERE columnname IN (2,3,4,9,17);
```

6. **LIKE** Keyword is used to select data that matches the given pattern.      
    * *%* symbol denotes one or more characters
    * *_* symbol denotes a single character

```sql
SELECT * 
FROM table_name
WHERE columnname LIKE 'pattern';
-- searches for text in column that starts with a and has any number of characters
WHERE columnname LIKE 'a%';
-- searches for text that has 6 characters and ends with y
WHERE columnname LIKE '_____y';
```

7. **REGEXP** Keyword is Better alternate to LIKE Keyword,this accepts all the regular expersion patterns for data searching.   
    * Major advantage over LIKE  Keyword is that we can perform complex pattern matching.
    * *^* symbol specifies that the pattern is at the beginning of the text.
    * *$* symbol specifies that the pattern is at the end of the text.
    * *character* any given character is matched if the text contains that text.
    * *\** matches one or more characters
    * *.* matches one character
    * *[abcd]* text in square brackets is matched 
    * *[a-d]* text with at least one of the ranged item is matched
    * *r[a-d]* text with ra,rb,rc,rd is matched
    * *|* or symbol is used to provide alternates to patterns.  
```sql
SELECT * 
FROM table_name
WHERE columnname REGEXP 'pattern';
WHERE columnname REGEXP '*';
WHERE columnname REGEXP '^a';
WHERE columnname REGEXP 'a$';
WHERE columnname REGEXP '[a-d]';
WHERE columnname REGEXP 'a[s-u]';
WHERE columnname REGEXP 'aur|sat|mon';
WHERE columnname REGEXP 'he...';
WHERE columnname REGEXP 'hello';
```

8. **AND** Keyword is used to select columns that satisfy both the conditions.       
    * And is used in conjunction with Where keyword             
    * The result is true when both conditions are true.             

```sql
SELECT *
FROM table_name
WHERE condition AND condition;
-- returns columns that satisfy both the conditions.
```

9. **OR** Keyword is used to select columns that satisfy at-least one condition.   
    * OR is used in conjunction with where keyword
    * The result is true when at-least on of the condition is true.
```sql
SELECT *
FROM table_name
WHERE condition OR condition;
```

1.  **NOT** Keyword is used to select columns that don't satisfy the given condition.        
    * the result is false when the given input is true.             
```sql
SELECT *
FROM table_name
WHERE NOT condition;
```             
We can Combine AND,OR,NOT values to perform multiple conditional operations.        


11. **ORDER BY** Keyword is used to sort the output of query,by a given column.       
    * By default results are sorted by primary key columns(PRIMARY KEY),i.e ascending order.
    * We can sort the order of the column to descending order,using **DESC** keyword.
    * We can sort the data by multiple columns,so resulted is sorted by first column,then second column and so on.  
    * sorting can be done by ascending and descending order of multiple columns.
```sql
SELECT *
FROM table_name
ORDER BY column_name
ORDER BY column_name DESC
ORDER BY column1 ASC, column2 DESC
```

12. **INSERT INTO** keyword is used to insert new data into a table.        
    * we can insert data directly or by specifing the column name then the value for that column
    * the order of values inserting should be same as the table column order
    * **VALUES** Keyword is used in combination with INSERT INTO to provide the values for each column of table.
    * Value should be given to columns that don't accept a null value or doesn't have a default value.

```sql
INSERT INTO table_name
VALUES (value1,value2,value3);

INSERT INTO table_name (column1,column2,column3)
VALUES (value1,value2,value3);
```             

13.  **NULL** Keyword is used to with WHERE keyword to specify that the column data is NULL or NOT NULL.
    * **IS NULL** Keyword is used to take data from table whose values are NULL
    * **IS NOT NULL** Keyword is used to take data from table whose values are not null             

```sql
SELECT *
FROM table_name
WHERE column_name IS NULL;
WHERE column_name IS NOT NULL;
```

14. **LIMIT** Keyword is used to limit the output of our query.
    * This useful when our database may contain millions of records and we only 10 rows or few records.
    * Mysql supports **LIMIT** Keyword while oracle sql uses **ROWNUM** Keyword for same purpose.   
```sql
SELECT *
FROM table_name
WHERE column_name IS NULL
LIMIT 20;
```

15.  **UPDATE** Keyword is used to update existing record data of a table.
    * we have to be careful when updating data in a table
    * if a row is not specified this query will update the entire column with given value.
    * **SET** Keyword is used to update/set the row with new data

```sql
UPDATE table_name
SET column_name='value', column_name2='value'
WHERE column_name='value';

-- if the where clause is not given the entire column will be set to alfred
UPDATE Customers
SET ContactName='Alfred Schmidt', City='Frankfurt'
-- the above data will only be set to row whose customerid is 1
WHERE CustomerID=1;
```

16. **DELETE** Keyword is used to delete an entire row of a table.
    * have to be careful deleting the data in table
    * If we omit the where clause,this query will delete all rows in the table.

```sql
DELETE 
FROM table_name
WHERE column_name='value';

DELETE FROM table_name;
-- deletes all rows in the table

DELETE 
FROM Customers
-- will delete the row containing customer name alfreds
WHERE CustomerName='Alfreds Futterkiste';
```

17. **MIN/MAX()** functions are used to return the minium and maximum value of a column.           
    * This is a function and takes the column name as the input
    * Often MIN/MAX functions are used with an alias with **AS**,or the result will have a column name of MIN(column)

```sql
SELECT MIN(column_name)
FROM table_name;

SELECT MIN(price) AS minimum_price
FROM Products;
-- If we don't use an alias the result will have the column name MIN(price)

SELECT MAX(price) AS maximum_price
FROM Products;
```

18. **COUNT()** function is used to count the number of rows/records in a given column,that are not null.
    * takes a column name as the input.

```sql
SELECT COUNT(column_name)
FROM table_name

SELECT COUNT(customer_id)
FROM customers;
-- returns number of NON NULL records in the customer_id column
```

19.  **AVG()** function is used to return the average value of the numeric column.
    * takes a column name as the input.
```sql
SELECT AVG(column_name)
FROM table_name

SELECT AVG(price)
FROM products;
-- returns AVERAGE of price
```

20.  **SUM()** Function is used to return the sum of numeric column values.      
    * takes a column name as the input.
    
```sql
SELECT SUM(column_name)
FROM table_name

SELECT SUM(salary)
FROM employees;
-- returns total salary of employees.
```

21. **AS** Keyword is used to provide an alias(temporary) for the table column name.
    * this is used to display a meaningful name to user instead of the functions/arithmetic operations done to achieve that column.
    * Used to make our query cleaner by renaming the table name to a small value.   

```sql
SELECT price * 0.9 AS "Discounted Price"
FROM products;
-- If no alias is given then the column will have the name, price * 0.9
```

22. **JOIN** Keyword is used to join multiple tables using existing relations.  
    * tables are joined using the **ON** Keyword,to check the unique values(primary key) that are present in both tables.
    * There are two types of joins in SQL, **INNER**(Default),**OUTER**.
    * The joining can be of two tables in same database, two tables in different databases,in different servers.
    * It is quite common to see multiple join statements in a single query.
    * **INNER JOIN** Keyword is same as  **JOIN** Keyword,this returns the records that are common in both tables
    * **OUTER JOIN** is of two types **LEFT OUTER JOIN**,**RIGHT OUTER JOIN**, the outer keyword can be skipped,it is optional.
    * **LEFT JOIN** returns all values from left table and the matched records in right table
    * **RIGHT JOIN** returns all values in right table and matched records in left table.
    * **USING** was introduced in latest mysql version to check the condition like **ON** does
    * Here the column name must be same for two tables that being joined,

```sql
SELECT *
FROM table_1
JOIN table_2
ON condition;

SELECT *
FROM orders
JOIN customers
ON orders.customer_Id = customers.customer_Id;
-- will return records that have same customer id.
USING(customer_id);
-- this works the same way as the above ON command but this is shorter,
-- only works if column name is same across tables.


SELECT *
FROM orders
LEFT JOIN customers
ON orders.customer_id = customers.customer_id;
-- returns all the records of orders and matched values from customers table

SELECT *
FROM orders
RIGHT JOIN customers
ON orders.customer_id = customers.customer_id;
-- returns all the records of customers and matched values from orders table
```

23.  **SELF JOIN** Keyword is used to join the table with itself.
    * While using self join we have to give alias to table name,otherwise an ambiguous error is raised.

```sql
SELECT *
FROM customers A
JOIN customers B
WHERE A.city != B.city;
-- will return records that are not equal.
```

24. **UNION** Operattor is used to merge output of two queries in to single query.
    * For a proper UNION of tables, the number of columns on tables should be same and of same data type and same order of columns.
    * If number of columns don't match then the row data is set to null.
    * **UNION ALL** Operator returns all records of both select queries,while **UNION** Keyword returns only the unique/distinct records.

```sql
SELECT City FROM Customers
UNION
SELECT City FROM Suppliers
ORDER BY City;
-- will return only unique values of customers and suppliers

SELECT City FROM Customers
UNION ALL
SELECT City FROM Suppliers
ORDER BY City;
-- will return all the city names from both results

SELECT City, Country FROM Customers
WHERE Country='Germany'
UNION
SELECT City, Country FROM Suppliers
WHERE Country='Germany'
ORDER BY City;
-- can also use conditions with where keyword
```

25. **GROUP BY** Statement is used to group the results of a column in to single result.
    * multiple contry names are grouped to denote the first row of one country value
    * Used with other functions to count the number of results of each column

```sql
SELECT COUNT(orders),Customer_name
FROM Customers
GROUP BY Customer_name;
-- Here the output shows each individual customer name with their number of orders.
-- shows one entry for group of same customer name
```

26. **HAVING** Keyword is introduced in latest version of MYSQL to extend WHERE Keyword functionality.
    * query returns the records that have the given condition.
    * Having clause can use existing functions  to create conditions 

```sql
SELECT *
FROM Customers
GROUP BY Country
HAVING COUNT(Customer_name) >5;
-- will return records of countries that have more than 5 customers,
-- can't have this condition in where keyword.
```

27. **EXISTS** Operator is used to return the existence of some records of a query.
    * Returns true if one or more records are present for the given query.
    * The condition checked for existence is another select query.

```sql
SELECT SupplierName
FROM Suppliers
WHERE EXISTS 
    (SELECT ProductName 
    FROM Products 
    WHERE Products.SupplierID = Suppliers.supplierID AND Price < 20);

-- returns the suppliers names that satisfy the Exists condition.
-- The condition is another select query,that checks if the price is less than 20.
```

28. **ANY/ALL** Operator is used to check if the subqueries result is present in where condition.
    * A select statement is used to get records for comparisions.
    * **ANY** Operator is used to check if any of the subqueries result match the condition.
    * **ALL** Operator is used to check if all of the subqueries result matches the condition
    * Ex: when using any operator,the conditions value should be one of the values of result
    * Ex: when using all operator,the conditions value should be all the value of result.

```sql
SELECT *
FROM customers
WHERE customer_city = ANY (
    SELECT shipper_city 
    FROM Shippers
    WHERE deliver_days < 2;
    -- returns the city names having shippers that can deliver in 2 days.
)
-- will print the customers details that live in one of the cities that a shipper can deliver.
-- Ex: hyd = ANY(hyd,delhi,mumbai), true,used most often.

SELECT *
FROM customers
WHERE customer_city = ALL (
    SELECT shipper_city 
    FROM Shippers
    WHERE deliver_days < 2;
    -- returns the city names having shippers that can deliver in 2 days.
)
-- will print the customers details that live in all cities that shipper can deliver
-- Ex: hyd = ALL(hyd,delhi,mumbai). this is false,since one customer can't live in multiple places.
```

29. **ALTER TABLE** Keyword is used to modify/add/delete table data.
    * **ALTER COLUMN** is used to modify the column type/add/delete data.

```sql
ALTER TABLE table_name
ALTER COLUMN product_name int;
-- changes the data type of column to int

ALTER TABLE table_name
DROP COLUMN product_name;
-- deletes the entire product_name column
```

30. **DROP** Keyword is used to delete an entire column,table,database.
    * **DROP TABLE** deletes the entire table
    * **DROP DATABASE** deletes the entire database
    * **DROP COLUMN** deletes the entire column
    * **DROP VIEW** deletes a view from memory

```sql
ALTER TABLE table_name
DROP COLUMN column_name;
-- deletes given column

DROP TABLE table_Name;
-- deletes specified table

DROP DATABASE database_name;
-- deletes specified database

DROP VIEW views_name;
-- deletes specified view.

ALTER TABLE table_name
DROP CONSTRAINT PRIMARY KEY;
-- deletes the tables primary key
```


30. **VIEW** Keyword is used to create a temporary/virtual table from multiple queries.
    * **CREATE VIEW** is used to create a view from other tables.
    * **CREATE OR REPLACE VIEW** is used to update the data in a view.

```sql
CREATE OR REPLACE VIEW view_name AS
SELECT column1,column2,column3
FROM table_name;
-- this query adds the columns to view if they are missing.
```


31. **CREATE** Keyword is used to create database and tables,with specified datatypes.
    * **CREATE DATABASE** creates an empty database
    * **CREATE TABLE** creates a table with given column names and datatypes.
    * **CREATE VIEW** creates a view from other tables

```sql
CREATE DATABASE database_Name;
-- creates a database with given name,needs admin privileges to do this.

CREATE TABLE table_name(
    column_name datatype(length_of_values)
);

CREATE TABLE persons(
    person_id int,
    first_name varchar(255),
    -- accepts string data till 255 characters
    city varchar(255)
);
```

32. **PRIMARY KEY** keyword is used to create a primary key column in a table.
    * By default we use a ID column for primary key
    * It is best practice to have only one primary key column per table.
    * **AUTO INCREMENT** is used to increment the columns value by one(default) automatically

```sql
CREATE TABLE persons(
    ID int NOT NULL,
    first_name varchar(255) NOT NULL,
    Age int,
    PRIMARY KEY(ID)
    -- making the ID column a primary key value
);

ALTER TABLE persons
DROP PRIMARY KEY;
-- will delete the primary key constraint.
```


Creating a Registration Page using Java,Mysql,tomcat,ubuntu,eclipse


## Installation:

### Java installation:
Download the latest java jdk version at the time of writing this document it is openjdk 14
1. `sudo apt-get install openjdk-14-jdk openjdk-14-jre`
2. test the installation with `javac -version`

### Tomcat installation:
Installing tomcat in windows/ubuntu
1. Download the zip file and extract it to ~/.tomcat
2. Thats it nothing more to do

### MySQL installation
install mysql in ubuntu by downloading the apt package
1. download the mysql deb `https://dev.mysql.com/downloads/repo/apt/`
2. install the deb package `sudo dpkg -i mysql-apt-config_w.x.y-z_all.deb`
3. update and install mysql server `sudo apt-get update && sudo apt-get install mysql-server && sudo apt-get install mysql-workbench-community`
4. verify the installation with `mysql --version`
5. run `mysql_secure_installation` then select appropriate options to install with good password that you will remember
6. This password is for root user of mysql,this is different from root user of ubuntu installation
7. As a best practice it is preferred to create a new user and database for this user,grant permission to this database.
8. `CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'password';` creates a new user
9. `GRANT all privileges ON database_name.* TO 'username'@'localhost';` grants all permissions to the user on specified database
10. to access an account of mysql use `mysql -u accountname -p`,to access root user of mysql `mysql -u root -p`,password(0000)
11. restart the mysql service with `sudo systemctl status mysql && sudo systemctl restart mysql && sudo systemctl status mysql`
12. then login to mysql account and work on some tables, do the same with mysql workbench software to verify the mysql connection


### Eclipse installation
Eclipse is an open source software editor for various languages(C,C++,Java(SE),Java(EE),Python,PHP).
1. Go to eclipse website and download the latest installer software,don't download the zip it will be standalone and needs a lot of setup manually to be configured.
2. After downloading the installer extract and run it in terminal `./eclipse-inst`
3. Install eclipse on home directory for easy access and privileges for users.
4. Take a shortcut on home screen and start menu 

#### Configuring Eclipse
1. To develop normal/core java projects use eclipse java ide.
2. to develop servlets/jsp/websites with java use eclipse java ee edition.
3. After installation change download the themes from eclipse market place,color themes,start autosave
4. in eclipse a project is used for even a single file,so it is a best practice to create a project then a main class file that is start of project then all other classes refer to this file.

#### Tomcat in eclipse
To make use of tomcat in eclipse java ee we click on servers option then select the same version of tomcat as the previous installed tomcat then locate the folder containing extracted tomcat code(~/.tomcat)
1. run the current jsp/servlet page in run as server and change the default browser to chrome browser for better debugging.


### creating a signup login page 
Using java,servlets,jsp,html,css,sql,tomcat,eclipse

Create a dynamic web project and create three jsp files 
login.jsp,register.jsp,welcome.jsp
1. create a basic html login,register,welcome pages then paste the code in jsp files
2. create appropriate java files to get data from jsp and database
3. install mysql connector java to tomcat library and in java build path of eclipse for easy access to mysql service
4. create a servlet that contains the account id,password,jdbc connection to mysql port and database name
5. Test this connection then complete the front end and backend with no errors.
6. create a table in mysql directly,use this table with matching column names in servlet code
7. `create table customer (customer char(20),password char(10),name char(20))`
8. Run the login jsp with tomcat then create a new user and save data,while loging in check the values with existing one
9. If same show the welcome page with custom page/custom feed.
