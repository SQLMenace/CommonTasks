The following query will give you for all the databases the last time it was backed up or display NEVER if it wasn't backed up



```SQL
SELECT s.Name AS DatabaseName,'Database backup was taken on  ' + 
CASE WHEN MAX(b.backup_finish_date) IS NULL THEN 'NEVER!!!' ELSE
CONVERT(VARCHAR(12), (MAX(b.backup_finish_date)), 101) END AS LastBackUpTime
FROM sys.sysdatabases s
LEFT OUTER JOIN msdb.dbo.backupset b ON b.database_name = s.name
GROUP BY s.Name
```
