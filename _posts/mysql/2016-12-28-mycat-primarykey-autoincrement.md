---
layout: post
title: Mycat mysql自增长主键的配置
categories: mycat
---


# 版本 

> mycat1.6  
> ubuntu16.04  
> mysql5.7

# 参考 

> 分布式数据库架构及企业实践--基于mycat中间件  

# 使用数据库方式的sequence配置  

### 1.在随便一个数据节点上创建mycat_sequence表  

{% highlight bash %}
# sql语句
CREATE TABLE `mycat_sequence` (
  `name` varchar(50) COLLATE utf8_unicode_ci NOT NULL,
  `current_value` int(11) NOT NULL,
  `increment` int(11) NOT NULL DEFAULT '100',
  PRIMARY KEY (`name`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;
# 创建相关的函数

DELIMITER $$
CREATE FUNCTION `mycat_seq_currentval`(seq_name varchar(50)) 
RETURNS varchar(64) CHARSET utf8
DETERMINISTIC
BEGIN
declare retval varchar(64);
set retval="-999999999,null";
select concat(cast(current_value as char),",",cast(increment as char)) 
	into retval from mycat_sequence where name=seq_name;
RETURN retval;
END$$
DELIMITER ;

DELIMITER $$
CREATE  FUNCTION `mycat_seq_nextval`(seq_name varchar(50)) 
RETURNS varchar(64) CHARSET utf8
DETERMINISTIC
BEGIN
update mycat_sequence set current_value=current_value+increment
where name=seq_name;
RETURN mycat_seq_currentval(seq_name);
END$$
DELIMITER ;

DELIMITER $$
CREATE FUNCTION `mycat_seq_setval`(seq_name varchar(50), value integer) 
RETURNS varchar(64) CHARSET utf8
DETERMINISTIC
BEGIN
update mycat_sequence set current_value=value where name=seq_name;
RETURN mycat_seq_currentval(seq_name);
END$$
DELIMITER ;

{% endhighlight %}


### 2.插入数据  

比如你希望user表使用序列,可以这样插入  

{% highlight bash %}
mysql> insert into mycat_sequence(name,current_value,increment) values('USER',0,1);
{% endhighlight %}  

### 3.schema.xml的配置  

schema.xml 要配置mycat_sequence的逻辑表  

{% highlight bash %}
<table name="mycat_sequence" dataNode="节点名"></table>
{% endhighlight %} 


### 4.sequence_db_conf.properties 的配置  

USER=节点名


### 5.server.xml的配置  

{% highlight bash %}
 <property name="sequnceHandlerType">1</property>
{% endhighlight %} 

### 6.两个 auto increment

mysql创建表主键id 要配 auto_increment  
schema.xml 配置的逻辑表 autoIncrement="true"  


# 使用  


{% highlight bash %}
insert into user(id,name) values(next value for MYCATSEQ_USER,'Lilei');
{% endhighlight %}
