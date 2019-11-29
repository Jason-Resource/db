```sql
# 获取30天前的日期 - 2019-10-31
SELECT DATE_SUB(CURDATE(), INTERVAL 29 DAY) 

# 获取创建时间是30天前的档案数据
SELECT
	* 
FROM
	crm_record 
WHERE
	create_time < DATE_SUB( CURDATE(), INTERVAL 29 DAY )
```
----

```sql
# 必须要括号括起来，再查一次，才能关联其他表（把结果集转为中间表）
select temp.* from (
		select record.id,record.member_id,record.city from crm_record as record where member_id in (select a.member_id from 
		(select member_id,max(create_time) max from crm_reply where member_id in (SELECT member_id FROM `crm_record` where status in (0,1,2)) and department_id=22 and member_id>0
		GROUP BY member_id order by create_time desc) a where a.max<DATE_SUB(CURDATE(), INTERVAL 29 DAY) )
) temp

LEFT JOIN crm_contract as contract on contract.member_id=temp.member_id
```
----

```sql
# 获取 当前日期、当前日期的周一的日期、当前日期的周日的日期
select curdate(), date_sub(curdate(),interval WEEKDAY(curdate()) day) as first, date_sub(curdate(),interval WEEKDAY(curdate()) -6 day) as end;

#当年第一天：
SELECT DATE_SUB(CURDATE(),INTERVAL dayofyear(now())-1 DAY);

#当年最后一天：
SELECT concat(YEAR(now()),'-12-31');  

#当前week的第一天：  
select date_sub(curdate(),INTERVAL WEEKDAY(curdate()) + 1 DAY);

#当前week的最后一天：  
select date_sub(curdate(),INTERVAL WEEKDAY(curdate()) - 5 DAY);

#前一week的第一天：  
select date_sub(curdate(),INTERVAL WEEKDAY(curdate()) + 8 DAY);

#前一week的最后一天：  
select date_sub(curdate(),INTERVAL WEEKDAY(curdate()) + 2 DAY);

#前两week的第一天：  
select date_sub(curdate(),INTERVAL WEEKDAY(curdate()) + 15 DAY);

#前两week的最后一天：  
select date_sub(curdate(),INTERVAL WEEKDAY(curdate()) + 9 DAY);

#当前month的第一天：  
SELECT concat(date_format(LAST_DAY(now()),'%Y-%m-'),'01');

#当前month的最后一天：  
SELECT  LAST_DAY(now());

#前一month的第一天：  
SELECT concat(date_format(LAST_DAY(now() - interval 1 month),'%Y-%m-'),'01');

#前一month的最后一天：  
SELECT LAST_DAY(now() - interval 1 month);

#前两month的第一天：  
SELECT concat(date_format(LAST_DAY(now() - interval 2 month),'%Y-%m-'),'01');

#前两month的最后一天：  
SELECT  LAST_DAY(now() - interval 2 month);

#当前quarter的第一天：  
select concat(date_format(LAST_DAY(MAKEDATE(EXTRACT(YEAR FROM  CURDATE()),1) + interval QUARTER(CURDATE())*3-3 month),'%Y-%m-'),'01'); 

#当前quarter的最后一天：  
select LAST_DAY(MAKEDATE(EXTRACT(YEAR  FROM CURDATE()),1) + interval QUARTER(CURDATE())*3-1 month);

#前一quarter的第一天：  
select concat(date_format(LAST_DAY(MAKEDATE(EXTRACT(YEAR FROM CURDATE()),1) + interval QUARTER(CURDATE())*3-6 month),'%Y-%m-'),'01');

#前一quarter的最后一天：  
select  LAST_DAY(MAKEDATE(EXTRACT(YEAR FROM CURDATE()),1) + interval QUARTER(CURDATE())*3-4 month);

#前两quarter的第一天：  
select concat(date_format(LAST_DAY(MAKEDATE(EXTRACT(YEAR FROM CURDATE()),1) + interval QUARTER(CURDATE())*3-9 month),'%Y-%m-'),'01');

#前两quarter的最后一天：  
select LAST_DAY(MAKEDATE(EXTRACT(YEAR FROM CURDATE()),1) + interval QUARTER(CURDATE())*3-7 month);

```

----

```sql
select DATE_FORMAT(NOW(),'%Y%m%d%H%i%s')

按 年周 筛选
DATE_FORMAT(created_at,'%x%v')
%x	年，其中的星期一是周的第一天，4 位，与 %v 使用
%v	周 (01-53) 星期一是一周的第一天，与 %x 使用

# 分组统计
SELECT DATE_FORMAT(`created_at`, '%Y-%m-%d') `days`,count(id) `count` FROM pf_monitor_data  
where created_at<:end_time GROUP BY `days`

# begin_time 是时间戳，先转
SELECT DATE_FORMAT(FROM_UNIXTIME(`begin_time`,'%Y-%m-%D %h:%i:%s'), '%Y%u') `days`,count(id) `count` FROM statistics_access 
```
