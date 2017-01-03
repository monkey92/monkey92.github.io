---
layout: post
title: composer安装全局包
categories: php
---

###  场景  

当需要使用一些php的命令行工具时候，你可能需要多次添加环境变量来找到这些命令，但是如果这些命令行工具提供另composer的安装方式的话，一切都变的简单了～～～  

{% highlight bash %}
composer global require 'psy/psysh'
{% endhighlight %}

此命令会在 ~/.composer 或者 ~/.config/composer 下安装需要的包。  


### 修改环境变量  

{% highlight bash %}
export PATH=/home/your_name/.config/composer/vendor/bin:$PATH
{% endhighlight %}

### 删除全局包  

{% highlight bash %}
composer global remove 'psy/psysh'
{% endhighlight %}