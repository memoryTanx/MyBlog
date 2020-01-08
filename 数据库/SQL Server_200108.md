SQL Server 日期和时间数据类型及函数 (Transact-SQL)


```
-- 返回包含计算机的日期和时间的 datetime 值，SQL Server 的实例在该计算机上运行 。 返回值不包括时区偏移量。
GETDATE ( )

-- 返回表示指定 date 的指定 datepart 的字符串 。
DATENAME ( datepart , date )

-- 返回两个指定日期之间所跨的日期或时间 datepart 边界数 。
DATEDIFF ( datepart , startdate , enddate )

-- 通过将一个时间间隔与指定 date 的指定 datepart 相加，返回一个新的 datetime 值 。
DATEADD (datepart , number , date )

-- 确定 datetime 或 smalldatetime 输入表达式是否为有效的日期或时间值 。
ISDATE ( expression )
```

例子
```
select convert(varchar(10),getdate(),120)  -- 只返回当前日期，且为2012-12-12格式（最有用）

datediff(day,createdate,GetDate())=0      -- 判断是否当天，createdate为日期字段

-- 1.一个月第一天的
Select DATEADD(mm, DATEDIFF(mm,0,getdate()), 0)

-- 2.本周的星期一
Select DATEADD(wk, DATEDIFF(wk,0,getdate()), 0)

-- 3.一年的第一天
Select DATEADD(yy, DATEDIFF(yy,0,getdate()), 0)

-- 4.季度的第一天
Select DATEADD(qq, DATEDIFF(qq,0,getdate()), 0)

-- 5.当天的半夜
Select DATEADD(dd, DATEDIFF(dd,0,getdate()), 0)

-- 6.上个月的最后一天
Select dateadd(ms,-3,DATEADD(mm, DATEDIFF(mm,0,getdate()), 0))

-- 7.去年的最后一天
Select dateadd(ms,-3,DATEADD(yy, DATEDIFF(yy,0,getdate()), 0))

-- 8.本月的最后一天
Select dateadd(ms,-3,DATEADD(mm, DATEDIFF(m,0,getdate())+1, 0))

-- 9.本年的最后一天
Select dateadd(ms,-3,DATEADD(yy, DATEDIFF(yy,0,getdate())+1, 0))

-- 10.本月的第一个星期一
select DATEADD(wk, DATEDIFF(wk,0,dateadd(dd,6-datepart(day,getdate()),getdate())), 0) 

select datename(week,getdate()) as '本年第多少周',
       datename(weekday,getdate()) as '今天是周几'

select 本年第多少周=datename(week,getdate())
      ,今天是周几=datename(weekday,getdate())

--  dateadd 在向指定日期加上一段时间的基础上，返回新的datetime值
-- 向日期加上2天 或 增加1个月
    select dateadd(day,2,'2004-10-15') --返回：2004-10-17 00:00:00.000
    select dateadd(month,2,'2004-10-15') --返回：2004-12-17 00:00:00.000

--3. datediff 返回跨两个指定日期的日期和时间边界数。
     select datediff(day,'2004-09-01','2004-09-18') --返回天数：17
     select DateDiff(s,'2005-07-20','2005-7-25 22:56:32') --返回值为 514592 秒
     select DateDiff(ms,'2005-07-20','2005-7-25 22:56:32') --返回值为 微秒
     select DateDiff(d,'2005-07-20','2005-7-25 22:56:32') -- 返回值为 5 天
     select DatePart(w,'2005-7-25 22:56:32')--返回值为 2 即星期一(周日为1，周六为7)
     select DatePart('d','2005-7-25 22:56:32')--返回值为 25即25号
     select DatePart('y','2005-7-25 22:56:32')--返回值为 206即这一年中第206天
     select DatePart('yyyy','2005-7-25 22:56:32')--返回值为 2005即2005年

--DateDiff (interval,date1,date2) 以interval 指定的方式，
--返回date2 与date1两个日期之间的差值 date2-date1
--DateAdd (interval,number,date) 以interval指定的方式，加上number之后的日期
--DatePart (interval,date) 返回日期date中，interval指定部分所对应的整数值
--DateName (interval,date) 返回日期date中，interval指定部分所对应的字符串名称

-- 返回当前日期和时间
   select GETDATE()

--  返回代表指定日期的指定日期部分的整数。
    select datepart(month, '2004-10-15') --返回 月
    select datepart(day, '2004-10-15') --返回 日
    select datepart(year, getdate()) --返回 年
    select convert(varchar(8),getdate(),114)  -- 当前时间
    select datename(weekday, getdate()) --返回：星期五
    select datepart(weekday, getdate()) --返回：小写星期2-1
    select convert(varchar(10),getdate(),120)  -- 当前日期
    select datepart(S, '2004-10-15') --返回 月
--  返回时间到豪秒
    Select CONVERT(VARCHAR(30),GETDATE(),9)

--  获取当前日期，年、月、日、周、时、分、秒
    select GETDATE() as '当前日期',
    DateName(year,GetDate()) as '年',
    DateName(month,GetDate()) as '月',
    DateName(day,GetDate()) as '日',
    DateName(dw,GetDate()) as '星期',
    DateName(week,GetDate()) as '周数',
    DateName(hour,GetDate()) as '时',
    DateName(minute,GetDate()) as '分',
    DateName(second,GetDate()) as '秒'


print DateName(second,GetDate())

--  格式
select replace(replace(replace(CONVERT(varchar, getdate(), 120 ),'-',''),' ',''),':','')
20040912110608

select CONVERT(varchar(12) , getdate(), 111 )
2004/09/12

select CONVERT(varchar(12) , getdate(), 112 )
20040912

select CONVERT(varchar(12) , getdate(), 102 )
2004.09.12

select CONVERT(varchar(12) , getdate(), 101 )
09/12/2004

select CONVERT(varchar(12) , getdate(), 103 )
12/09/2004

select CONVERT(varchar(12) , getdate(), 104 )
12.09.2004

select CONVERT(varchar(12) , getdate(), 105 )
12-09-2004

select CONVERT(varchar(12) , getdate(), 106 )
12 09 2004

select CONVERT(varchar(12) , getdate(), 107 )
09 12, 2004

select CONVERT(varchar(12) , getdate(), 108 )
11:06:08

select CONVERT(varchar(12) , getdate(), 109 )
09 12 2004 1

select CONVERT(varchar(12) , getdate(), 110 )
09-12-2004

select CONVERT(varchar(12) , getdate(), 113 )
12 09 2004 1

select CONVERT(varchar(12) , getdate(), 114 )
11:06:08.177
 

-- 查询最近一个月内的点击率大于100的记录数据：
select * from t_business_product where hit_count>100 and datediff(Dd,last_date,getdate())<=30 order by id desc

-- 查询最近一周内的点击率大于100的记录数据：
select * from t_business_product where hit_count>100 and datediff(Dw,last_date,getdate())<=7 order by id desc

-- 你可以使用LIKE来返回正确的记录。通过在日期表达式中包含通配符“％”，
-- 你可以匹配一个特定日期的所有时间。这里有一个例子：
--这个语句可以匹配正确的记录。因为通配符“％”代表了任何时间。

Select * FROM weblog Where entrydate LIKE ‘Dec 25 2000%’
 

select @@version

```

————————————————

版权声明：本文为CSDN博主「敦厚的曹操」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。

原文链接：https://blog.csdn.net/dxnn520/article/details/8456653
