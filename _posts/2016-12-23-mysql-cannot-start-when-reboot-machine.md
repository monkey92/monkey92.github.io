---
layout: post
title: mysql服务开机无法启动
categories: mysql
---

# 版本
> ubuntu16.04  
> mysql5.7 (二进制包手动安装)

# 日志记录

[ERROR] Could not create unix socket lock file /var/run/mysqld/mysqld.sock.lock

# 解决办法

{% highlight bash %}
cd /var/run/
sudo mkdir -m0755 mysqld
sudo chown mysql:mysql mysqld
sudo service mysqld start
{% endhighlight %}

# 注意

如果你的 /run 目录使用的是 tmpfs 文件系统的话(shell> df 查看)，在关机的时候，
你所创建的mysqld目录会消失，也就是说你重启的时候又会报这个错误。最好的办法是
在开机后 mysql服务启动前就需要创建mysqld目录

# 最佳方案

进入/etc/init.d/ 下查找mysql服务启动的脚本文件，我这里是mysqld 。也许你的不一样，
可以自定义名称的。 在脚本文件的开头加入创建目录的语句。  
{% highlight kbash %}
mkdir -p -m0755 /var/run/mysqld
chown mysql:mysql /var/run/mysqld
{% endhighlight %}

