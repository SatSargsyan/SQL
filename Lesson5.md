#

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


