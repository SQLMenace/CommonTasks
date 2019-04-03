This query will return all the active extended events sessions, you can quickly see the properties


```sql

SELECT dxs.name,
dxs.create_time,*
FROM sys.dm_xe_sessions AS dxs;


```

This query will give you all the sessions, even the ones that are not running

```SQL
 SELECT *
 FROM sys.server_event_sessions 
 ```
