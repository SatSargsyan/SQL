# SQL

Fill in the missing keyword to list the table names.
Show Tables



###The WHERE Statement

The WHERE clause is used to extract only those records that fulfill a specified criterion.

The syntax for the WHERE clause:
```C#
SELECT column_list 
FROM table_name
WHERE condition;
```
Consider the following table:
nkar sql1


In the above table, to SELECT a specific record:
```C#
SELECT * FROM customers
WHERE ID = 7;
```
nkar sql2

###SQL Operators

Comparison Operators and Logical Operators are used in the WHERE clause to filter the data to be selected.

The following comparison operators can be used in the WHERE clause:

nkar sql3

For example, we can display all customers names listed in our table, with the exception of the one with ID 5.
```C#
SELECT * FROM customers
WHERE ID != 5;
```
nkar sql4

As you can see, the record with ID=5 is excluded from the list.


###The BETWEEN Operator

The BETWEEN operator selects values within a range. The first value must be lower bound and the second value, the upper bound.

The syntax for the BETWEEN clause is as follows:
```C#
SELECT column_name(s)
FROM table_name
WHERE column_name BETWEEN value1 AND value2;
```
The following SQL statement selects all records with IDs that fall between 3 and 7:
```C#
SELECT * FROM customers 
WHERE ID BETWEEN 3 AND 7;
```
nkar sql5

###Text Values

####When working with text columns, surround any text that appears in the statement with single quotation marks (').

####The following SQL statement selects all records in which the City is equal to 'New York'.
```C#
SELECT ID, FirstName, LastName, City 
FROM customers
WHERE City = 'New York';
```
nkar sql6

###Logical Operators

####Logical operators can be used to combine two Boolean values and return a result of true, false, or null.
The following operators can be used:

nkar sql7

When retrieving data using a SELECT statement, use logical operators in the WHERE clause to combine multiple conditions.

If you want to select rows that satisfy all of the given conditions, use the logical operator, AND.

nkar sql8

To find the names of the customers between 30 to 40 years of age, set up the query as seen here:
```C#
SELECT ID, FirstName, LastName, Age
FROM customers
WHERE Age >= 30 AND Age <= 40;
```
This results in the following output:

nkar sql9

You can combine as many conditions as needed to return the desired results.
###OR

If you want to select rows that satisfy at least one of the given conditions, you can use the logical OR operator.

The following table describes how the logical OR operator functions:
nkar 10


For example, if you want to find the customers who live either in New York or Chicago, the query would like this:
```C#
SELECT * FROM customers 
WHERE City = 'New York' OR City = 'Chicago';
```
Result:
nkar 11

###Combining AND & OR

The SQL AND and OR conditions may be combined to test multiple conditions in a query. 
These two operators are called conjunctive operators.

When combining these conditions, it is important to use parentheses, so that the order to evaluate each condition is known.

Consider the following table:

nkar 12

The statement below selects all customers from the city "New York" AND with the age equal to "30" OR “35":
```C#
SELECT * FROM customers
WHERE City = 'New York'
AND (Age=30 OR Age=35);
```
Result:
nkar13


You can nest as many conditions as you need.

Fill in the blanks to select customers whose ids are either 1 or 2, and whose city is ''Boston''.
```C#
SELECT * FROM customers
WHERE (id = 1 OR  id = 2)
AND city = 'Boston'
```
###The IN Operator

The IN operator is used when you want to compare a column with more than one value. 

For example, you might need to select all customers from New York, Los Angeles, and Chicago.
With the OR condition, your SQL would look like this:
```C#
SELECT * FROM customers 
WHERE City = 'New York'
OR City = 'Los Angeles'
OR City = 'Chicago';
```
Result:
nkar 15

###The IN Operator

You can achieve the same result with a single IN condition, instead of the multiple OR conditions:
```C#
SELECT * FROM customers 
WHERE City IN ('New York', 'Los Angeles', 'Chicago');
```
This would also produce the same result:
nkar 16
Note the use of parentheses in the syntax.


###The NOT IN Operator

The NOT IN operator allows you to exclude a list of specific values from the result set. 

If we add the NOT keyword before IN in our previous query, customers living in those cities will be excluded:
```C#
SELECT * FROM customers 
WHERE City NOT IN ('New York', 'Los Angeles', 'Chicago');
```
Result:
nkar 17

###The CONCAT Function

The CONCAT function is used to concatenate two or more text values and returns the concatenating string.

