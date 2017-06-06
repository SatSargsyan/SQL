#
## [ORDER BY](https://msdn.microsoft.com/en-us/library/bb399723(v=vs.110).aspx)
####Ordering Nested Queries
In the Entity Framework, a nested expression can be placed anywhere in the query; the order of a nested query is not preserved.
```C#
-- The following query will order the results by the last name.  
SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact as C1  
        ORDER BY C1.LastName  

-- In the following query, ordering of the nested query is **ignored**.  
SELECT C2.FirstName, C2.LastName  
    FROM (SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact as C1  
        ORDER BY C1.LastName) as C2  
```
## [Sorting data using order by](https://msdn.microsoft.com/en-us/library/cc716784(v=vs.100).aspx)
