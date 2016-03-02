
```SQL
declare @date date = '20160301' --getdate() - 10 -- your start range
declare @Enddate date = '20160310' --getdate()   -- your end range


;with cte as(
select *, ROW_NUMBER() over(order by Thedate) as row
from(
select dateadd(dd,number,@date) as Thedate from master..spt_values
where type = 'P'
and  dateadd(dd,number,@date) between @date and @Enddate
) x
where datepart(dw,Thedate) not in (1,7) --weekends in the US (SET DATEFIRST 7)
--and not exists( select 1 from YourHolidayTable -- this is your holiday table
--	where  x.Thedate = holidayDate )
)

SELECT ct1.Thedate, datediff(dd,ct1.Thedate,ct2.Thedate) as Diff 
FROM cte ct1 join cte ct2 on ct1.row = ct2.row + 1
```


Output
```
Thedate	Diff
2016-03-02	-1
2016-03-03	-1
2016-03-04	-1
2016-03-07	-3
2016-03-08	-1
2016-03-09	-1
2016-03-10	-1
```
