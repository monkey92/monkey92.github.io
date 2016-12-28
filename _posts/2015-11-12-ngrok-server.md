---
layout: post
title: scp的使用
categories: linux
---


##  搭建自己的ngrok服务  

### 一、准备工作  

参考链接:     http://tonybai.com/2015/03/14/selfhost-ngrok-service/  

### 二、实操步骤

#### 1、搭建编译环境，下载ngrok源码  

安装go语言的环境  
下载go语言安装包    http://www.golangtc.com/download 设置好环境变量  

sudo apt-get install build-essential    mercurial   #这两个工具要先安装  
下载ngrok源码    git clone https://github.com/inconshreveable/ngrok.git

#### 2、生成自签名证书  

使用ngrok.com官方服务时，我们使用的是官方的SSL证书。自建ngrokd服务，我们需要生成自己的证书，并提供携带该证书的ngrok客户端。

我们这里以NGROK_BASE_DOMAIN="dev.airoa.cn"为例，生成证书的命令如下：

{% highlight bash %}

$ openssl genrsa -out rootCA.key 2048
$ openssl req -x509 -new -nodes -key rootCA.key -subj "/CN=dev.airoa.cn" -days 5000 -out rootCA.pem
$ openssl genrsa -out device.key 2048
$ openssl req -new -key device.key -subj "/CN=dev.airoa.cn" -out device.csr
$ openssl x509 -req -in device.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out device.crt -days 5000

# 执行完以上命令，在ngrok目录下就会新生成6个文件：

-rw-rw-r– 1 ubuntu ubuntu 1001 Mar 14 02:22 device.crt
-rw-rw-r– 1 ubuntu ubuntu  903 Mar 14 02:22 device.csr
-rw-rw-r– 1 ubuntu ubuntu 1679 Mar 14 02:22 device.key
-rw-rw-r– 1 ubuntu ubuntu 1679 Mar 14 02:21 rootCA.key
-rw-rw-r– 1 ubuntu ubuntu 1119 Mar 14 02:21 rootCA.pem
-rw-rw-r– 1 ubuntu ubuntu   17 Mar 14 02:22 rootCA.srl

# ngrok通过bindata将ngrok源码目录下的assets目录（资源文件）打包到可执行文件(ngrokd和ngrok)中 去，
# assets/client/tls和assets/server/tls下分别存放着用于ngrok和ngrokd的默认证书文件，
# 我们需要将它们替换成我们自己生成的：(因此这一步务必放在编译可执行文件之前)

cp rootCA.pem assets/client/tls/ngrokroot.crt
cp device.crt assets/server/tls/snakeoil.crt
cp device.key assets/server/tls/snakeoil.key

{% endhighlight %}

#### 3、编译ngrokd和ngrok

在ngrok目录下执行如下命令

##### 编译服务端 ngrokd：  

make release-server  

编译过程可能出现的问题  

1，源代码语法错误  
	解决： 下载最新的go语言开发包  
2，code.google.com/p/log4go 下载logo4go包的时候 链接超时  
	解决： 到 http://www.golangtc.com/download/package 下载 并解压到 path/to/ngrok/src 下面

##### 编译 客户端 ngrok:

$ make release-client

### 三、调试  

1、启动ngrokd  

{% highlight bash %}

$ ngrokd -domain="dev.airoa.cn" -httpAddr=":8080" -httpsAddr=":8081"
[03/14/15 04:47:24] [INFO] [registry] [tun] No affinity cache specified
[03/14/15 04:47:24] [INFO] [metrics] Reporting every 30 seconds
[03/14/15 04:47:24] [INFO] Listening for public http connections on [::]:8080
[03/14/15 04:47:24] [INFO] Listening for public https connections on [::]:8081
[03/14/15 04:47:24] [INFO] Listening for control and proxy connections on [::]:4443
… …

{% endhighlight %}

2、公网连接ngrokd  

{% highlight bash %}
将生成的ngrok下载到自己的电脑上。
创建一个配置文件ngrok.cfg，内容如下：

server_addr: "dev.airoa.cn:4443"
trust_host_root_certs: false

执行ngrok：
$ ngrok -subdomain example -config=ngrok.cfg 80



如果要生成windows可以用的客户端 

GOOS=windows GOARCH=386 make release-server release-client  #这样编译

其他平台 参考

GOOS                   GOARCH                          OS version
linux                386 / amd64 / arm             >= Linux 2.6
darwin               386 / amd64                   OS X (Snow Leopard + Lion)
freebsd              386 / amd64                   >= FreeBSD 7
windows              386 / amd64                   >= Windows 2000

{% endhighlight %}