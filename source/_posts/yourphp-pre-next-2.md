---
title: YourPHP 上一篇下一篇优化代码「适应各种模型」
link: yourphp-pre-next-2
tags:
  - php
  - Yourphp
  - 二次开发
  - 代码
  - 开源程序
  - 笔记
id: '800'
categories:
  - - 笔记
date: 2013-08-23 11:49:26
---

今天又碰到一个网友问 YourPHP 上一往篇下一篇怎么写，以前我初学 YourPHP 建站的时候其实也遇到过这个问题。我也纠结了不少时间，官方给的开发手册里边根本就没有这个标签。后来东找西看，在它的标签扩展里面发现了上一篇跟下一篇的标签，其实 YourPHP 的作者在标签扩展里面有写这两个标签，只是没有写在手册里面。顿时有一种被坑了的感觉(/ □ \\)。 但是这两个标签并不是很好用，于是自己又写了下，是放在模版文件里面的，直接复制过去就行，源代码：

where("id<$id")->field("title,url")->order("id desc")->find();
$next = M($module\_name)->where("id>$id")->field("title,url")->order("id asc")->find();
$pre ? $pre = '上一篇：['.$pre\['title'\].']('.$pre['url'].')' : $pre = '上一篇：已经是第一篇了';
$next ? $next = '下一篇：['.$next\['title'\].']('.$next['url'].')' : $next = '下一篇：文章还没写出来呢';
?>
*   {$pre}
*   {$next}