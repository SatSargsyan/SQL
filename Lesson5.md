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
View-i het ashkhatum enq inchpes sovorakan table-i het

```C#
select * from   Faculty_Gender_Count
```

### PROCEDURE VS FUNCTION

```c#
alter proc INS_Students
@StudentID int null,
 @FirstName nvarchar(100), 
 @LastName nvarchar(100),
  @Email nvarchar(100),
   @Tel_number nvarchar(100), 
   @Birt_of_date date, 
   @Resume nvarchar(max), 
   @FacultyID int, 
   @Address nvarchar(100),
    @GenderID int  
	as
	begin
	if (@studentID is null)
	begin
	insert into [dbo].[Students]( FirstName, LastName, Email, Tel_number, Birt_of_date, [Resume], FacultyID, [Address], GenderID)
	values ( @FirstName, @LastName, @Email, @Tel_number, @Birt_of_date, @Resume, @FacultyID, @Address, @GenderID)
	select * from Students where StudentID=scope_identity()
	end 
	else
	begin
	update Students set
	FirstName=isnull(@FirstName,FirstName),
	 LastName=isnull(@LastName, LastName),
	 Email=isnull(@Email, Email),
	 Tel_number=isnull(@Tel_number,Tel_number),
	  Birt_of_date=isnull(@Birt_of_date,Birt_of_date),
	   [Resume]=isnull(@Resume, [Resume]),
	   FacultyID=isnull(@FacultyID,FacultyID),
	    [Address]=isnull(@Address,[Address]),
		 GenderID=isnull(@GenderID,GenderID)
		 where StudentID=@StudentID
		 end
		 select * from Students where StudentID=@StudentID
	end

```


procedure-n aveli layn hnaravorutyunner uni, qan function-y. So that prosedure-i mej karogh enq func ogtagortsel, bayc func-i mej proc chenq karogh

select-i mej func karogh enq grel, proc voch

proc-y execute e linum

### [Exists transact-sql](https://docs.microsoft.com/en-us/sql/t-sql/language-elements/exists-transact-sql)
[Exists](https://www.techonthenet.com/sql/exists.php)-y result set e veradardznum
[Exists Examples](https://www.w3schools.com/sql/sql_exists.asp)
[Exists examples](http://www.dofactory.com/sql/where-exists)
```C#
create function  FN_AGECALC(@DATE date)
returns int
as
begin
declare @res int
set @res=YEAR(getdate())-YEAR(@DATE)
return @res
end


-------------------------------------------------Ashkhatacnenq func-y
select dbo.FN_AGECALC(GETDATE()) as AgeFunc
----------------------------------------------------
--gtnenq mer students-ic ogtagortselov mer grats func-y
select FirstName,LastName, dbo.FN_AGECALC([Birt_of_date]) as Age  from Students
---------------------------------------------------
declare @var int 
set @var=1

print @var
--they are same
declare @var int 
select @var=1

print @var
------------------------------------------------------------------------------
--selectn ayn aravelutyunn uni set-ic, vor  karogh enq naev nshel vor table-ic ev naev payman

declare @var int 
set @var=FacultyID from students --where StudentID=4

print @var




create function  FN_concat(@facultyId int)
returns nvarchar(max)
as
begin
declare @firstname nvarchar(max)=''
Select @firstname+=' ,'+[FirstName] from [dbo].[Students] where [FacultyID]=@facultyId
return @firstname
end


select [FacultyID],[FacultyName],dbo.FN_concat(FacultyID) as names from Faculties
```


### [Triggers](https://docs.microsoft.com/en-us/sql/t-sql/statements/create-trigger-transact-sql)
```C#
create trigger INS_Check
on [dbo].[Students]
after insert
as
begin
select * from inserted
end




insert into [dbo].[Students]
([FirstName],[LastName],[FacultyID],[GenderID])
values
('karen','Tovmasyan',1,1),
('Liana','Tovmasyan',1,2),
('karen','Tovmasyan',1,1),
('Liana','Tovmasyan',1,2),
('karen','Tovmasyan',1,1),
('Liana','Tovmasyan',1,2),
('karen','Tovmasyan',1,1),
('Liana','Tovmasyan',1,2),
('karen','Tovmasyan',1,1),
('Liana','Tovmasyan',1,2),
('karen','Tovmasyan',1,1),
('Liana','Tovmasyan',1,2),
('karen','Tovmasyan',1,1),
('Liana','Tovmasyan',1,2)



--------------------------------------------------------------
create trigger INS_Limited
on [dbo].[Students]
after insert
as
begin 
if exists (select 1 /* count(*)  */ from Students 
	where [FacultyID] in (select  [FacultyID] from inserted)
	group by  FacultyID
	having count(*)>10)  
	begin
	Rollback
	end
end

```

After that chi toghni, ete pordzenq avelacnel, kta hetevyal errorY
```C#

(14 row(s) affected)
Msg 3609, Level 16, State 1, Line 63
The transaction ended in the trigger. The batch has been aborted.
```

### [Check constrait]()
### [Unique and check](https://docs.microsoft.com/en-us/sql/relational-databases/tables/unique-constraints-and-check-constraints)

### Unique constrait 
Unique-y tuyl e talis null, i tarberutyun primary key-i

Cascading

```C#
Select *from Students
order by StudentID desc offset 5 rows fetch next 5 rows only
------------------------------------------------------------
declare @off int=6, @next int =5
Select *from Students
order by StudentID desc offset  @off rows fetch next @next rows only
```

### Window functions

```C#
select *, count(*) over(partition by FacultyID)from Students
```




### Index
amen inch bajanum e 8kb-oc ejeri

[Clustered index](https://docs.microsoft.com/en-us/sql/relational-databases/indexes/clustered-and-nonclustered-indexes-described)

primary key clustered index e sarqum,
u miayn mek clustered index karogh e unenal, hgum chi parunakum, henc nuyn tabli mej e sarqum



### [Transactions](https://docs.microsoft.com/en-us/sql/t-sql/language-elements/transactions-transact-sql)


[ACID](https://msdn.microsoft.com/en-us/library/aa480356.aspx)


