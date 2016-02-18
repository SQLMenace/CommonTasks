Sometimes you want to quickly see how many files a database has, how much space a file is using and how much space is free. 
You can use the sys.database_files catalog view.


```SQL
SELECT
    a.file_id ,
    CONVERT(DECIMAL(12,2),ROUND(a.size/128.000,2)) AS [file_size_mb],
    CONVERT(DECIMAL(12,2),ROUND(FILEPROPERTY(a.name,'SpaceUsed')/128.000,2)) AS [space_used_mb] ,
    CONVERT(DECIMAL(12,2),ROUND((a.size-FILEPROPERTY(a.name,'SpaceUsed'))/128.000,2)) AS [free_space_mb],
    name,
    a.physical_name
FROM
 sys.database_files a
```
