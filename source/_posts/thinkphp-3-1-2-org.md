---
title: ThinkPHP 3.1.2载入ORG扩展文件的问题
tags:
  - php
  - thinkphp
  - 二次开发
  - 框架
id: '602'
categories:
  - - 笔记
date: 2013-07-06 17:33:59
---

几个月没有使用thinkphp了。今天重新下载一个3.1.2的来做项目，以前用的都是2.2的。或者就是3.0的.，没有使用过3.1.2的版本。3.1.2的版本只有核心文件。所以很多扩展都需要自己加载。 就那今天要写的验证码来说说吧。。如果是2.2版本的THINKPHP完整版，只需要import('ORG.Util.Image');这样就可以加载Image类库了。但是在3.1.2里面。只有核心文件。没有扩展类库。如果要加载Image类库。需要将该类库放到THINKPHP目录下的extend下。在extend下建立一个文件夹，名为为Library.然后将ORG扩展目录放置在该文件夹内。文件夹层次为 \\www\\ThinkPHP\\Extend\\Library\\ORG，ORG目录里面就是类库的分类了：Crypt、Util、Net等目录了。 当然。你也可以将需要的类库放置到你当前的目录Lib目录下。例如\\www\\home\\Lib\\ORG，加载方法也是一样的。但是有一点需要注意。目录文件前面需要加上符号  @  , 表示当前项目 。 代码如：import('@.ORG.Util.Image'); 需要注意的一点就是。大小写必须对应。否则可能会出错。 另外，要使用Image类库的验证码操作。需要加载另外一个类库。String.class.php。。