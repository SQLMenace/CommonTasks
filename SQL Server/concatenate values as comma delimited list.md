
How to concatenate a comma delimited list from a bunch of values in rows
Create a simple table so that we can run this example
``` SQL
CREATE TABLE #Temp (id int,
					name varchar(100),
					SomeDate datetime,
					SomeCode char(5),
					CurrencyCode char(3))
```

Make sure this returns something
``` SQL
SELECT * FROM tempdb.dbo.syscolumns
WHERE id = OBJECT_ID('tempdb.dbo.#Temp')
```

This is the code
``` SQL
DECLARE @ColumnList VARCHAR(8000)
        SELECT @ColumnList = (
        SELECT  name + ', ' AS [text()]
			FROM tempdb.dbo.syscolumns
			WHERE id = OBJECT_ID('tempdb.dbo.#Temp')
			ORDER BY colorder
	FOR XML PATH('') )
 
SELECT LEFT(@ColumnList,(LEN(@ColumnList) -1))
```
And here is what the output looks like
```
id, name, SomeDate, SomeCode, CurrencyCode
```
