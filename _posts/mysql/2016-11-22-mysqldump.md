---
layout: post
title: mysqldump 的使用
categories: mysql
---

# 版本  
mysql: 5.7

# 参考
[mysql5.7 手册](http://dev.mysql.com/doc/refman/5.7/en/mysqldump.html)

# 笔记

{% highlight bash %}
    #dump所有数据
    shell> mysqldump -uuser_name -p -h 172.17.0.1 -P 3306 --all-databases > all.sql
    #dump指定的数据库
    shell> mysqldump -uuser_name -p -h 172.17.0.1 -P 3306 --databases db_1 db_2 > db_1&db_2.sql
    #dump指定表的数据
    shell> mysqldump -uuser_name -p -h 127.0.0.1 -P 8066 db_1 table_1 > table_1.sql
    #dump结果不增加 create table 语句
    shell> mysqldump -uuser_name -p -h 127.0.0.1 -P 8066 -t db_1 table_1 > table_1.sql
    #dump结果的insert 语句添加具体的字段名
    shell> mysqldump -uuser_name -p -h 127.0.0.1 -P 8066 -c db_1 table_1 > table_1.sql
    #dump复合条件的行
    shell> mysqldump -uuser_name -p -h 127.0.0.1 -P 8066 -t -c -w'id>10' db_1 table_1 > table_1.sql
{% endhighlight %}