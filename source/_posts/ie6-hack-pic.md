---
title: 解决多张图片排版在IE6下有空隙的方法
link: ie6-hack-pic
tags:
  - CSS
  - hack
  - HTML
  - IE6
  - 兼容
  - 排版
id: '47'
categories:
  - - 分享
date: 2012-12-29 01:43:02
---

对于IE6，我已经没有什么话可说了，更多的只是忍耐，然后细心的去检查代码。 多张图片排版，举个例子，如下图 [![](../images/uploads/2012/12/6pic.png "六张图片")](../images/uploads/2012/12/6pic.png) 六张图片并排排列，中间没有任何元素。但是在IE6下面就会出现这样的情况 [![](../images/uploads/2012/12/6pic2.png "6pic2")](../images/uploads/2012/12/6pic2.png) 每个图片中间会有一个小缝隙，而且不知来路。经过一番寻找，发现在IE下面多图片之间不能有任何空格或者回车。到此问题解决。