---
title: IIS6.0下搭建php+mysql服务器环境小白篇
link: iis6-php-mysql
tags:
  - mysql
  - php
  - 服务器
  - 笔记
id: '25'
categories:
  - - 笔记
date: 2012-11-15 18:15:18
---

已经是第二次给客户建立IIS下的PHP+MYSQL环境了，本以为有了第一次，第二次会很容易，结果还是经过了一番周折。 其实只要是搞清楚步骤了，很快就能弄好。

1.  下载PHP，msi安装版很适合我，就是文件大了一点点。
2.  下载FastCGI，这个很好找。安装了之后在fcgiext.ini的\[Types\]下面加上 php=PHP \[PHP\] ExePath=C:\\Program Files\\PHP\\php-cgi.exe
3.  打开IIS服务器管理界面，在网站的属性里面选择主目录这个选项卡->配置，添加一个应用程序扩展，可执行文件为C:\\WINDOWS\\system32\\inetsrv\\fcgiext.dll，后缀为 .php。
4.  然后下载mysql,默认安装就行了。管理工具我选的是phpmyadmin，

基本的步骤就是上面这些。希望下次遇到IIS不会恐慌！