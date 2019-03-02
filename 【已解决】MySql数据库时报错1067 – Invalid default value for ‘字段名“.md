### 【已解决】MySql数据库时报错1067 – Invalid default value for ‘字段名“

最近对MySQL数据库做了升级，升级到版本8，再去导入以前转储的sql文件时，出现以下错误：

```sql
1067 – Invalid default value for ‘字段名“
```

最后查阅了相关文档，发现是MySQL的严格模式导致的问题。

**解决方法：**

1. **临时修改：**

   进入MySQL数据库，修改`session` 下的`sql_mode`

   ```
   mysql> set session
       -> sql_mode='ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION';
   
   ```

2. **永久修改：**

   在文件 `/etc/mysql/mysql.conf.d/mysqld.cnf`中添加下面的内容：

   ```sql
   sql_mode='ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION';
   ```

   结果如图

![1550672647785](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\1550672647785.png)

**保存后重启mysql**

```shell
sudo service mysql restart
```

***

**分享时最好的学习！**

