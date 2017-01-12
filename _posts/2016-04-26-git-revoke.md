---
layout: post
title: git 撤销
categories: git
---


### 参考  

>[git 撤销](https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-%E6%92%A4%E6%B6%88%E6%93%8D%E4%BD%9C)


### 撤销追踪某个文件  

{% highlight bash %}
git rm --cached <file_name>
# 再把此文件记录到 .gitignore 文件里面
{% endhighlight %}

### 重写提交信息  

当执行git commit 提交完成之后，发现有些文件没有添加，或者提交信息写错了。<br>
此时可以执行 git commit --amend 重新提交。<br>
比如，提交后忘记了暂存某些需要的修改<br>

{% highlight bash %}
git commit -m "fixed the bug_110"
# 发现有些修改没有提交
git add fogotton_changes
# 发现提交说明写错了
git commit --amend -m "fix the issue_110"
{% endhighlight %}

--amend 选项只是对上一次提交的修改，并不会新建提交快照

### 撤销暂存的文件  

{% highlight bash %}
git reset HEAD <file_name>
{% endhighlight %}


### 撤销工作区文件的修改  

{% highlight bash %}
# 撤销工作区的修改
git checkout -- <file_name>
# 回到上一个提交的版本
git checkout <file_name>
{% endhighlight %}