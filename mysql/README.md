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
