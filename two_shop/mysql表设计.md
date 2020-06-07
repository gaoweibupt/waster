## mysql表设计

### mysql的安装

#### 直接安装


**下载地址**
在该地址中查找操作系统 windows、macOS、linux对应的版本进行下载即可。
[https://dev.mysql.com/downloads/mysql/](
https://dev.mysql.com/downloads/mysql/)
需要先注册并登录oracle账户才可以下载。


**安装指南**
windows：<br/>
[https://www.mysql.com/cn/why-mysql/white-papers/visual-guide-to-installing-mysql-windows-zh/](https://www.mysql.com/cn/why-mysql/white-papers/visual-guide-to-installing-mysql-windows-zh/)
macOS：<br/>
[https://zhuanlan.zhihu.com/p/27960044](https://zhuanlan.zhihu.com/p/27960044)
linux:
在linux下安装mysql的方式比较多，有些操作系统自带了mysql；在linux下安装可以自行查找相关的博客，这里也给出来一个参考链接[https://www.runoob.com/mysql/mysql-install.html](https://www.runoob.com/mysql/mysql-install.html)。

#### docker
docker 是虚拟化容器技术，基于docker可以快速的构建标准化的运行环境。
这里就做docker的详细介绍了，可以参考如下链接进行安装。
[https://www.runoob.com/docker/docker-install-mysql.html](https://www.runoob.com/docker/docker-install-mysql.html)

执行如下命令就可以运行mysql:

```
docker run -d --name mysql -v ~/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=yanwu12138 -p 3306:3306 mysql:5.7
```

执行如下命令进入到docker容器中，并连接mysql:

```
docker exec -it mysql bash
root@ca0f4b520b81:/# mysql -h localhost -uroot -p123456
mysql>
```

### 创建数据表

```
mysql>create database payment;

mysql>use payment;

mysql> CREATE TABLE `product_order` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT,
  `uid` bigint(20) NOT NULL DEFAULT '0',
  `product_id` bigint(20) NOT NULL DEFAULT '0',
  `pay_amount` bigint(20) NOT NULL DEFAULT '0',
  `pay_status` tinyint(3) NOT NULL DEFAULT '0',
  `create_time` int(10) NOT NULL DEFAULT '0',
  `update_time` int(10) NOT NULL DEFAULT '0',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8;
```

两点注意:
1.默认值为零值，不要用null； null值对于索引是无效的
2.时间用时间戳表示:
* 不用考虑时区问题
* 计算方便，检索效率高
