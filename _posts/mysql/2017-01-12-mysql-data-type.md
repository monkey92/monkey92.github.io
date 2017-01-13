---
layout: post
title: mysql数据类型整理
categories: mysql
---


## mysql数据类型整理  

### 数值类型 

**除bit类型的m表示m个bit位之外其他的int类型的m只影响zerofill属性**


|类型				|宽度														|
|bit[(m)]			| m个bit位 默认为1 只能存储0,1								|
|tinyint[(m)]		| 小整形 1个字节											|
|bool				| tinyint(1) 												|
|smallint[(m)]		| 两个字节													|
|int[(m)]			| 4个字节													|
|bigint[(m)]		| 8个字节													|
|decimal[(m[,d])]	| 字符存储的浮点数m是总位数,d是小数点后的位数				|
|float[(m,d)]		| 浮点数													|
|double[(m,d)]		| 浮点数													|


### 日期和时间类型

**fsp 是微妙部分的长度默认是0**  

|类型				|宽度														|
|date				| 1000-01-01 to 9999-12-31									|
|datetime[(fsp)]	| 1000-01-01 00:00:00.000000 to 9999-12-31 23:59:59.999999	|
|timestamp[(fsp)]	| 1970-01-01 00:00:01.000000 to 2038-01-19 03:14:07.999999 	|
|time				| HH:MM:SS[.fsp] 											|
|year				| 1901 to 2155 and 0000										|


### 字符串类型  

|类型				|宽度														|
|char[(m)]			| m取值 from 0 to 255	default 1							|
|varchar(m)			| m取值 from 0 to 65535										|
|text[(m)]			| 可存储65535个单字节字符								 	|
|longtext			| 可存储4GB个单字节字符										|



