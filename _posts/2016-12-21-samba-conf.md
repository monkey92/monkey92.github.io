---
layout: post
title: samba 配置
categories: linux
---

# samba配置多个共享目录

{% highlight bash %}
[www]
    comment=www
    path=/var/www
    writable=yes
[share]
    comment=share
    path=/home/deng/share
    writable=yes
[projects]
    comment=projects
    path=/home/deng/projects
    writable=yes
{% endhighlight %}


# 配置用户

比如你想在windows上让www-data用户来访问共享，并且在windows上创建的文件都是以www-data身份创建的，那么
你就需要在samba里为www-data用户配置密码。特别的，你共享的目录对www-data用户也要有可写权限。  

{% highlight bash %}
# 添加samba用户
smbpassword -a www-data
# 会提示设置密码
{% endhighlight %}

