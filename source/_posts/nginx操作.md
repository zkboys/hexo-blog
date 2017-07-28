---
title: nginx操作
date: 2017-07-28 10:39:42
category: [后端, nginx]
tags: [nginx]
toc: true
---
# nginx 操作
> 反向代理（Reverse Proxy）方式是指以代理服务器来接受internet上的连接请求，然后将请求转发给内部网络上的服务器，并将从服务器上得到的结果返回给internet上请求连接的客户端，此时代理服务器对外就表现为一个服务器。

## 安装
```bash
sudo apt-get install nginx
```

## 启动
```
进入服务器nginx目录：cd /etc/nginx/
执行：sudo nginx
```

## 查看进程
```
ps -ef|grep nginx
```
## 停止
waiting for the worker processes to finish serving current requests
```
sudo nginx -s quit 或 sudo kill -s QUIT 1628（进程编号）
```

without waiting for the worker processes to finish serving current requests
```
sudo nginx -s stop
```

## 重启
更改配置文件之后需要重启
```
sudo nginx -s reload
```

Once the master process receives the signal to reload configuration, it checks the syntax validity of the new configuration file and tries to apply the configuration provided in it. If this is a success, the master process starts new worker processes and sends messages to old worker processes, requesting them to shut down. Otherwise, the master process rolls back the changes and continues to work with the old configuration. Old worker processes, receiving a command to shut down, stop accepting new connections and continue to service current requests until all such requests are serviced. After that, the old worker processes exit.

一旦主线程得到重启命令，它会先校验配置是否正确，如果正确，主线程会启动新的worker线程，关闭旧的worker线程。否则，主线程会回滚到原先的配置，旧的worker线程会得到一个shut down命令，停止接受新连接，但是会继续服务当前请求，当所有的请求处理完之后，会退出。

官网这段话什么意思？如果配置错误，master会roll back，但是worker还是会exit？

## pid文件丢失问题解决方法
```
wangshubin@pc:/etc/nginx$ sudo nginx -c /etc/nginx/nginx.conf
```

## nginx.config配置

这个文件中的配置基本上是没动,只是添加两个include

具体的配置在sites-enabled和sites-available中
```

user wangshubin;

worker_processes 4;

pid /run/nginx.pid;

events {

     worker_connections 768;

     # multi_accept on;

}

http {

     ##

     # Basic Settings

     ##

     sendfile on;

     tcp_nopush on;

     tcp_nodelay on;

     keepalive_timeout 65;

     types_hash_max_size 2048;

        client_max_body_size 10m;

     # server_tokens off;

     # server_names_hash_bucket_size 64;

     # server_name_in_redirect off;

     include /etc/nginx/mime.types;

     default_type application/octet-stream;

     ##

     # Logging Settings

     ##

     access_log /var/log/nginx/access.log;

     error_log /var/log/nginx/error.log;

     ##

     # Gzip Settings

     ##

     gzip on;

     gzip_disable "msie6";

     # gzip_vary on;

     # gzip_proxied any;

     # gzip_comp_level 6;

     # gzip_buffers 16 8k;

     # gzip_http_version 1.1;

     # gzip_types text/plain text/css application/json application/x-javascript text/xml application/xml application/xml+rss text/javascript;

     ##

     # nginx-naxsi config

     ##

     # Uncomment it if you installed nginx-naxsi

     ##

     #include /etc/nginx/naxsi_core.rules;

     ##

     # nginx-passenger config

     ##

     # Uncomment it if you installed nginx-passenger

     ##

     #passenger_root /usr;

     #passenger_ruby /usr/bin/ruby;

     ##

     # Virtual Host Configs

     ##

     include /etc/nginx/conf.d/*.conf;

     include /etc/nginx/sites-enabled/*;

}

#mail {

#     # See sample authentication script at:

#     # http://wiki.nginx.org/ImapAuthenticateWithApachePhpScript

#

#     # auth_http localhost/auth.php;

#     # pop3_capabilities "TOP" "USER";

#     # imap_capabilities "IMAP4rev1" "UIDPLUS";

#

#     server {

#          listen     localhost:110;

#          protocol   pop3;

#          proxy      on;

#     }

#

#     server {

#          listen     localhost:143;

#          protocol   imap;

#          proxy      on;

#     }

#}
```

