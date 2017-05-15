#

### [Create logins]()
Security->Logins->New login->


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

#### 15.05.2017
```C#
Alter table Students add GenderID int not null default(1)
```
```C#
select * from Students
```

```C#
Select * from Students
where GenderID=1
```

```C#
Select count(StudentID) as a from Students
where GenderID=2
group by FacultyID
```
```C#
--Stanal aghjikneri qanaky,FacultyID,FacultyName
Select Count(StudentID) as [COUNT], [Faculties].FacultyID, max(Faculties.FacultyName) as Name from 
  Students inner join Faculties on Students.FacultyID=Faculties.FacultyID
   Where GenderId=1
  Group By Faculties.FacultyID   --ete gender id-ov khmbavoreinq, apa max -Y skhal kberer
  --they are same
  select tmp.*, Faculties.FacultyName from Faculties inner join   --tmp.*-y kberi arden nor aliasi syunery
  (
  select [Students].FacultyID,  Count(StudentID) as st_cnt from  Students
    where GenderId=1
    Group By Students.FacultyID  
  ) as tmp on Faculties.FacultyID=tmp.FacultyID
  
```



 #### --they  are same, bayc aranc null-i  ev isull funkciayi ognutyamb
 ```C#
  Select isnull(tgha.FacultyID , agjik.FacultyID) as FacultyID,
   isnull(tgha.Name,agjik.Name) as FacultyName, tgha.COUNTTgha, agjik.COUNTAghjik from
   (Select Count(StudentID) as [COUNTTgha], [Faculties].FacultyID, max(Faculties.FacultyName) as Name from 
  Students inner join Faculties on Students.FacultyID=Faculties.FacultyID
   Where GenderId=1
  Group By Faculties.FacultyID ) as tgha 
  full join 
      (Select Count(StudentID) as [COUNTAghjik], [Faculties].FacultyID, max(Faculties.FacultyName) as Name from 
  Students inner join Faculties on Students.FacultyID=Faculties.FacultyID
   Where GenderId=2
  Group By Faculties.FacultyID ) as agjik on agjik.FacultyID=tgha.FacultyId
```

#### creating views
```c#
create view Faculty_Gender_Count as
  Select isnull(tgha.FacultyID , agjik.FacultyID) as FacultyID,
   isnull(tgha.Name,agjik.Name) as FacultyName, tgha.COUNTTgha as MaleCount, agjik.COUNTAghjik FemaleCount from
   (Select Count(StudentID) as [COUNTTgha], [Faculties].FacultyID, max(Faculties.FacultyName) as Name from 
  Students inner join Faculties on Students.FacultyID=Faculties.FacultyID
   Where GenderId=1
  Group By Faculties.FacultyID ) as tgha 
  full join 
      (Select Count(StudentID) as [COUNTAghjik], [Faculties].FacultyID, max(Faculties.FacultyName) as Name from 
  Students inner join Faculties on Students.FacultyID=Faculties.FacultyID
   Where GenderId=2
  Group By Faculties.FacultyID ) as agjik on agjik.FacultyID=tgha.FacultyId
 ```
