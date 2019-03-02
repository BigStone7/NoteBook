## 	【已解决】Error running 'xxx项目': Command line is too long. Shorten command line for xxx or also for Spring Boot default configuration.

根据错误信息可知，指令太过长，根据提示缩短指令即可。

在IDEA中找到 Run-> Edit Configurations打开：

![1550331311790](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\1550331311790.png)

在 Environment-> Shorten command line 的内容配置为 `JAR`即可解决：

![1550331679844](C:\Users\zhang\AppData\Roaming\Typora\typora-user-images\1550331679844.png)