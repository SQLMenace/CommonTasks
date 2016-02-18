
Index fragmentation


Returns size and fragmentation information for the data and indexes of all the tables in SQL Server.


mode | NULL | DEFAULT
Is the name of the mode. mode specifies the scan level that is used to obtain statistics. mode is sysname. 
Valid inputs are DEFAULT, NULL, LIMITED, SAMPLED, or DETAILED. The default (NULL) is LIMITED.


```SQL

SELECT dm.[object_id]
, DB_NAME(DB_ID()) + '.' + s.[name] +'.' + o.[name]
, dm.[index_id]
, i.[name]
, dm.[partition_number]
, dm.[index_type_desc]
, i.[fill_factor]
, dm.[avg_fragmentation_in_percent],
dm.page_count,
dm.record_count,
dm.min_record_size_in_bytes,
dm.max_record_size_in_bytes
FROM sys.objects o
INNER JOIN sys.indexes i
ON o.[object_id] = i.[object_id] --AND i.name  = NULL
INNER JOIN sys.dm_db_index_physical_stats (DB_ID(), NULL, NULL, NULL, 'SAMPLED') dm
ON i.[object_id] = dm.[object_id]
AND i.[index_id] = dm.[index_id]
--AND dm.[avg_fragmentation_in_percent] >= 5
INNER JOIN sys.schemas s
ON o.[schema_id] = s.[schema_id]
INNER JOIN sys.stats st
ON i.[name] = st.[name] AND o.[object_id] = st.[object_id]
AND o.[type] = 'U'
```
