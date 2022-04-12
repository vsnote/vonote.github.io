---
title: 在Apache服务器中配置ThinkPHP伪静态URL
tags:
  - php
  - PHP框架
  - thinkphp
  - 二次开发
  - 代码
  - 笔记
id: '730'
categories:
  - - 笔记
date: 2013-08-02 20:50:31
---

ThinkPHP 作为国内最流行的一个PHP框架，由于她开发应用的便捷，便吸引越来越多的开发者开始使用她来做项目的底层架构。像我PHP基础并不是很好，也可以使用她来完成一个像模像样的项目。 下面便分享一些使用ThinkPHP需要了解的东西。

#### 去掉 URL 中的 index.php

ThinkPHP是单一入口的，默认的 URL 不是很友好。但 ThinkPHP 提供了各种机制来定制需要的 URL 格式，配合 Apache 里面的 .htaccess 文件，更是可以定制出人性化的更利于 SEO 的 URL 地址来。 .htaccess文件是 Apache 服务器中的一个配置文件，它负责相关目录下的网页配置。我们可以利用 .htaccess 文件的 Rewrite 规则来隐藏掉 ThinkPHP URL 中的 index.php 文件（即入口文件），这也是 ThinkPHP URL 伪静态的第一步。 例如原来的 URL 为： http://127.0.0.1/index.php/Index/insert 去掉 index.php 之后变为： http://127.0.0.1/Index/insert 如此一来，就变成了 http://服务器地址/应用模块名称/操作名称\[/变量参数\] 的常见 URL 格式。 更改 Apache httpd.conf 配置文件 提示：如果在虚拟主机商配置，请直接配置第三、四步，因为支持 .htaccess 的空间已经配置好了前面两步。用编辑器打开 Apache 配置文件 httpd.conf（该文件位于 Apache 安装目录Apache2conf），并按如下步骤修改。 **一、加载了 mod\_rewrite.so** 确认加载了 mod\_rewrite.so 模块（将如下配置前的 # 号去掉）： LoadModule rewrite\_module modules/mod\_rewrite.so **二、更改 AllowOverride 配置** 更改需要读取 .htaccess 文件的目录，将原来的目录注释掉： #<Directory "C:/Program Files/Apache Group/Apache2/htdocs"> 更改 AllowOverride None 为 AllowOverride FileInfo Options ，更改后的配置如下所示： #<Directory "C:/Program Files/Apache Group/Apache2/htdocs"> AllowOverride FileInfo Options .htaccess 是基于目录来控制的， 该句即表示需要读取 .htaccess 文件的目录，要根据实际具体 Apache 的解析目录来配置。虚拟主机如果提供 .htaccess 控制，一般都已经配置好了。 **三、添加 .htaccess 文件 Rewrite 规则** 在需要隐藏 index.php 的目录下（本教程中为 E:/html/myapp，也即入口文件所在目录）创建 .htaccess 文件，并写入如下规则代码： RewriteEngine on #不显示index.php RewriteCond %{REQUEST\_FILENAME} !-d RewriteCond %{REQUEST\_FILENAME} !-f RewriteRule ^(.\*)$ index.php/$1 \[QSA,PT,L\] **四、更改项目配置文件** 编辑项目配置文件 Conf/config.php ，将 URL 模式配置为 2（Rewrite模式）： 'URL\_MODEL'=>2, 至此，各个配置已经完成。保存各配置文件后，重启 Apache 服务器并删除 Runtime 目录下的项目缓存文件，在浏览器访问隐藏 index.php 后的地址测试是否成功： http://127.0.0.1/html/myapp/Index/index 如果访问成功，那么利用 Apache .htaccess 文件的 Rewrite 规则隐藏 index.php 入口文件的配置就成功了。