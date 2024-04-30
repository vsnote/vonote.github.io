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

在 linux+nginx 环境下配置 codeigniter 使用 pathinfo 的 URL 方式，跟 windows 下的区别不大，但是要注意版本问题。 服务器环境：centos 6.3、nginx1.4.7、php5.2.17

```conf
server {
    listen  80;
    server_name www.example.com;
    rewrite_log on;
    root /www/www.example.com;    
    index index.php  index.html index.htm;        
    location / {
        index index.php index.html index.htm;
    }
    location ~ \.php($/) {
        fastcgi_pass 127.0.0.1:9000;
        fastcgi_index index.php;
        fastcgi_split_path_info ^(.+\.php)(.*)$;
        fastcgi_param PATH_INFO $fastcgi_path_info;
        fastcgi_param SCRIPT_FILENAME  $document_root$fastcgi_script_name;
        include fastcgi_params;
    }

    if (!-e $request_filename) {
        rewrite ^/(.*)$ /index.php/$1 last;
        break;
    }

    location ~ /\.ht {
        deny all;
    }
}
```
