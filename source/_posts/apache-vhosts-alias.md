---
title: Apache 添加虚拟主机/虚拟目录
link: apache-vhosts-alias
tags:
  - alias
  - apache
  - vhost
id: '1012'
categories:
  - - 笔记
date: 2014-06-21 13:19:50
---

## Apache 添加虚拟目录

```
vim /usr/local/apache/conf/httpd.conf #编辑apache配置文件

:/IfModule alias_module #搜索alias模块

Alias /test "/www/test" #添加test虚拟目录

:wq #保存

service httpd restart #重启 Apache
```

## Apache 添加虚拟主机

```
vim /usr/local/apache/conf/extra/httpd-vhosts.conf #编辑apache虚拟主机配置文件
```

```apache
<VirtualHost *:80> ServerName domain.com  
 DocumentRoot "/phpstudy/www/domain"  
<Directory "/phpstudy/www/domain">  
    Options +Indexes +FollowSymLinks +ExecCGI  
    AllowOverride All  
    Order allow,deny  
    Allow from all  
    Require all granted  
</Directory>  
</VirtualHost>
```
