How to quickly dump the results from a query into a csv file

```Powershell
Invoke-Sqlcmd -ServerInstance .\sql2016 -Database msdb -Query "
SELECT TOP 1000 name,create_date
FROM sys.procedures
ORDER BY create_date" |
export-csv  -NoTypeInformation -path  c:\temp\QueryOutput.csv
```
