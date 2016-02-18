
To list all the tables that are partitioned you can use the sys.partitions view. 
However be aware that all tables and indexes in SQL Server contain at least one partition.
We filter out all the objects with just 1 partition

```SQL
SELECT object_name(object_id),index_id,partition_number,rows,data_compression_desc
FROM sys.partitions s
WHERE EXISTS(SELECT NULL 
                FROM sys.partitions s2 
                WHERE s.object_id = s2.object_id 
                AND partition_number > 1
                AND s.index_id = s2.index_id)
ORDER BY object_name(object_id),index_id,rows DESC
```
