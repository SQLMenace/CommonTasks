Just run this

```SQL
CREATE TABLE #test(Id tinyint,SomeDate date, Charge decimal(20,10))

insert #test
SELECT 1,'20120101',1000
UNION ALL
SELECT 1,'20120401',200
UNION ALL
SELECT 1,'20120501',300
UNION ALL
SELECT 1,'20120601',600
UNION ALL
SELECT 2,'20120101',100
UNION ALL
SELECT 2,'20130101',500
UNION ALL
SELECT 2,'20140101',-800
UNION ALL
SELECT 3,'20120101',100




SELECT id, someDate as StartDate,
LEAD(dateadd(dd,-1,SomeDate),1,'99991231') 
 OVER (PARTITION BY id ORDER BY SomeDate) as Enddate,
  Charge,
  SUM(Charge) OVER (PARTITION BY id ORDER BY SomeDate 
     ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
          AS RunningTotal
  FROM #test
  ORDER BY id, SomeDate
```
In the table

```
Id	SomeDate	Charge
1	2012-01-01	1000.0000000000
1	2012-04-01	200.0000000000
1	2012-05-01	300.0000000000
1	2012-06-01	600.0000000000
2	2012-01-01	100.0000000000
2	2013-01-01	500.0000000000
2	2014-01-01	-800.0000000000
3	2012-01-01	100.0000000000
```


Output from SQl Query
```
id	StartDate	Enddate	Charge	RunningTotal
1	2012-01-01	2012-03-31	1000.0000000000	1000.0000000000
1	2012-04-01	2012-04-30	200.0000000000	1200.0000000000
1	2012-05-01	2012-05-31	300.0000000000	1500.0000000000
1	2012-06-01	9999-12-31	600.0000000000	2100.0000000000
2	2012-01-01	2012-12-31	100.0000000000	100.0000000000
2	2013-01-01	2013-12-31	500.0000000000	600.0000000000
2	2014-01-01	9999-12-31	-800.0000000000	-200.0000000000
3	2012-01-01	9999-12-31	100.0000000000	100.0000000000
```

Explained here [Easy running totals with windowing functions](http://sqlservercode.blogspot.com/2016/03/easy-running-totals-with-windowing.html)
