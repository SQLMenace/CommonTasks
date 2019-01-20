This will tell you if there are any databases or logs being backed up or restored at this moment


```SQL
SELECT 
    d.PERCENT_COMPLETE AS [%Complete],
    d.TOTAL_ELAPSED_TIME/60000 AS ElapsedTimeMin,
    d.ESTIMATED_COMPLETION_TIME/60000   AS TimeRemainingMin,
    d.TOTAL_ELAPSED_TIME*0.00000024 AS ElapsedTimeHours,
    d.ESTIMATED_COMPLETION_TIME*0.00000024  AS TimeRemainingHours,
    d.COMMAND as Command,
    s.text as CommandExecuted
FROM    sys.dm_exec_requests d
CROSS APPLY sys.dm_exec_sql_text(d.sql_handle)as s
WHERE  d.COMMAND LIKE 'RESTORE DATABASE%'
or d.COMMAND     LIKE 'RESTORE LOG%'
OR d.COMMAND     LIKE 'BACKUP DATABASE%'
OR d.COMMAND     LIKE 'BACKUP LOG%'
ORDER   BY 2 DESC, 3 DESC
```
