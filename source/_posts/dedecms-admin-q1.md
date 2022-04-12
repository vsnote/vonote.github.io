---
title: dedecms 织梦登录后台慢的完美解决方案
tags:
  - dedecms
  - 二次开发
  - 代码
  - 开源程序
  - 笔记
id: '749'
categories:
  - - 笔记
date: 2013-08-09 02:10:02
---

用了下 **dedecms** v5.7 SP1 版本，发现很多问题，其中一个比较严重的是，架到服务器上的 dedecms 网站后台打开菜单选项卡得不能动，等半天显示505服务器错误，这个真让人纠结，在本地调试明明好好的，放在服务器为什么不行了呢？检查了下源文件，发现是 dedecms 安全提示执行缓慢造成的，下面是解决方案： 打开 dedecms 后台/templets/的index\_body.htm文件，找到第25行至第34行代码，将其注释掉，保存上传覆盖，刷新下后台，OK，解决了！ ![dedecms-admin-q1](http://vsnote.test/wp-content/uploads/2013/08/0.jpg)