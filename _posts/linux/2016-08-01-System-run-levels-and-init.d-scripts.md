---
layout: post
title: ubuntu系统的运行级别和启动脚本
categories: linux
---


##  参考 

> http://www.debian.org/doc/debian-policy/ch-opersys.html#s-sysvinit  

## 关于运行级别  
	
Table 1. Mapping between runlevels and systemd targets  

| Runlevel | Target |
|----------|:---------------:|
|0|poweroff.target|
|1|rescue.target|
|2,3,4|multi-user.target|
|5|graphical.target|
|6|reboot.target|


##  部分翻译  

### 理解  

/etc/init.d 目录下存放所有的开机启动脚本，被/etc/rcn.d/ 目录下的脚本引用。  
/etc/rcn.d 目录下的脚本命名规则为 Kmmscript  Smmscript  
K stop   
S start  
mm 两个10进制数，越小启动优先级越高  
script  脚本名称  

比如从runlevel2 切换到 runlevel3 ,首先会执行rc3.d 下的所有K 开头的脚本，并传入stop参数。  
然后执行 S 开头的脚本 并传入start 参数。

但是对于runlevel0 和 runlevel6 这两个运行级别，以K S 开头的脚本都会执行，都会传入单个stop参数。






