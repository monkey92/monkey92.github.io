---
layout: post
title: mysql数据类型整理
categories: mysql
---


## mysql数据类型整理  

### 数值类型 

**除bit类型的m表示m个bit位之外其他的int类型的m只影响zerofill属性**


|类型				|宽度														|
|:--------------	|:----------------------------------------------------------|
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

