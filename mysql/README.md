```sql
select DATE_FORMAT(NOW(),'%Y%m%d%H%i%s')

# 分组统计
SELECT DATE_FORMAT(`created_at`, '%Y-%m-%d') `days`,count(id) `count` FROM pf_monitor_data  
where created_at<:end_time GROUP BY `days`

# begin_time 是时间戳，先转
SELECT DATE_FORMAT(FROM_UNIXTIME(`begin_time`,'%Y-%m-%D %h:%i:%s'), '%Y%u') `days`,count(id) `count` FROM statistics_access 
```
