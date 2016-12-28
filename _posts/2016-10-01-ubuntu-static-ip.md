---
layout: post
title: ubuntu配置静态ip
categories: linux
---


## 修改 /etc/network/interfaces

{% highlight bash %}

source /etc/network/interfaces.d/*

# The loopback network interface
auto lo
iface lo inet loopback

# The primary network interface
auto enp0s3
iface enp0s3 inet static
address         192.168.0.111
gateway         192.168.0.1
netmask         255.255.255.0
netaddress      192.168.0.0
broadcast       192.168.0.255
dns-nameserver  211.138.24.66 211.138.30.66


{% endhighlight %}

## 重启网络服务  

sudo service networking restart