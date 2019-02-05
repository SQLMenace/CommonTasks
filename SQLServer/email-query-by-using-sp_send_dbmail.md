Here is a quick and dirty way to quickly email the results of a query


``` SQL

declare @DBEmailProfileName varchar(100) ='Db profile'
declare @recipients varchar(100) = '...@...com'
declare @subject nvarchar(100) = 'Testing email..subject'
declare @body varchar(100) = 'Body text goes here'

exec msdb.dbo.sp_send_dbmail      
@profile_name =@DBEmailProfileName    -- if ommited..it will use default profile 
, @recipients = @recipients  
--, @copy_recipients = @copy_recipientsTo      
, @subject = @subject      
, @body_format = 'text'     --'HTML'  
, @body = @body  
, @attach_query_result_as_file=  0   -- 1 if you want the query attached as a file
, @query = '      
  
set nocount on;      
exec xp_fixeddrives    
'        
, @execute_query_database = 'master'      
, @query_result_width = 1000      
, @query_result_header = 1 

```
