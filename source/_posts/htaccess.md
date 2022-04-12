---
title: 通过.htaccess文件实现301重定向
tags:
  - php
  - 学习
  - 开发
  - 资料
id: '54'
categories:
  - - 分享
date: 2013-01-21 12:16:29
---

我之前用的是

> RewriteEngine On RewriteCond %{HTTP\_HOST} ^http://gwjsl.com \[NC\] RewriteRule ^(.\*) http://www.gwjsl.com \[L\]

这样看着是对的，但是其实是错的。这个不能实现301。 再看下面这个 修改.htaccess文件内容为下

> RewriteEngine On RewriteCond %{HTTP\_HOST} !^www.gwjsl.com$ \[NC\] RewriteRule ^(.\*)$ http://www.gwjsl.com/$1 \[L,R=301\]

咋的一看觉得是错的。但是这个才能实现301~ 把www.gwjsl.com改为你自己的域名就行。