
If you have a user defined table type and you need to know quickly generate some varianle with the same type, you csan use this code

For example if this is your table type

```SQL
CREATE TYPE [dbo].[MyCustomType] AS TABLE(
	[SomeId] [int] NULL,
	[SomeOtherId] [int] NULL,
	[SomeDate] [datetime] NOT NULL,
	SOmeValue varchar(100) not null)
GO
```

And you run this

```SQL

       declare @TableTpeName VARCHAR(100)
	   select @TableTpeName = 'MyCustomType'  -- the name of the tabe type


	   select 'DECLARE @' + c.name + ' ' +  t.name + 
	   case when c.user_type_id =167 then '(' + convert(varchar(100),c.max_length) + ')'  + ' = ''Bla''' 
	        when c.user_type_id in(106,108) then '(' + convert(varchar(100),c.precision) + ',' + convert(varchar(100),c.scale) + ')'  + ' = 0' 
	        when c.user_type_id in(56,127,104) then '' + ' = 0' 
			when c.user_type_id in(61) then '' + ' = ''20131210''' 
	   end as ScalePrecision 
	   from sys.all_columns c
	   join sys.types t on c.user_type_id = t.user_type_id
	   where object_name(object_id)  like '%' + @TableTpeName + '%'


	   
	   
	   declare @name varchar(8000)
	   select @name ='SELECT '
	   select @name = @name + '@' + c.name +', '
	   from sys.all_columns c
	   join sys.types t on c.user_type_id = t.user_type_id
	   where object_name(object_id) like '%' + @TableTpeName + '%'

	   SELECT @name = LEFT(@name,LEN(@name)-1)
	   SELECT @name = 'DECLARE @TVP ' + @TableTpeName + char(13) + char(10) + 'INSERT @TVP '+ char(13) + char(10) + @name
	   SELECT @name 
```

The output of the code above will be the following

```SQL
DECLARE @SomeId int = 0
DECLARE @SomeOtherId int = 0
DECLARE @SomeDate datetime = '20131210'
DECLARE @SOmeValue varchar(100) = 'Bla'


DECLARE @TVP MyCustomType
INSERT @TVP 
SELECT @SomeId, @SomeOtherId, @SomeDate, @SOmeValue

```
