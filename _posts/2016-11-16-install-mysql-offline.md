---
layout: post
title: ubuntu16.04 离线安装 mysql5.7
categories: mysql
---

# 版本
OS: ubuntu16.04  
mysql: 5.7 (二进制安装包mysql-5.7.16-linux-glibc2.5-x86_64.tar.gz)

# 参考
[mysql5.7 手册](http://dev.mysql.com/doc/refman/5.7/en/binary-installation.html)

# 安装步骤以及遇到的问题

## 环境依赖

mysql 依赖libaio 的库.  

{% highlight bash %}
    sudo apt-get intall libaio1
{% endhighlight %}

如果系统没有联网，可以下载libaio的包进行安装。  
[下载地址](https://launchpad.net/ubuntu/+source/libaio)   

{% highlight bash %}
    sudo dpkg -i path/to/libaio.deb
{% endhighlight %}

## 解压安装包

{% highlight bash %}
    # 解压到 /usr/local 下面
    sudo tar -zxvf path/to/mysql-5.7.16-linux-glibc2.5-x86_64.tar.gz -C /usr/local
{% endhighlight %}


## 安装涉及的相关命令

{% highlight bash %}
    sudo groupadd mysql
    sudo useradd -r -g mysql -s /bin/false mysql
    cd /usr/local
    # 创建软连接指向全路径方便管理
    sudo ln -s mysql-5.7.16-linux-glibc2.5-x86_64 mysql
    cd mysql
    sudo mkdir mysql-files
    sudo chown -R mysql .
    sudo chgrp -R mysql .
    # 初始化数据目录
    sudo bin/mysqld --initialize --user=mysql 
    sudo bin/mysql_ssl_rsa_setup
    sudo chown -R root .
    sudo chown -R mysql data mysql-files
{% endhighlight %}


## mysql 配置
复制 support-files 目录下的 my-default.cnf 到 /etc/my.cnf  
下面的配置只是一部分  
{% highlight bash %}
    [client]
    socket=/var/run/mysqld/mysqld.sock

    [mysqld]
    user		= mysql
    basedir 	= /usr/local/mysql
    datadir 	= /usr/local/mysql/data
    port 		= 3306
    pid-file	= /var/run/mysqld/mysqld.pid
    socket		= /var/run/mysqld/mysqld.sock

    log_error	= /var/log/mysql/error.log

    sql_mode=NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES 

    default-time_zone = '+8:00'

{% endhighlight %}

## 注册mysql启动服务到系统的开机启动服务
复制 support-files 目录下的 mysql.server 到 /etc/init.d/mysqld  
执行
{% highlight bash %}
  sudo update-rc.d -f mysqld defaults  
{% endhighlight %}


## 开启mysql 服务

{% highlight bash %}
  sudo service mysqld start 
{% endhighlight %}

## 关闭mysql 服务

{% highlight bash %}
  sudo service mysqld stop 
{% endhighlight %}


# 注意

1. 初始化数据目录的时候 会创建一个 root 的用户用来连接数据库，会生成一个随机的密码，注意查看。  
2. 使用随机密码连接数据库之后需要重置数据库密码。ALTER USER 'root'@'localhost' IDENTIFIED BY 'new_password';







