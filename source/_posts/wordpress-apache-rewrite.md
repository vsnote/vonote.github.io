---
title: wordpress伪静态设置(Apache服务器下)
link: wordpress-apache-rewrite
tags:
  - apache
  - wordpress
  - 代码
  - 开发
  - 教程
  - 程序
id: '31'
categories:
  - - 笔记
date: 2012-11-30 18:13:55
---

今天刚刚把服务器移植好，出了一些小问题。 文章的地址打不开，在网站根目录下面创了个.hatccess文件。 <IfModule mod\_rewrite.c> RewriteEngine on RewriteCond %{REQUEST\_FILENAME} !-d RewriteCond %{REQUEST\_FILENAME} !-f RewriteRule ^(.\*)$ index.php/$1 \[QSA,PT,L\] </IfModule> 加入这段代码，就实现伪静态了！ 我之前的用的是美国的VPS，感觉速度很慢，还经常宕机(就是价格比较便宜)。没办法，又在香港找了个。 Window系统安装和方便，但是运行Wordpress不是很好。所以我让他们的技术给我装了个Linux系统，还有kloxo这个平台，管理起来很方便，因为主要是要测试一些站点，放虚拟主机里面太麻烦，希望这个空间太平无事~