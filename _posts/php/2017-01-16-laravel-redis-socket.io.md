---
layout: post
title: laravel实现浏览器与服务器的时时通信
categories: php
---


### 依托的技术  

> redis + socket.io + nodejs  


### 思路  

业务代码还是用php来写，主要利用redis的pub功能。 把服务器端更新频繁的数据pub到redis服务里面。  
浏览器与服务器的时时通信，依然需要socket.io建立连接，socket.io的server还是用nodejs版的实现，
[参考代码在这里](https://github.com/monkey92/nodejs-redis-socketio-demo)。  
nodejs端的redis主要负责sub,并且响应到sub之后把数据把数据emit到浏览器，浏览器进行dom修改就可以显示时时数据。  
浏览器端的socket.io如果想要pub数据，可以通过ajax请求laravel并交由laravel的队列让laravel来pub。[DEMO地址](https://github.com/monkey92/laravel-redis-socketio-demo/blob/master/resources/views/chat.blade.php) 

### 示意图  

<img src="/assets/img/php/php-socket.io.png" alt="">