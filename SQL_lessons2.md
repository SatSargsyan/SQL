### [NUMA](https://technet.microsoft.com/en-us/library/ms178144(v=sql.105).aspx)
Understanding Non-uniform Memory Access

Microsoft SQL Server is non-uniform memory access (NUMA) aware, and performs well on NUMA hardware without special configuration. As clock speed and the number of processors increase, it becomes increasingly difficult to reduce the memory latency required to use this additional processing power. To circumvent this, hardware vendors provide large L3 caches, but this is only a limited solution. NUMA architecture provides a scalable solution to this problem. SQL Server has been designed to take advantage of NUMA-based computers without requiring any application changes.


### [Indexes](https://www.tutorialspoint.com/sql/sql-indexes.htm)

[What is index](https://ru.wikipedia.org/wiki/%D0%98%D0%BD%D0%B4%D0%B5%D0%BA%D1%81_(%D0%B1%D0%B0%D0%B7%D1%8B_%D0%B4%D0%B0%D0%BD%D0%BD%D1%8B%D1%85))

[CREATE INDEX](https://msdn.microsoft.com/ru-ru/library/ms188783.aspx)

[CREATE INDEX Example](https://www.w3schools.com/sql/sql_create_index.asp)

[Структура индекса](https://habrahabr.ru/post/247373/)
![index_sql](https://cloud.githubusercontent.com/assets/25159667/25070935/9d458562-22bb-11e7-9a65-6f09dd6f190c.JPG)

[Indexes](https://www.tutorialspoint.com/sql/sql-indexes.htm) are special lookup tables that the database search engine can use to speed up data retrieval. Simply put, an index is a pointer to data in a table. An index in a database is very similar to an index in the back of a book.

For example, if you want to reference all pages in a book that discuss a certain topic, you first refer to the index, which lists all topics alphabetically and are then referred to one or more specific page numbers.

An index helps speed up SELECT queries and WHERE clauses, but it slows down data input, with UPDATE and INSERT statements. Indexes can be created or dropped with no effect on the data.

Creating an index involves the CREATE INDEX statement, which allows you to name the index, to specify the table and which column or columns to index, and to indicate whether the index is in ascending or descending order.

Indexes can also be unique, similar to the UNIQUE constraint, in that the index prevents duplicate entries in the column or combination of columns on which there's an index.

#### The CREATE INDEX Command:
The basic syntax of CREATE INDEX is as follows:
```C#
CREATE INDEX index_name ON table_name;
```
#### Single-Column Indexes:
A single-column index is one that is created based on only one table column. The basic syntax is as follows:
```C#
CREATE INDEX index_name
ON table_name (column_name);
```
#### Unique Indexes:
Unique indexes are used not only for performance, but also for data integrity. A unique index does not allow any duplicate values to be inserted into the table. The basic syntax is as follows:
```C#
CREATE UNIQUE INDEX index_name
on table_name (column_name);
```
#### Composite Indexes:
A composite index is an index on two or more columns of a table. The basic syntax is as follows:
```C#
CREATE INDEX index_name
on table_name (column1, column2);
```
Whether to create a single-column index or a composite index, take into consideration the column(s) that you may use very frequently in a query's WHERE clause as filter conditions.

Should there be only one column used, a single-column index should be the choice. Should there be two or more columns that are frequently used in the WHERE clause as filters, the composite index would be the best choice.

#### Implicit Indexes:
Implicit indexes are indexes that are automatically created by the database server when an object is created. Indexes are automatically created for primary key constraints and unique constraints.

#### The DROP INDEX Command:
An index can be dropped using SQL DROP command. Care should be taken when dropping an index because performance may be slowed or improved.

The basic syntax is as follows:
```C#
DROP INDEX index_name;
```
You can check INDEX Constraint chapter to see actual examples on Indexes.

### When should indexes be avoided?
Although indexes are intended to enhance a database's performance, there are times when they should be avoided. The following guidelines indicate when the use of an index should be reconsidered:

##### Indexes should not be used on small tables.

##### Tables that have frequent, large batch update or insert operations.

##### Indexes should not be used on columns that contain a high number of NULL values.

##### Columns that are frequently manipulated should not be indexed.

