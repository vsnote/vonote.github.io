---
title: Yourphp v3.0 正式版安装和Ypampz集成环境体验
tags:
  - php
  - Yourphp
  - yourphp3.0
  - 二次开发
  - 代码
  - 开源程序
id: '636'
categories:
  - - 笔记
date: 2013-07-18 09:56:41
---

**Yourphp**正式版应该是前几天就出来了，貌似官方没有写发布的消息，而是在下载的地方改成了3.0正式版。我也是昨天去下载了才看本来打算自己安装Nginx + PHP5.3 + MySQL5 + ZendLoader 的环境的，但在Yourphp作者的网盘里面看到了Ypampz这个程序。Ypampz也是Yourphp的作者自己弄的一个集成环境，集成了Apache2.4+mysql5+php5.3+zendLoader这几个Yourphp需要的程序。

#### **Ypampz截图**

![ypampz](http://vsnote.test/wp-content/uploads/2013/07/ypampz.jpg)  

#### Ypampz运行截图

![ypampz2](http://vsnote.test/wp-content/uploads/2013/07/ypampz2.jpg)   这个程序看起来蛮清爽的，可以无痕迹运行Apache和Mysql，相当于一个绿色版软件。

#### Yourphp3.0后台界面：

![yourphp3](http://vsnote.test/wp-content/uploads/2013/07/YP3.jpg) 接下来说说Yourphp3.0的变化：

*   程序后台的界面还是一样，并没有啥新鲜感
*   后台首页多了一个序列号的信息，看来作者是要极力推崇开源程序正版化了
*   模块管理新增单页模型，原本在模型管理里面的在线留言也移动到这里了
*   模块管理新增财务管理，这个貌似很高端，应该是搞商务的用的
*   在本机测试，貌似3.0的后台有点略卡
*   体验完毕

按照官方的说法，精简了Thinkphp的核心，程序运行会更快更稳。为啥后台感觉比之前2.0版的要卡很多，好吧，我智商拙计，待以后看看官方说法。

#### 下载地址

[yourphp3.0正式版下载](http://pan.baidu.com/share/link?shareid=688108135&uk=1796312283) [Ypampz下载](http://pan.baidu.com/share/link?shareid=691954315&uk=1796312283)