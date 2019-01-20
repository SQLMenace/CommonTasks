The syntax to rename a table is as follows

```SQL
EXEC sp_rename 'Schema.Tablename', 'NewTableName';  
```

So if you have a table named dbo.Cars and you want to rename it to Vehicles in the same schema, you would do the following


```SQL
EXEC sp_rename 'dbo.Cars', 'Vehicles';  
```