sites-available文件夹中，inc.eking99.com文件中的内容
sites-enabled文件夹中保存的文件就是sites-available其中的文件
sites-enabled表明sites-available中哪个"网站"是激活状态
sites-enabled中的文件会删除,或者从sites-available中拷贝过来,是一个软链接
```

# Enumerate all the Tornado servers here

upstream inc_eking_tornadoes {

    server 127.0.0.1:8081;

    server 127.0.0.1:8082;

}

proxy_next_upstream error;

server {

    listen 80;

    server_name inc.eking99.com;

    # Allow file uploads

    client_max_body_size 100M;

    location ^~ /s/ {

        alias /home/admin/deploy/inc-eking-web/public/;

        if ($query_string) {

            expires max;

        }

    }

    #location = /favicon.ico {

    #    rewrite (.*) /s/favicon.ico;

    #}

    #location = /robots.txt {

    #    rewrite (.*) /s/robots.txt;

    #}

    location / {

        proxy_read_timeout 1800;

        proxy_pass_header Server;

        proxy_set_header Host $http_host;

        proxy_redirect false;

        proxy_set_header X-Real-IP $remote_addr;

        proxy_set_header X-Scheme $scheme;

        proxy_pass http://inc_eking_tornadoes;

    }

}
```

## nginxWebSocket配置

两种方式
1. 修改nginx.config:
     ```
     map $http_upgrade $connection_upgrade{
          default upgrade;
          "" close;
     }
     ```

     具体网站配置文件：
     ```
     proxy_http_version 1.1;
     proxy_set_header Upgrade $http_upgrade;
     proxy_set_header Connection "upgrade";
     ```
2. 将这两个配置都写到具体网站配置文件中。（将map...放到server配置上面）

## 平时处理nginx用到的一些东西：

一、具体用法

    ln -s 源文件 目标文件

    当我们需要在不同的目录，用到相同的文件时，我们不需要在每一个需要的目录下都放一个必须相同的文件，我们只要在某个固定的目录，放上该文件，然后在其它的目录下用ln命令链接（link）它就可以，不必重复的占用磁盘空间，只生成目标文件的一个镜像。

    例如：ln -s /tmp/less /usr/local/bin/less

二、注意：

    （1）ln命令会保持你每一处连接文件的同步性，不论更改源文件还是目标文件，另一处文件也会有相 同的改动。

    （2）ln命令分为软连接和硬链接（无参数-s）。与软连接不同的是，硬链接会在你选定的位置上生成一个与原来文件大小相同的文件。无论是软连接还是硬链接都具有文件的同步性。

    （3）当一个存储空间，具有几个硬链接时，删除其中的一个，并不会对存储空间进行操作，所以其它的硬链接不会受到影响。

    （4）ln默认时间里硬链接（无参数-s）。

## 原先 www.eking99.com nginx配置：
```
server {
    listen 80 default_server;
    listen [::]:80 default_server ipv6only=on;

    root /home/admin/deploy/www-eking99-web;
    index index.html index.htm;

    server_name www.eking99.com;

    location / {
    }
}

server {
    listen 80;
    server_name eking.mobi www.eking.mobi eking.umail.cn;
    rewrite ^/(.*) http://www.eking99.com/$1 permanent;
}
```

## 原www.eking.com nginx配置：
```

#all the Tornado servers here
upstream www_eking99_tornadoes {
    server 127.0.0.1:9090;
}

proxy_next_upstream error;

server {
    listen 80;
    server_name www.eking99.com eking99.com
    # Allow file uploads
    client_max_body_size 15M;

    location ^~ /s/ {
        alias /home/admin/deploy/www-eking-web/public/;
        if ($query_string) {
            expires max;
        }
    }

    location = /favicon.ico {
        rewrite (.*) /s/favicon.ico;
    }
    location = /robots.txt {
        rewrite (.*) /s/robots.txt;
    }

    location / {
        proxy_pass_header Server;
        proxy_set_header Host $http_host;
        proxy_redirect off; #老版本是false
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Scheme $scheme;
        proxy_pass http://www_eking99_tornadoes;
    }
}

```
## 一般服务器nginx位置：
```
/etc/nginx
sites-available为可用配置，但是不是实际跑的配置
sites-enable 为当前启用的配置，是sites-available的软连接

```
### nginx目录中文件及其作用：
```
conf.d

mime.types

nginx.conf

sites-enabled

fastcgi_params

naxsi_core.rules

proxy_params

uwsgi_params

koi-utf

naxsi.rules

scgi_params

win-utf

koi-win

naxsi-ui.conf.1.4.1

sites-available
```

## 前后端分离 ngnix配置：
```
# 服务地址
upstream api_service {
  server localhost:8080;
  keepalive 2000;
}
#
server {
        listen       80;
        server_name  localhost;
        location / {
          root /home/app/nginx/html;
          index index.html;
          try_files $uri $uri/ /index.html; #react-router 防止页面刷新出现404
        }
        location ^~/api { // 代理ajax请求，前端的ajax请求配置了统一的baseUrl = ‘/api’
           proxy_pass http://api_service/;
           proxy_set_header Host  $http_host;
           proxy_set_header Connection close;
           proxy_set_header X-Real-IP $remote_addr;
           proxy_set_header X-Forwarded-Server $host;
        }
}

```
