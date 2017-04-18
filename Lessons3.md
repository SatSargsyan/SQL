### TRUNCATE TABLE

#### The SQL [TRUNCATE TABLE](https://www.tutorialspoint.com/sql/sql-truncate-table.htm) command is used to delete complete data from an existing table.

You can also use [DROP TABLE]() command to delete complete table but it would remove complete table structure form the database and you would need to re-create this table once again if you wish you store some data.

Syntax:
The basic syntax of TRUNCATE TABLE is as follows:
```c#
TRUNCATE TABLE  table_name;
```

### [VIEW ](https://www.tutorialspoint.com/sql/sql-using-views.htm)

A view is nothing more than a SQL statement that is stored in the database with an associated name. A view is actually a composition of a table in the form of a predefined SQL query.

A view can contain all rows of a table or select rows from a table. A view can be created from one or many tables which depends on the written SQL query to create a view.

Views, which are kind of virtual tables, allow users to do the following:

Structure data in a way that users or classes of users find natural or intuitive.

Restrict access to the data such that a user can see and (sometimes) modify exactly what they need and no more.

Summarize data from various tables which can be used to generate reports.

Creating Views:
Database views are created using the CREATE VIEW statement. Views can be created from a single table, multiple tables, or another view.

To create a view, a user must have the appropriate system privilege according to the specific implementation.

The basic CREATE VIEW syntax is as follows:
```C#
CREATE VIEW view_name AS
SELECT column1, column2.....
FROM table_name
WHERE [condition];
```
You can include multiple tables in your SELECT statement in very similar way as you use them in normal SQL SELECT query.

```C#
CREATE VIEW CUSTOMERS_VIEW AS
SELECT name, age
FROM  CUSTOMERS;
```
