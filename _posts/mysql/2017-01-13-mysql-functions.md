---
layout: post
title: mysql常用函数整理
categories: mysql
---

### 字符串函数  

<table class="table table-hover table-striped table-bordered">
	
	<tr>
		<td>concat(col_1,col_2,...)</td>
		<td>连接字符串,如果一个参数是null返回结果是null</td>
	</tr>
	<tr>
		<td>concat_ws(separator,col_1,col_2,...])</td>
		<td>连接字符串,并用separator分割，跳过值为null列，如果separator是null返回结果是null</td>
	</tr>
	<tr>
		<td>instr(str,substr)</td>
		<td>查询子串在str中出现的位置,没有返回0</td>
	</tr>
	<tr>
		<td>left(str,len)</td>
		<td>从左边截取len长度的字符</td>
	</tr>

</table>


### 数学函数  

<table class="table table-hover table-striped table-bordered">
	
	<tr>
		<td>floor(n)</td>
		<td>向下取整</td>
	</tr>
	<tr>
		<td>rand()</td>
		<td>返回 [0,1)之间的随机数, eg: [5,7] floor(5 + rand() * 2)</td>
	</tr>
	<tr>
		<td>rand()</td>
		<td>可以用在随机排序上：select * from t order by rand();</td>
	</tr>

</table>


### 时间日期函数  


<table class="table table-hover table-striped table-bordered">
	
	<tr>
		<td>current_date()</td>
		<td>当前日期</td>
	</tr>
	<tr>
		<td>curre_time()</td>
		<td>当前时间</td>
	</tr>
	<tr>
		<td>current_timestamp()</td>
		<td>当前时间戳</td>
	</tr>
	<tr>
		<td>date_sub(d1,d2)</td>
		<td>d1 - d2 eg: 查看最近一个月的记录, select * from t where date_col >= date_sub(current_date(),interval 30 day); </td>
	</tr>
	<tr>
		<td>day(date_str)</td>
		<td>从date_str提取天</td>
	</tr>
	<tr>
		<td>month(date_str)</td>
		<td>从date_str提取月</td>
	</tr>
	<tr>
		<td>year(date_str)</td>
		<td>从date_str提取年</td>
	</tr>
</table>

