This lists all tables with identity columns and their last value in the table

```SQL
SELECT  @@Servername AS ServerName ,
        DB_NAME() AS DBName ,
        OBJECT_SCHEMA_NAME(object_id) AS SchemaName ,
        OBJECT_NAME(object_id) AS TableName ,
        Column_id ,
        Name AS IdentityColumn ,
        Seed_Value ,
        Last_Value,
		increment_value
FROM    sys.identity_columns
ORDER BY SchemaName ,
        TableName ,
        Column_id;
```
