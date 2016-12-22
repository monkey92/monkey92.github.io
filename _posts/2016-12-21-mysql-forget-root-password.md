---
layout: post
title: mysql 忘记root密码
categories: mysql
---

# 版本
> mysql5.7

# mysql 忘记root密码

1. 跳过权限检查启动mysql服务  
在my.cnf 加入 skip-grant-tables 这一行  

2. 重启mysql服务， 再次登录不需要密码  

3. 修改密码  

{% highlight bash %}
update user set authentication_string=password('123456') where User='root' and Host='localhost';
{%  endhighlight %}

4. 注释掉 skip-grant-tables 这一行  

5. 重启mysql服务






