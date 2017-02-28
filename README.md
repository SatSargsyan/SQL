# SQL


Fill in the missing keyword to list the table names.
Show Tables



The WHERE Statement

The WHERE clause is used to extract only those records that fulfill a specified criterion.

The syntax for the WHERE clause:
SELECT column_list 
FROM table_name
WHERE condition;

Consider the following table:
nkar sql1


In the above table, to SELECT a specific record:
SELECT * FROM customers
WHERE ID = 7;

nkar sql2

###SQL Operators

Comparison Operators and Logical Operators are used in the WHERE clause to filter the data to be selected.

The following comparison operators can be used in the WHERE clause:

nkar sql3

For example, we can display all customers names listed in our table, with the exception of the one with ID 5.
SELECT * FROM customers
WHERE ID != 5;

nkar sql4

As you can see, the record with ID=5 is excluded from the list.


###The BETWEEN Operator

The BETWEEN operator selects values within a range. The first value must be lower bound and the second value, the upper bound.

The syntax for the BETWEEN clause is as follows:
SELECT column_name(s)
FROM table_name
WHERE column_name BETWEEN value1 AND value2;

The following SQL statement selects all records with IDs that fall between 3 and 7:
SELECT * FROM customers 
WHERE ID BETWEEN 3 AND 7;

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
SELECT ID, FirstName, LastName, Age
FROM customers
WHERE Age >= 30 AND Age <= 40;

This results in the following output:

nkar sql9

You can combine as many conditions as needed to return the desired results.
###OR

If you want to select rows that satisfy at least one of the given conditions, you can use the logical OR operator.

The following table describes how the logical OR operator functions:
nkar 10


For example, if you want to find the customers who live either in New York or Chicago, the query would like this:
SELECT * FROM customers 
WHERE City = 'New York' OR City = 'Chicago';

Result:
nkar 11

###Combining AND & OR

The SQL AND and OR conditions may be combined to test multiple conditions in a query. 
These two operators are called conjunctive operators.

When combining these conditions, it is important to use parentheses, so that the order to evaluate each condition is known.

Consider the following table:

nkar 12

The statement below selects all customers from the city "New York" AND with the age equal to "30" OR “35":
SELECT * FROM customers
WHERE City = 'New York'
AND (Age=30 OR Age=35);

Result:
nkar13


You can nest as many conditions as you need.

Fill in the blanks to select customers whose ids are either 1 or 2, and whose city is ''Boston''.
SELECT * FROM customers
WHERE (id = 1 OR  id = 2)
AND city = 'Boston'

###The IN Operator

The IN operator is used when you want to compare a column with more than one value. 

For example, you might need to select all customers from New York, Los Angeles, and Chicago.
With the OR condition, your SQL would look like this:
SELECT * FROM customers 
WHERE City = 'New York'
OR City = 'Los Angeles'
OR City = 'Chicago';

Result:
nkar 15

###The IN Operator

You can achieve the same result with a single IN condition, instead of the multiple OR conditions:
SELECT * FROM customers 
WHERE City IN ('New York', 'Los Angeles', 'Chicago');

This would also produce the same result:
nkar 16
Note the use of parentheses in the syntax.


###The NOT IN Operator

The NOT IN operator allows you to exclude a list of specific values from the result set. 

If we add the NOT keyword before IN in our previous query, customers living in those cities will be excluded:
SELECT * FROM customers 
WHERE City NOT IN ('New York', 'Los Angeles', 'Chicago');

Result:
nkar 17

###The CONCAT Function

The CONCAT function is used to concatenate two or more text values and returns the concatenating string.

Let's concatenate the FirstName with the City, separating them with a comma:
SELECT CONCAT(FirstName, ', ' , City) FROM customers;

The output result is:
nkar 18

###The AS Keyword

A concatenation results in a new column. The default column name will be the CONCAT function.
You can assign a custom name to the resulting column using the AS keyword:
SELECT CONCAT(FirstName,', ', City) AS new_column 
FROM customers;

And when you run the query, the column name appears to be changed.
nkar 19


###Arithmetic Operators

Arithmetic operators perform arithmetical operations on numeric operands. The Arithmetic operators include addition (+), subtraction (-), multiplication (*) and division (/). 

The following employees table shows employee names and salaries:
nkar 20
The example below adds 500 to each employee's salary and selects the result:
SELECT ID, FirstName, LastName, Salary+500 AS Salary
FROM employees;

Result:
nkar 21

###The UPPER Function

The UPPER function converts all letters in the specified string to uppercase. 
The LOWER function converts the string to lowercase.

The following SQL query selects all LastNames as uppercase:
SELECT FirstName, UPPER(LastName) AS LastName 
FROM employees;

Result:
nkar 22

If there are characters in the string that are not letters, this function will have no effect on them.

###SQRT and AVG

The SQRT function returns the square root of given value in the argument.

Let's calculate the square root of each Salary:
SELECT Salary, SQRT(Salary) 
FROM employees;

Result:
nkar 23

Similarly, the AVG function returns the average value of a numeric column:
SELECT AVG(Salary) FROM employees;

Result:
nkar 24

The SUM function

The SUM function is used to calculate the sum for a column's values

For example, to get the sum of all of the salaries in the employees table, our SQL query would look like this:
SELECT SUM(Salary) FROM employees;

Result:
nkar 25

The sum of all of the employees' salaries is 31000.

###Subqueries
A subquery is a query within another query. 

Let's consider an example. We might need the list of all employees whose salaries are greater than the average.
First, calculate the average:
SELECT AVG(Salary) FROM employees;

As we already know the average, we can use a simple WHERE to list the salaries that are greater than that number.
SELECT FirstName, Salary FROM employees 
WHERE  Salary > 3100
ORDER BY Salary DESC;

The DESC keyword sorts results in descending order. 
Similarly, ASC sorts the results in ascending order.

Result:
nkar 26


A single subquery will return the same result more easily.
SELECT FirstName, Salary FROM employees 
WHERE  Salary > (SELECT AVG(Salary) FROM employees) 
ORDER BY Salary DESC;

The same result will be produced.
nkar 26 the same

Enclose the subquery in parentheses. 
Also, note that there is no semicolon at the end of the subquery, as it is part of our single query.

###The Like Operator

The LIKE keyword is useful when specifying a search condition within your WHERE clause.
SELECT column_name(s)
FROM table_name
WHERE column_name LIKE pattern;

SQL pattern matching enables you to use "_" to match any single character and "%" to match an arbitrary number of characters (including zero characters).

For example, to select employees whose FirstNames begin with the letter A, you would use the following query:
SELECT * FROM employees 
WHERE FirstName LIKE 'A%';

Result:
nkar 27

As another example, the following SQL query selects all employees with a LastName ending with the letter "s":
SELECT * FROM employees 
WHERE LastName LIKE '%s';

Result:
nkar 28
The % wildcard can be used multiple times within the same pattern.


###The MIN Function

The MIN function is used to return the minimum value of an expression in a SELECT statement.

For example, you might wish to know the minimum salary among the employees.
SELECT MIN(Salary) AS Salary FROM employees;


All of the SQL functions can be combined together to create a single expression.





