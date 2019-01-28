A basic view of all the user connections to the database servers


```SQL
SELECT  @@Servername AS Server ,
        DB_NAME(database_id) AS DatabaseName ,
        Login_name AS LoginName ,
       last_request_start_time,
        last_request_end_time, 
		program_name,
		host_name,
		status,
		cpu_time,
		memory_usage,
		reads,
		writes
FROM    sys.dm_exec_sessions
WHERE   is_user_process = 1
ORDER BY DatabaseName;
```
