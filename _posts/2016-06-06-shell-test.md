---
layout: post
title: shell 的比较与测试总结
categories: linux
---

## shell 的比较与测试  

### 1.算数比较  

* 等于 -eq
* 不等于 -ne
* 大于 -gt
* 小于 -lt
* 大于等于 -ge
* 小于等于 -le

对于算数比较可以按照下面的方法结合多个条件进行测试:  
[ $var1 -ne 0 -a $var2 -gt 2 ] #使用逻辑与-a  
[ $var1 -ne 0 -o var2 -gt 2 ] #逻辑或 -o  


### 2.文件系统相关测试  

* [ -f $file_var ] 是否是文件
* [ -x $file ] 文件是否可执行
* [ -w $file ] 文件是否可写
* [ -r $file ] 文件是否可读
* [ -d $var ] 是否是目录
* [ -e $var ] 文件是否存在
* [ -L $var ] 是否是符号连接文件

### 字符串比较 使用双中括号  

* [[ $str1 = $str2 ]] 当$str1 等于 $str2 时候返回真 也可以使用 [[ $str1 == $str2 ]]
* [[ $str1 != $str2 ]] $str1 不等于 $str2
* [[ $str1 > $str2 ]] $str1 的字母顺序比$str2 大
* [[ $str1 < $str2 ]]
* [[ -z $str1 ]] $str1 包含的是空字符串
* [[ -n $str1 ]] $str1 包含的是非空字符串


**注意在 = 前后各有一个空格。如果忘记加空格,那就不是比较关系了,而变成了赋值语句**

无论对于字符串的比较还是算数比较都可以使用逻辑运算符 && 和 || 能够很容易地将多个条件组合起来:  
{% highlight bash %}
if [[ -n $str1 ]] && [[ -z $str2 ]] ;
then
commands;
fi
{% endhighlight %}









