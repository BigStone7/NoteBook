MySQL系统变量(system variables)实际上是一些系统参数，用于初始化或设定数据库对系统资源的占用，文件存放位置等，我们可以通过·=`shows variables like`

慢查询日志的开启：

```sql
mysql> show variables like 'slow_query_log';

+----------------+-------+
| Variable_name  | Value |
+----------------+-------+
| slow_query_log | ON    |
+----------------+-------+
1 row in set, 1 warning (0.01 sec)
```

