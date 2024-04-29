---
title: thinkphp 框架里面原生 php 代码的写法
link: thinkphp-php-code-in-template
tags:
  - php
  - thinkphp
  - 代码
  - 框架
id: '535'
categories:
  - - 笔记
date: 2013-06-25 16:58:32
---

**thinkphp** 框架还是2011年的时候接触的，那时正好暑假闲的发慌，而那时候家里面又没有网络，刚好硬盘里面有一个 thinkphp 的学习视频，于是就啃了两个月的 thinkphp 教程。 到现在也两年多了，很久没有用它写过东西了，有些地方还真记不住。就把它发到这里吧！ 一共是有两张方法，第一种就是用PHP标签：

 $siteName="菜鸟笔记";
$siteUrl="http://vsnote.test";
echo $siteName.' '.$siteUrl; 

第二种是使用原声PHP写法：

以上两种方法都可以运行PHP语法，但是不可以在里面使用thinkphp的标签和模板变量，比如： 我在控制器里面定义了一个变量

$this->assign('siteName',"菜鸟笔记");

然后我想在模板里面判断，当这个变量等于菜鸟笔记的时候就输出"http://vsnote.test"

 if({$siteName} == "菜鸟笔记") echo "http://vsnote.test"; 

因为在PHP代码里面使用了模板变量 $siteName，所以是不会生效的。 最近会抽点时间来复习一下 thinkphp，到时候会把一些笔记都记录下来。(记性太差了)