Let's concatenate the FirstName with the City, separating them with a comma:
```C#
SELECT CONCAT(FirstName, ', ' , City) FROM customers;
```

The output result is:
nkar 18

###The AS Keyword

A concatenation results in a new column. The default column name will be the CONCAT function.
You can assign a custom name to the resulting column using the AS keyword:
```C#
SELECT CONCAT(FirstName,', ', City) AS new_column 
FROM customers;
```
And when you run the query, the column name appears to be changed.
nkar 19


###Arithmetic Operators

Arithmetic operators perform arithmetical operations on numeric operands. The Arithmetic operators include addition (+), subtraction (-), multiplication (*) and division (/). 

The following employees table shows employee names and salaries:
nkar 20
The example below adds 500 to each employee's salary and selects the result:
```C#
SELECT ID, FirstName, LastName, Salary+500 AS Salary
FROM employees;
```
Result:
nkar 21

###The UPPER Function

The UPPER function converts all letters in the specified string to uppercase. 
The LOWER function converts the string to lowercase.

The following SQL query selects all LastNames as uppercase:
```C#
SELECT FirstName, UPPER(LastName) AS LastName 
FROM employees;
```
Result:
nkar 22

If there are characters in the string that are not letters, this function will have no effect on them.

###SQRT and AVG

The SQRT function returns the square root of given value in the argument.

Let's calculate the square root of each Salary:
```C#
SELECT Salary, SQRT(Salary) 
FROM employees;
```
Result:
nkar 23

Similarly, the AVG function returns the average value of a numeric column:
```C#
SELECT AVG(Salary) FROM employees;
```
Result:
nkar 24

The SUM function

The SUM function is used to calculate the sum for a column's values

For example, to get the sum of all of the salaries in the employees table, our SQL query would look like this:
```C#
SELECT SUM(Salary) FROM employees;
```
Result:
nkar 25

The sum of all of the employees' salaries is 31000.

###Subqueries
A subquery is a query within another query. 

Let's consider an example. We might need the list of all employees whose salaries are greater than the average.
First, calculate the average:
```C#
SELECT AVG(Salary) FROM employees;
```
As we already know the average, we can use a simple WHERE to list the salaries that are greater than that number.
```C#
SELECT FirstName, Salary FROM employees 
WHERE  Salary > 3100
ORDER BY Salary DESC;
```
The DESC keyword sorts results in descending order. 
Similarly, ASC sorts the results in ascending order.

Result:
nkar 26


A single subquery will return the same result more easily.
```C#
SELECT FirstName, Salary FROM employees 
WHERE  Salary > (SELECT AVG(Salary) FROM employees) 
ORDER BY Salary DESC;
```
The same result will be produced.
nkar 26 the same

Enclose the subquery in parentheses. 
Also, note that there is no semicolon at the end of the subquery, as it is part of our single query.

###The Like Operator

The LIKE keyword is useful when specifying a search condition within your WHERE clause.
```C#
SELECT column_name(s)
FROM table_name
WHERE column_name LIKE pattern;
```
SQL pattern matching enables you to use "_" to match any single character and "%" to match an arbitrary number of characters (including zero characters).

For example, to select employees whose FirstNames begin with the letter A, you would use the following query:
```C#
SELECT * FROM employees 
WHERE FirstName LIKE 'A%';
```
Result:
nkar 27

As another example, the following SQL query selects all employees with a LastName ending with the letter "s":
```C#
SELECT * FROM employees 
WHERE LastName LIKE '%s';
```
Result:
nkar 28
The % wildcard can be used multiple times within the same pattern.


###The MIN Function

The MIN function is used to return the minimum value of an expression in a SELECT statement.

For example, you might wish to know the minimum salary among the employees.
SELECT MIN(Salary) AS Salary FROM employees;


All of the SQL functions can be combined together to create a single expression.

###Types of Join

The following are the types of JOIN that can be used in MySQL:
- INNER JOIN
- LEFT JOIN
- RIGHT JOIN

INNER JOIN is equivalent to JOIN. It returns rows when there is a match between the tables.

Syntax:
SELECT column_name(s)
FROM table1 INNER JOIN table2 
ON table1.column_name=table2.column_name;

Note the ON keyword for specifying the inner join condition.

The image below demonstrates how INNER JOIN works:

nkar 29

Only the records matching the join condition are returned.

LEFT JOIN

