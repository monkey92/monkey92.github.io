---
layout: post
title: ubnutu16.04 php环境搭建
categories: linux php
---

# php7.0环境搭建

## 命令行安装

{% highlight bash %}
#主要安装
sudo apt-get install php7.0
#扩展安装
sudo apt-get install php7.0-mcrypt
sudo apt-get install php7.0-mysql
sudo apt-get install php7.0-curl
{% endhighlight %}

## 命名行安装之后的相关文件位置

### 执行命令:  
/usr/bin/php -> /etc/alternatives/php -> /usr/bin/php7.0  
/usr/bin/php7.0  
  
### 配置文件:
/etc/php/7.0/cli/php.ini  
/etc/php/7.0/fpm/php.ini
/etc/php/7.0/mods-available/*.ini  

### 扩展包位置:  
/usr/lib/php/20151012/  