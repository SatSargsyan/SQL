#
## [ORDER BY](https://msdn.microsoft.com/en-us/library/bb399723(v=vs.110).aspx)
#### Ordering Nested Queries
In the Entity Framework, a nested expression can be placed anywhere in the query; the order of a nested query is not preserved.

-- The following query will order the results by the last name.  
```C#

SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact as C1  
        ORDER BY C1.LastName  
```
-- In the following query, ordering of the nested query is **ignored**.  
```C#

SELECT C2.FirstName, C2.LastName  
    FROM (SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact as C1  
        ORDER BY C1.LastName) as C2  
```
## [Sorting data using order by](https://msdn.microsoft.com/en-us/library/cc716784(v=vs.100).aspx)

## Multiple sort 
```C#
var Result = Items.OrderBy(x => x.DateModified).ThenBy(x => x.DateCreated);
```
### [Order by multiple columns using Lambas and LINQ](https://dzone.com/articles/how-order-multiple-columns)
Assuming  list is “Phones” and contains the following data
```C#
public class Phone
{
       public int ID { get; set; }
       public string Name { get; set; }
}
public class Phones : List
{
        public Phones()
        {
            Add(new Phone { ID = 1, Name = "Windows Phone 7" });
            Add(new Phone { ID = 5, Name = "iPhone" });
            Add(new Phone { ID = 2, Name = "Windows Phone 7" });
            Add(new Phone { ID = 3, Name = "Windows Mobile 6.1" });
            Add(new Phone { ID = 6, Name = "Android" });
            Add(new Phone { ID = 10, Name = "BlackBerry" });
        }
}
```
```C#
dataGridView1.DataSource = (from m in new Phones()
                                       orderby m.Name, m.ID
                                       select m).ToList();
```
The same we can do using lambda expression
```C#
dataGridView1.DataSource = new Phones().OrderByDescending(a => a.Name).ThenByDescending(a => a.ID).ToList();
```
