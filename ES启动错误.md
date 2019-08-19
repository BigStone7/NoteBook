Docker是基于Linux容器（LXC）等技术发展起来的一项轻量级的操作系统虚拟化解决方案，类似于虚拟机一般。用户利用docker技术可以快速的的实现服务的部署、扩容、管理等工作。

### 准备

* 参考文档：https://docs.docker.com/
* 操作系统：centOS 7.6

### docker的安装

安装文档：https://docs.docker.com/install/linux/docker-ce/centos/

1. 卸载旧的docker版本

   ```shell
   sudo yum remove docker \
                   docker-client \
                   docker-client-latest \
                   docker-common \
                   docker-latest \
                   docker-latest-logrotate \
                   docker-logrotate \
                   docker-engine
   ```

   

2. 更新系统

   ```shell
   sudo yum update
   ```

3. 设置仓库