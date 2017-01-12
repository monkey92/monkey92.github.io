---
layout: post
title: git 远程分支
categories: git
---

### 参考  

> [git-远程分支](https://git-scm.com/book/zh/v2/Git-%E5%88%86%E6%94%AF-%E8%BF%9C%E7%A8%8B%E5%88%86%E6%94%AF)

### 远程跟踪分支（名词）  

远程跟踪分支 是 **远程分支状态引用**，是你不能移动 的 **本地引用**。当进行网络操作时他们会自动移动。<br>
远程跟踪分支 记录的是你上次连接到远程仓库时分支的状态。

{% highlight bash %}
# 查看所有分支
git branch -a
1.1
learn
* master
remotes/origin/1.0 # 远程跟踪分支
remotes/origin/1.1 # 远程跟踪分支
remotes/origin/HEAD -> origin/1.1 # 远程跟踪分支
remotes/origin/master # 远程跟踪分支
#查看本地分支与远程跟踪分支的对应关系
git branch -vv
1.1 3ac822d [origin/1.1] fixes #5099
learn 3ac822d #5099
* master 06c4562 [origin/master] Update json-schema & other deps, fixes #5374
{% endhighlight %}

### 远程操作命令  

{% highlight bash %}
#1.从远程主机抓取本地没有的数据，更新本地数据库
#2.移动本地远程跟踪分支与远程库保持一次
git fetch <origin_host_name>
# 与当前分支合并
git merge origin/master
#推送本地分支到远程 如果远程没有就创建
git push origin master:master
#删除远程分支
git push origin --delete <branch_name>
{% endhighlight %}

### 跟踪分支 (名词)  

特别注意的是当你抓取新的远程跟踪分支的时候，本地并不会生成一份可编辑的副本，也就是说不会有一个新的本地分支与远程跟踪分支相关联。
{% highlight bash %}
#创建本地分支并与远程分支相关联 此时创建的本地分支叫做跟踪分支
git checkout -b <local_branch_name> <origin_branch_name>
{% endhighlight %}










