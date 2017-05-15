#

###[Create logins]()

For writing another language, we will write    N'Անունը'



```c#
Select [StudentID], 
FirstName+' '+LastName  as ALLName
from[dbo].[Students]
where  StudentID between 2 and 10
```



LTRIM probelner maqrum e dzakhic, RTRIM  probelner maqrum e ajic erb char enq sahmanats linum

```C#
Select [StudentID], 
FirstName+' '+LastName+' '+cast(StudentID as varchar(200))
  as ALLName
from[dbo].[Students]
where  StudentID between 2 and 10
```

```C#
Select [StudentID], 
FirstName+' '+LastName+' '+cast(StudentID as varchar(200))
  as ALLName
from[dbo].[Students]
```

```C#
Select [StudentID], 
FirstName+' '+LastName+' '+cast(StudentID as varchar(200))
  as ALLName
from[dbo].[Students]
where FirstName like N'լի%'
```


```C#
convert(varchar,StudentID)
```

convert@ nuyn castn e anum, bayc 3 argument karogh e @ndunel

```C#
Select 
count(StudentID), FacultyID from Students
group by FacultyID
```


foreign key jnjelu  hamar alter table delete-ov jnjel, nor drop anel table-@

```C#
select count(StudentID) as SumID, [FacultyID] from Students
Group By [FacultyID]
having count(StudentID)>4
```


```C#
select count(*)  from (
select count(StudentID) as SumID, [FacultyID] from Students
Group By [FacultyID] ) as nor
where SumID>4
```

```C#
Select *from [dbo].[Students]
join [dbo].[Faculties]on [Students].[FacultyID]=[Faculties].FacultyID
```


```C#
Select Count(StudentID) as [COUNT], [Faculties].FacultyID, max(Faculties.FacultyName) as Name from 
  Students inner join Faculties on Students.FacultyID=Faculties.FacultyID
  Group By Faculties.FacultyID
```
```C#
Select * from ( Select [FirstName],StudentID
  from [dbo].[Students] 
  union
  select [LastName],StudentID
  from [dbo].[Students]) as nor
  order by StudentID
 ```
 
 ```C#
 Select * from ( Select [FirstName],StudentID
  from [dbo].[Students] 
  union all
  select [LastName],StudentID
  from [dbo].[Students]) as nor
  order by StudentID
  ```

