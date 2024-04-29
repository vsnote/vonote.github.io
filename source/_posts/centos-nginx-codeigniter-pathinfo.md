---
title: centos nginx 配置 codeigniter pathinfo(伪静态)
link: centos-nginx-codeigniter-pathinfo
tags:
  - centos
  - codeigniter
  - linux
  - nginx
id: '1020'
categories:
  - - 笔记
date: 2014-07-09 10:21:01
---

在 linux+nginx 环境下配置 codeigniter 使用 pathinfo 的URL方式，跟windows下的区别不大，但是要注意版本问题。 服务器环境：centos 6.3、nginx1.4.7、php5.2.17

server {
    listen  80;
    server\_name www.example.com;
    rewrite\_log on;
    root /www/www.example.com;    
    index index.php  index.html index.htm;        
    location / {
        index index.php index.html index.htm;
    }
    location ~ \\.php($/) {
        fastcgi\_pass 127.0.0.1:9000;
        fastcgi\_index index.php;
        fastcgi\_split\_path\_info ^(.+\\.php)(.\*)$;
        fastcgi\_param PATH\_INFO $fastcgi\_path\_info;
        fastcgi\_param SCRIPT\_FILENAME  $document\_root$fastcgi\_script\_name;
        include fastcgi\_params;
    }

    if (!-e $request\_filename) {
        rewrite ^/(.\*)$ /index.php/$1 last;
        break;
    }

    location ~ /\\.ht {
        deny all;
    }
}