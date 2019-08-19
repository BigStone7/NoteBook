### 1.创建新用户

```shell
adduser 用户名
```

### 2.初始化密码

```shell
passwd 用户名
```

```shell
New password:  #输入密码
Retype new password: #确认密码
passwd: all authentication tokens updated successfully.
```

### 3.用户授权

在centOS中，新创建的个人用户只有`home`文件下的权限，并且新用户是无法使用sudo命令。所以想要使用`root`权限的新用户必须进行授权。

对用户权限的修改可以通过对`/etc/sudoers`文件的修改实现。具体操作如下：

* 给`sudoers`文件授权，使其可读写。

  ```shell
  chmod -v u+w /etc/sudoers
  ```

* 修改`sudoers`文件，添加新用户

  ```shell
  ## Allow root to run any commands anywhere 
  root ALL=(ALL) ALL
  新用户名 ALL=(ALL) ALL 
  ```

  保存后退出！

#### 补充：

文件查找命令

```shell
whereis 文件名
```

```shell
# 例如查看sudoers文件位置
whereis sudoers

sudoers: /etc/sudoers /etc/sudoers.d /usr/share/man/man5/sudoers.5.gz
```

