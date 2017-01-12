---
layout: post
title: git的文件状态
categories: git
---

###  参考  

> [git-book](https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-%E8%AE%B0%E5%BD%95%E6%AF%8F%E6%AC%A1%E6%9B%B4%E6%96%B0%E5%88%B0%E4%BB%93%E5%BA%93)

### 文件状态  

工作目录下的文件不外乎有两种文件状态 ： 已跟踪和未跟踪<br>
已跟踪的文件是指哪些已经被纳入版本控制的文件，即在上一次的快照中有它们的记录，在工作一段时间之后他们的状态可能处于未修改，已修改，已放入暂存区。工作目录中除了已跟踪的文件其他都属于未跟踪文件，他们既没有在上一次的快照中，也没有在暂存区中。


结构图<br>
![](http://itufei.oss-cn-hangzhou.aliyuncs.com/git-file-status.png?id=1)<br>


文件状态变化周期<br>

![文件的状态变化周期](http://itufei.oss-cn-hangzhou.aliyuncs.com/lifecycle.png)


### 查看文件状态  


{% highlight bash %}
git status -s
{% endhighlight %}


新添加未跟踪的文件前面有 ?? 标记<br>
新添加到暂存区的文件 前面有 A 标记 <br>
修改过的文件前面有 M 标记。 M 有两个可以出现的位置，左边的M表示修改了并存放进了暂存区，右边的M表示修改了 还没有放入暂存区里面<br>


### 跟踪新文件  


{% highlight bash %}
# 把新文件加入到暂存区 如果是目录就递归目录下的所有文件
git add <file_name | directory>
{% endhighlight %}

### 忽略文件  

当有些文件不需要git管理，比如日志文件 ， 临时文件 ， 库文件等 ，创建 .gitignore 文件来忽略

{% highlight bash %}
# .gitignore
vendor/
logs/*.log
node_modules/
docs/**/*.pdf
{% endhighlight %}

### 提交更新  

{% highlight bash %}
git commit -m "msg"
{% endhighlight %}

提交只是对暂存区快照的提交，任何还未被暂存仍然保持修改状态的文件不会被提交。每次运行提交操作，都是对你的项目做一次快照，以后可以回到这个状态。


### 移除文件  

删除文件的两种操作： 
1. 从工作目录中手工删除文件 ， 然后 执行 git rm `<file_name>` 记录此次文件移除的操作
2. 直接执行 git rm 命令，如果在删除之前文件已经被修改且被提交到暂存区，需要进行强制删除，git rm -f `<file_name>`, 
另外 如果你不小心把不希望被git追踪的文件 提交到了暂存区，你可以使用 git rm --cached `<file_name>` 来移除暂存区，此时并不会在工作区把文件删除，然后再把此文件放到.gitignore 文件里面。


### 移动文件  

{% highlight bash %}
git mv file.php file.java # 重命名
git mv file.php dir/a/b/ # 移动
{% endhighlight %}

{% highlight bash %}
# git mv 相当于运行了下面三条命令
mv file.php file.java
git rm file.php
git add file.java
{% endhighlight %}