The LEFT JOIN returns all rows from the left table, even if there are no matches in the right table. 

This means that if there are no matches for the ON clause in the table on the right, the join will still return the rows from the first table in the result.

The basic syntax of LEFT JOIN is as follows:
SELECT table1.column1, table2.column2...
FROM table1 LEFT OUTER JOIN table2
ON table1.column_name = table2.column_name;

The OUTER keyword is optional, and can be omitted.

The image below demonstrates how LEFT JOIN works:
nkar 30

Consider the following tables:
customers:
nkar 31

items:
nkar 32

The following SQL statement will return all customers, and the items they might have:
SELECT customers.Name, items.Name 
FROM customers LEFT OUTER JOIN items 
ON customers.ID=items.Seller_id;

Result:
nkar33
The result set contains all the rows from the left table and matching data from the right table. 
If no match is found for a particular row, NULL is returned.

###RIGHT JOIN

The RIGHT JOIN returns all rows from the right table, even if there are no matches in the left table.
nkar 34

The basic syntax of RIGHT JOIN is as follows:
SELECT table1.column1, table2.column2...
FROM table1 RIGHT OUTER JOIN table2
ON table1.column_name = table2.column_name;

Again, the OUTER keyword is optional, and can be omitted.

Consider the same example from our previous lesson, but this time with a RIGHT JOIN:
SELECT customers.Name, items.Name FROM customers
RIGHT JOIN items ON customers.ID=items.Seller_id;

Result:
nkar 35

The RIGHT JOIN returns all the rows from the right table (items), even if there are no matches in the left table (customers).
There are other types of joins in the SQL language, but they are not supported by MySQL.

###Set Operation

Occasionally, you might need to combine data from multiple tables into one comprehensive dataset. This may be for tables with similar data within the same database or maybe there is a need to combine similar data across databases or even across servers. 

To accomplish this, use the UNION and UNION ALL operators. 

UNION combines multiple datasets into a single dataset, and removes any existing duplicates.
UNION ALL combines multiple datasets into one dataset, but does not remove duplicate rows. 
UNION ALL is faster than UNION, as it does not perform the duplicate removal operation over the data set.

UNION

The UNION operator is used to combine the result-sets of two or more SELECT statements.

All SELECT statements within the UNION must have the same number of columns. The columns must also have the same data types. Also, the columns in each SELECT statement must be in the same order.
The syntax of UNION is as follows:
SELECT column_name(s) FROM table1
UNION
SELECT column_name(s) FROM table2;

Here is the First of two tables:


And here is the Second:

SELECT ID, FirstName, LastName, City FROM First
UNION
SELECT ID, FirstName, LastName, City FROM Second;

The resulting table will look like this one:

As you can see, the duplicates have been removed.

TIP:
If your columns don't match exactly across all queries, you can use a NULL (or any other) value such as:
SELECT FirstName, LastName, Company FROM businessContacts
UNION
SELECT FirstName, LastName, NULL FROM otherContacts;

###UNION ALL

UNION ALL selects all rows from each table and combines them into a single table. 

The following SQL statement uses UNION ALL to select data from the First and Second tables:
SELECT ID, FirstName, LastName, City FROM First
UNION ALL
SELECT ID, FirstName, LastName, City FROM Second;

The resulting table:

As you can see, the result set includes the duplicate rows as well.


Inserting Data

SQL tables store data in rows, one row after another. The INSERT INTO statement is used to add new rows of data to a table in the database. 
The SQL INSERT INTO syntax is as follows:
INSERT INTO table_name
VALUES (value1, value2, value3,...);

Make sure the order of the values is in the same order as the columns in the table.

Consider the following Employees table:
nkar
Use the following SQL statement to insert a new row:
INSERT INTO Employees 
VALUES (8, 'Anthony', 'Young', 35);

The values are comma-separated and their order corresponds to the columns in the table.
Result:
nkar
When inserting records into a table using the SQL INSERT statement, you must provide a value for every column that does not have a default value, or does not support NULL.

Inserting Data

Alternatively, you can specify the table's column names in the INSERT INTO statement:
INSERT INTO table_name (column1, column2, column3, ...,columnN)  
VALUES (value1, value2, value3,...valueN);

column1, column2, ..., columnN are the names of the columns that you want to insert data into.
INSERT INTO Employees (ID, FirstName, LastName, Age) 
VALUES (8, 'Anthony', 'Young', 35);

