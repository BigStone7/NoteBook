### MySQL Variables

MySQL Variables在这里实际上指的是一些参数，用于初始化或设定数据库对系统资源的占用，文件存放位置等。在新安装好系统后，就已经被初始化好了。但是我们有时候不想采取默认值，所以就需要对这些值做出改变。

####  MySQL的变量分为两种：

* **系统变量：**配置MySQL服务器的运行环境，可以用show variables查看

  按其作用域的不同可以分为以下两种：

  * **分为全局（GLOBAL）级**：对整个MySQL服务器有效

  * **会话（SESSION或LOCAL）级**：只影响当前会话

    有些变量同时拥有以上两个级别，MySQL将在建立连接时用全局级变量初始化会话级变量，但一旦连接建立之后，全局级变量的改变不会影响到会话级变量。

* **状态变量：**监控MySQL服务器的运行状态，可以用show status查看，不可以被修改。

#### 查看系统变量的值（show）

**查看方法一：** 系统变量存放在`performance_schema`数据库里的`GLOBAL_VARIABLES`和`SESSION_VARIABLES`表中，可以直接通过查看表的内容获得。

```sql
mysql> use performance_schema
Database changed

mysql> show tables like '%variables';
+-------------------------------------------+
| Tables_in_performance_schema (%variables) |
+-------------------------------------------+
| global_variables                          |
| persisted_variables                       |
| session_variables                         |
+-------------------------------------------+
3 rows in set (0.00 sec)
```

**查看方法二：**使用show variables语法

```sql
SHOW [GLOBAL | SESSION] VARIABLES [LIKE 'pattern' | WHERE expr]
```

* 精准查询：

  ```sql
  mysql> show variables like 'slow_query_log';
  
  +----------------+-------+
  | Variable_name  | Value |
  +----------------+-------+
  | slow_query_log | ON    |
  +----------------+-------+
  1 row in set, 1 warning (0.00 sec)
  ```

* 通配符查询（%）

  ```sql
  mysql> show variables like '%log';
  
  +----------------------------------+---------------------------+
  | Variable_name                    | Value                     |
  +----------------------------------+---------------------------+
  | back_log                         | 80                        |
  | general_log                      | OFF                       |
  | innodb_api_enable_binlog         | OFF                       |
  | log_statements_unsafe_for_binlog | ON                        |
  | relay_log                        | DESKTOP-Q8KGU39-relay-bin |
  | slow_query_log                   | ON                        |
  | sync_binlog                      | 1                         |
  | sync_relay_log                   | 10000                     |
  +----------------------------------+---------------------------+
  8 rows in set, 1 warning (0.00 sec)
  ```

* 单个字符匹配查询（ _ )

  ```sql
  mysql> show variables like 'log_b__';
  
  +---------------+-------+
  | Variable_name | Value |
  +---------------+-------+
  | log_bin       | ON    |
  +---------------+-------+
  1 row in set, 1 warning (0.01 sec)
  ```

* where 语句查询（语法参看sql where 语句）

  ```sql
  
  mysql> show variables where variable_name = 'version';
  
  +---------------+--------+
  | Variable_name | Value  |
  +---------------+--------+
  | version       | 8.0.13 |
  +---------------+--------+
  1 row in set, 1 warning (0.00 sec)
  
  mysql> show variables where value like '8.%';
  +----------------+--------+
  | Variable_name  | Value  |
  +----------------+--------+
  | innodb_version | 8.0.13 |
  | version        | 8.0.13 |
  +----------------+--------+
  2 rows in set, 1 warning (0.00 sec)
  ```

#### 修改系统变量的值

修改变量值的语法：

```sql
set [GLOBAL | SESSION] 需要设置的变量
```

```sql
mysql> set global  log_queries_not_using_indexes=ON;

Query OK, 0 rows affected (0.00 sec)
```

还有另外的一种写法：@@

```sql
mysql> set  @@global.log_queries_not_using_indexes=ON;

Query OK, 0 rows affected (0.00 sec)
```

@: 代表是用户变量

@@：代表系统变量

***

**END**