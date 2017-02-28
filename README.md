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



