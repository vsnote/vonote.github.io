---
title: Yourphp随机文章调用,纯SQL方法
link: yourphp-rand-article-sql
tags:
  - Yourphp
  - 代码
  - 导航
  - 开发
  - 笔记
id: '34'
categories:
  - - 笔记
date: 2012-12-07 04:55:43
---

Yourphp是一个使用ThinkPHP框架开发的CMS系统，因为之前对ThinkPHP有过一些了解，用这个方便修改，以后加什么东西也快。 Yourphp我一直知道，只是没有去用它，这次也是想试试水，看看它的功能是不是完善，要是行的话，以后就用它了！ 随机文章很简单，但是Yourphp貌似没有把它放在标签里面。所以不得不用SQL来写了。这个随机的语句还是第一次用~

> {php $sql='select \* from mmsite\_article ORDER BY RAND() limit 8'} <YP:list sql="$sql"> <li><img src="../Public/images/arrow.gif">&nbsp;&nbsp;<a href="{$r.url}" target="\_blank">{$r.title}</a></li> </YP:list>

之前我在list标签里面加了个参数 order="rand" 但是不行，难道是 order="rand()" ？等下再去试试。 这次的项目快完结了，只是有些细节需要再修改。做完这个项目，让自己先静下心来，沉淀。 越是到年底了，这心就是安稳不下来，如何是好啊！