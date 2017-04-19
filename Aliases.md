### [Aliases](https://www.youtube.com/watch?v=w1F0UgsYfis) are "alternate names" used for Columns and Tables.

### [Column Aliases]()

```C#
SELECT column_name as column_alias
FROM table_name

or

SELECT column_name  column_alias /**** without as ****/
FROM table_name
```

### [Using Table Aliases](https://technet.microsoft.com/en-us/library/ms187455(v=sql.105).aspx)

The readability of a SELECT statement can be improved by giving a table an alias, also known as a correlation name or range variable. A table alias can be assigned either with or without the AS keyword:
```C#
table_name AS table alias

or

table_name table_alias
```

```C#
SELECT table_alias.column_name, table_alias.column_name
FROM table_name table_alias
```

```C#
SELECT table_alias.column_name as column_alias
FROM table_name table_alias
```
In the following example the alias c is assigned to Customer and the alias s is assigned to Store.


```C#
SELECT c.CustomerID, s.Name
FROM Sales.Customer AS c
JOIN Sales.Store AS s
ON c.CustomerID = s.BusinessEntityID ;
```
