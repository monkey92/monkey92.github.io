---
layout: post
title: git 分支
categories: git
---

### 参考  

> [git分支](https://git-scm.com/book/zh/v2/Git-%E5%88%86%E6%94%AF-%E5%88%86%E6%94%AF%E7%AE%80%E4%BB%8B)

### 分支简介  

在进行提交操作时，git会保存一个提交对象(commit object)。该提交对象包含一个指向暂存内容快照的指针，作者的姓名，邮箱，提交信息，以及指向它父提交的之指针。首次提交产生的提交对象没有父对象，多个分支合并产生的提交对象有多个父对象。<br>


{% highlight bash %}
git add README test.rb LICENSE
git commit -m "init project"
{% endhighlight %}

现在 git 库中有5个对象： 3个 blob 对象(保存文件快照) 1个树对象(记录目录结构 和 blob 索引)<br>
和一个提交对象(记录树对像与提交信息)

![](http://itufei.oss-cn-hangzhou.aliyuncs.com/commit-and-tree.png)

<br>修改后再提交的变化

![](http://itufei.oss-cn-hangzhou.aliyuncs.com/commits-and-parents.png)

**git的分支，本质上仅仅是指向提交对象的可变指针。**<br>

分支及其提交历史:<br>
![](http://itufei.oss-cn-hangzhou.aliyuncs.com/branch-and-history.png)


### 分支操作  

{% highlight bash %}
# 查看分支
git branch
# 查看分支所指向的提交对象
git branch -v
# 创建分支
git branch testing
# 切换分支
git checkout testing
# 创建并切换分支
git checkout -b testing
# 查看哪些分支与当前分支已经合并
git branch --merged
# 查看哪些分支与当前分支没有合并
git branch --no-merged
# 删除分支
git branch -d <branch_name> # 已经合并过的分支
git branch -D <branch_name> # 没有合并的分支强制删除
{% endhighlight %}


新的分支会在当前的提交对象上创建一个指针<br>
![](http://itufei.oss-cn-hangzhou.aliyuncs.com/two-branches.png)


<br>git通过名为HEAD的特殊指针来判断当前在哪一个分支上
<br> 通过 git log 可以查看各个分支当前所指向的提交对象
{% highlight bash %}
git log --oneline --decorate
f30ab (HEAD, master, testing) add feature #32 - ability to add new
{% endhighlight %}

项目分叉历史:<br>
![](http://itufei.oss-cn-hangzhou.aliyuncs.com/advance-master.png)
