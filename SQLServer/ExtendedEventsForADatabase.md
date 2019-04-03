Here is a quick way to create an Extended Event sessions to filter on a specific database, just replace YourDatabase in the WHERE clause to the database name you are interested in


```SQL
IF EXISTS (SELECT null FROM sys.server_event_sessions  WHERE name = 'ProcsExecutions')
DROP EVENT SESSION ProcsExecutions ON SERVER
GO

CREATE EVENT SESSION ProcsExecutions ON SERVER 
ADD EVENT sqlserver.rpc_completed(
    ACTION(sqlos.task_time,sqlserver.client_app_name,sqlserver.client_hostname,sqlserver.database_name,sqlserver.sql_text)
    WHERE ([sqlserver].[database_name]=N'YourDatabase')
	),
ADD EVENT sqlserver.rpc_starting(
    ACTION(sqlos.task_time,sqlserver.client_app_name,sqlserver.client_hostname,sqlserver.database_name,sqlserver.sql_text)
    WHERE ([sqlserver].[database_name]=N'YourDatabase')
	 )


```
