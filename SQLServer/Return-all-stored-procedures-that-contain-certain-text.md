Sometimes you need to know then names of all the stored procedures that use a table or have a certain piece of code in them. Here is how to do that.


```SQL
SELECT * FROM sys.procedures
WHERE object_definition(object_id)  like '%mail%'
order by name
```
