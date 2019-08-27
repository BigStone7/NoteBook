## DDL

数据定义语言，定义了数据库的结构和数据表的结构。

####  对数据库定义

* 添加数据库

```sql
CREATE DATABASE database_name;
```

* 删除数据库

```sql
DROP DATABASE database_name;
```

#### 对数据表定义

* 创建数据表

```sql
CREATE TABLE table_name;
```

* 创建表结构

```sql
CREATE TABLE table_name (
	字段名 类型 约束条件
);
```

样例：

```sql
DROP TABLE IF EXISTS 'users';
CREATE TABLE 'users' (
	'id' int(11) NOT NULL AUTO_INCREMENT,
    'name' char(255) NOT NULL,
);
```

* 修改表的结构

```SQL
/*加字段*/
ALTER TABLE table_name ADD (字段名 类型）;
/*修改字段*/
ALTER TABLE table_name RENAME COLUMN old_field_name TO new_field_name;
/*修改数据类型*/
ALTER TABLE table_name MODIFY (field_name type);
/*删除字段*/
ALTER TABLE table_name DROP COLUMN field_name
```

#### 数据表常见约束

* 主键约束

  一条记录的唯一标识，不能重复，不能为空

* 外键约束

  表与表之间引用的完整性。

* 唯一约束

* 非空约束

* DEFAULT 

* CHECK

distinct