---
layout: post
title: failed to start lsb start and stop mysql
categories: mysql
---

# failed to start lsb start and stop mysql

使用 sudo service mysqld start 开启mysql服务失败  
使用 systemctl status mysql.service 查看到 failed to start lsb start and stop mysql 这个错误  

主意这个错误只是告诉你MySQL服务启动失败，但是并没有告诉你为什么失败了。  
搜素这个错误的原因的得到的解决办法可能并不是正真的问题。

# 解决

直接找到 mysqld 的可执行文件， 去执行它 ， 可能会把具体的错误打印在终端。