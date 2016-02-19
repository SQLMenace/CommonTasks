Someone wanted to know if there was something like @@identity/scope_identity() for a uniqueidentifier column 
with a default of newsequentialid(). 
There is not such a function but you can use OUTPUT INSERTED.Column to do something similar

```SQL

CREATE TABLE bla(ID INT,SomeID UNIQUEIDENTIFIER DEFAULT newsequentialid())
 
```

Here is how you use OUTPUT INSERTED.Column

```SQL
INSERT bla (ID)
    OUTPUT INSERTED.SomeID
VALUES(2)
```

You can also dump it into a variable

```SQL
DECLARE @MyTableVar TABLE( SomeID UNIQUEIDENTIFIER)
INSERT bla (ID)
    OUTPUT INSERTED.SomeID
        INTO @MyTableVar
VALUES(3)
 
SELECT SomeID FROM @MyTableVar
```
