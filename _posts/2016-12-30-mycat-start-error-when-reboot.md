---
layout: post
title: Mycat开机启动失败
categories: mycat
---

### 问题描述  

把mycat的启动命令放到/etc/rc.local里面,开机,重启都不会有  
mycat 的进程,一开始以为rc.local没有执行，然而再加一条其他命令  
其他命令却执行了，所以还是Mycat启动失败了。  
查看mycat日志，wrapper.log ,一看吓一跳  

{% highlight bash %}

Launching a JVM...
Unable to start JVM: No such file or directory (2)
JVM exited while loading the application.

{% endhighlight %}

居然是jvm启动失败...  

搜了下问题  [Stackoverflow上的](http://stackoverflow.com/questions/29355815/error-in-sonar-startup-unable-to-start-jvm-no-such-file-or-directory-2)  

### 解决办法  

wrapper的配置问题  

修改 $MYCAT_HOME/conf/wrapper.conf  
{% highlight bash %}
# 配置java的绝对路径
wrapper.java.command=/usr/local/java/bin/java
{% endhighlight %}




