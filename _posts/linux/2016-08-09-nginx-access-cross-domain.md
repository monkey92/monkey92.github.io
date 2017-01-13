---
layout: post
title: nginx允许跨域访问配置
categories: linux
---

## 配置文件  


{% highlight bash %}

server {
    listen       80;
    server_name  192.168.0.111;
    root /var/www/bdyq-api-server/public;
    location / {
        index  index.html index.htm index.php;
        try_files $uri $uri/ /index.php?$query_string;
    }
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }
    location ~ \.php$ {
        fastcgi_pass   unix:/run/php/php7.0-fpm.sock;
        fastcgi_index  index.php;
        fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
        include        fastcgi_params;
    }

    add_header  Access-Control-Allow-Origin *;
    add_header  Access-Control-Allow-Methods GET,POST,OPTIONS;
    add_header  Access-Control-Allow-Headers X-Requested-With,Content-Type;

}

{% endhighlight %}