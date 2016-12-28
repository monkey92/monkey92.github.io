---
layout: post
title: linux 杀死僵尸进程
categories: linux
---

{% highlight bash %}
ps -A -ostat,ppid,pid,cmd | grep -e '^[zZ]'
kill [ppid]
{% endhighlight %}