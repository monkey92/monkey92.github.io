---
layout: post
title: mysql5.7主从复制
categories: mysql
---

# 版本  
mysql: 5.7

# 参考
[mysql5.7 手册](http://dev.mysql.com/doc/refman/5.7/en/replication.html)

# 笔记
## 基于二进制日志的主从复制
(1)修改 master 的配置并重启mysql  
{% highlight bash %}
    [mysqld]
    log-bin=/var/log/mysql/mysql-bin.log
    #server-id 必须唯一 范围 1-2^32-1
    server-id=1
{% endhighlight %}
(2)为 slave 创建单独连接master 的用户  
{% highlight bash %}
    mysql>create user 'slave'@'%' identified by 'my_p@55w0rd';
    mysql>grant replication slave on *.* to 'slave'@'%';
{% endhighlight %}
(3)同步master 与 slave 数据，在配置 slave 的时候 master 已经运行了一段时间，已经有了一些数据，这些数据是与slave不同步的，
如果想这些数据也copy到slave上，需要把msater的这些数据在开启slave之前就进行同步。  
{% highlight bash %}
    #禁止再写入数据
    mysql>flush tables with read lock;
    #使用mysqldump 备份数据 shell 下执行
    shell> mysqldump -uroot -p --databases mydb --master-data > mydb.sql
    # 解除锁定
    mysql>unlock tables;
{% endhighlight %}
(4)修改 slave 的配置并重启mysql
{% highlight bash %}
    [mysqld]
    server-id=2
{% endhighlight %}
(5)在 slave 上建立与master 的同步信息  
{% highlight bash %}
    mysql> change master to
        ->master_host='192.168.0.102',
        ->master_user='slave',
        ->master_pasword='my_p@55w0rd',
        ->master_log_file='mysql-bin.000001',
        ->master_log_pos=94;
    # master_log_file 与 master_log_pos 在master 上 执行 mysql>show master status; 查看
{% endhighlight %}
(6)把(3)获得的需要同步的数据 导入到 slave  
{% highlight bash %}
    shell>mysql -uroot -p123456 < mydb.sql
{% endhighlight %}
(7)开启slave
{% highlight bash %}
    mysql>start slave;
    # 查看同步状态
    mysql>show slave status;
{% endhighlight %}