This will insert the data into the corresponding columns:
nkar

You can specify your own column order, as long as the values are specified in the same order as the columns.

Inserting Data

It is also possible to insert data into specific columns only.
INSERT INTO Employees (ID, FirstName, LastName) 
VALUES (9, 'Samuel', 'Clark');

Result:
nkar
The Age column for that row automatically became 0, as that is its default value.

###Updating Data

The UPDATE statement allows us to alter data in the table. 

The basic syntax of an UPDATE query with a WHERE clause is as follows:
UPDATE table_name
SET column1=value1, column2=value2, ...
WHERE condition;

You specify the column and its new value in a comma-separated list after the SET keyword.
If you omit the WHERE clause, all records in the table will be updated!

Updating Data

Consider the following table called "Employees":
nkar

To update John's salary, we can use the following query:
```C#
UPDATE Employees 
SET Salary=5000
WHERE ID=1;
```
Result:
nkar

###Updating Multiple Columns

It is also possible to UPDATE multiple columns at the same time by comma-separating them:
``C#
UPDATE Employees 
SET Salary=5000, FirstName='Robert'
WHERE ID=1;
```
Result:
nkar
You can specify the column order any way you like in the SET clause.

Deleting Data

The DELETE statement is used to remove data from your table. DELETE queries work much like UPDATE queries.
```C#
DELETE FROM table_name
WHERE condition; 
```
For example, you can delete a specific employee from the table:
```C#
DELETE FROM Employees
WHERE ID=1;
```
Result:
nkar
If you omit the WHERE clause, all records in the table will be deleted!
The DELETE statement removes the data from the table permanently.


###SQL Tables

A single database can house hundreds of tables, each playing its own unique role in the database schema. 

SQL tables are comprised of table rows and columns. Table columns are responsible for storing many different types of data, including numbers, texts, dates, and even files.

The CREATE TABLE statement is used to create a new table.
Creating a basic table involves naming the table and defining its columns and each column's data type.

###Creating a Table

The basic syntax for the CREATE TABLE statement is as follows:
CREATE TABLE table_name
(
column_name1 data_type(size),
column_name2 data_type(size),
column_name3 data_type(size),
....
columnN data_type(size)
);

- The column_names specify the names of the columns we want to create.
- The data_type parameter specifies what type of data the column can hold. For example, use int for whole numbers.
- The size parameter specifies the maximum length of the table's column.

Note the parentheses in the syntax.

Assume that you want to create a table called "Users" that consists of four columns: UserID, LastName, FirstName, and City.

Use the following CREATE TABLE statement:
```C#
CREATE TABLE Users
(
   UserID int,
   FirstName varchar(100), 
   LastName varchar(100),
   City varchar(100)
); 
```
varchar is the datatype that stores characters. You specify the number of characters in the parentheses after the type. So in the example above, our fields can hold max 100 characters long text.

Data Types

Data types specify the type of data for a particular column.

If a column called "LastName" is going to hold names, then that particular column should have a "varchar" (variable-length character) data type.

The most common data types:
Numeric
INT -A normal-sized integer that can be signed or unsigned.
FLOAT(M,D) - A floating-point number that cannot be unsigned. You can optionally define the display length (M) and the number of decimals (D).
DOUBLE(M,D) - A double precision floating-point number that cannot be unsigned. You can optionally define the display length (M) and the number of decimals (D). 

Date and Time
DATE - A date in YYYY-MM-DD format.
DATETIME - A date and time combination in YYYY-MM-DD HH:MM:SS format.
TIMESTAMP - A timestamp, calculated from midnight, January 1, 1970
TIME - Stores the time in HH:MM:SS format.

String Type
CHAR(M) - Fixed-length character string. Size is specified in parenthesis. Max 255 bytes.
VARCHAR(M) - Variable-length character string. Max size is specified in parenthesis.
BLOB - "Binary Large Objects" and are used to store large amounts of binary data, such as images or other types of files. 
TEXT - Large amount of text data.
Choosing the correct data type for your columns is the key to good database design.

Primary Key

The UserID is the best choice for our Users table's primary key.
Define it as a primary key during table creation, using the PRIMARY KEY keyword.
```C#
CREATE TABLE Users
(
   UserID int,
   FirstName varchar(100),
   LastName varchar(100),
   City varchar(100),
   PRIMARY KEY(UserID)
); 
```
Specify the column name in the parentheses of the PRIMARY KEY keyword.

Now, when we run the query, our table will be created in the database.


You can now use INSERT INTO queries to insert data into the table.

SQL Constraints

SQL constraints are used to specify rules for table data.

The following are commonly used SQL constraints:
NOT NULL - Indicates that a column cannot contain any NULL value.
UNIQUE - Does not allow to insert a duplicate value in a column. The UNIQUE constraint maintains the uniqueness of a column in a table. More than one UNIQUE column can be used in a table.
PRIMARY KEY - Enforces the table to accept unique data for a specific column and this constraint create a unique index for accessing the table faster.
CHECK - Determines whether the value is valid or not from a logical expression.
DEFAULT - While inserting data into a table, if no value is supplied to a column, then the column gets the value set as DEFAULT.

For example, the following means that the name column disallows NULL values.
name varchar(100) NOT NULL

During table creation, specify column level constraint(s) after the data type of that column.

AUTO INCREMENT

Auto-increment allows a unique number to be generated when a new record is inserted into a table.

Often, we would like the value of the primary key field to be created automatically every time a new record is inserted.

By default, the starting value for AUTO_INCREMENT is 1, and it will increment by 1 for each new record.
Let's set the UserID field to be a primary key that automatically generates a new value:
UserID int NOT NULL AUTO_INCREMENT,
PRIMARY KEY (UserID)


Using Constraints

The example below demonstrates how to create a table using constraints.
```C#
CREATE TABLE Users (
id int NOT NULL AUTO_INCREMENT,
username varchar(40) NOT NULL, 
password varchar(10) NOT NULL,
PRIMARY KEY(id)
);
```
The following SQL enforces that the "id", "username", and "password" columns do not accept NULL values. We also define the "id" column to be an auto-increment primary key field. 

Here is the result:


When inserting a new record into the Users table, it's not necessary to specify a value for the id column; a unique new value will be added automatically.

###ALTER TABLE

The ALTER TABLE command is used to add, delete, or modify columns in an existing table.
You would also use the ALTER TABLE command to add and drop various constraints on an existing table.

Consider the following table called People:
nkar
The following SQL code adds a new column named DateOfBirth:
nkar
Result:
nkar

All rows will have the default value in the newly added column, which, in this case, is NULL.

###Dropping

The following SQL code demonstrates how to delete the column named DateOfBirth in the People table.
```C#
ALTER TABLE People 
DROP COLUMN DateOfBirth;
```
The People table will now look like this:
nkar

The column, along with all of its data, will be completely removed from the table.

To delete the entire table, use the DROP TABLE command:
DROP TABLE People;

###Renaming

The ALTER TABLE command is also used to rename columns:
ALTER TABLE People
CHANGE FirstName name varchar(100);

This query will rename the column called FirstName to name.

Result:
nkar

Renaming Tables

You can rename the entire table using the RENAME command:
RENAME TABLE People TO Users;

This will rename the table People to Users.

###Views

In SQL, a VIEW is a virtual table that is based on the result-set of an SQL statement.

A view contains rows and columns, just like a real table. The fields in a view are fields from one or more real tables in the database.

Views allow us to:
- Structure data in a way that users or classes of users find natural or intuitive.
- Restrict access to the data in such a way that a user can see and (sometimes) modify exactly what they need and no more.
- Summarize data from various tables and use it to generate reports.

To create a view:
```C#
CREATE VIEW view_name AS
SELECT column_name(s)
FROM table_name
WHERE condition;
```
The SELECT query can be as complex as you need it to be. It can contain multiple JOINS and other commands.

Consider the Employees table, which contains the following records:
nkar

Let's create a view that displays each employee's FirstName and Salary.
```C#
CREATE VIEW List AS
SELECT FirstName, Salary
FROM  Employees;
```
Now, you can query the List view as you would query an actual table.
SELECT * FROM List;

This would produce the following result:
nkar

A view always shows up-to-date data! The database engine uses the view's SQL statement to recreate the data each time a user queries a view.


Updating a View

You can update a view by using the following syntax:
CREATE OR REPLACE VIEW view_name AS
SELECT column_name(s)
FROM table_name
WHERE condition;

The example below updates our List view to select also the LastName:
```C#
CREATE OR REPLACE VIEW List AS
SELECT FirstName, LastName, Salary
FROM  Employees;
```
Result:
nkar
You can delete a view with the DROP VIEW command.
```C#
DROP VIEW List;
```


