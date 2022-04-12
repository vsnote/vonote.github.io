---
title: jQuery 2.0 改革性版本，不再支持 IE6/7/8，是福是祸躲不过啊！
tags:
  - javascript
  - jquery
  - 代码
  - 开发
  - 菜鸟设计
id: '277'
categories:
  - - 分享
date: 2013-05-21 13:24:44
---

到JQuery2.0的发布，流行的jQuery JavaScript库到了一个重要里程碑。2.0版本比前任版本在大小上缩减了12%，但是更大的新闻是，jQuery 2.0不在对IE6，7，8三个版本进行支持。 七年前jQuery的诞生，开始让开发者更简单的操作HTML和编写JavaScript，jQuery的跨浏览器特性，更是很快受到了广大开发者的青睐。根据去年的一项调查显示，粗略估计，网络上一半的站点都在使用jQuery。 停止对旧版IE的支持，是否会改变jQuery的使用率？答案也许是不会。如果你的网站需要维护对IE8或者低版本（或者是IE9和IE10在兼容模式下运行），你只需要沿用jQuery1.9或者以下版本。 “jQuery2.0主要用于现代网络，”jQuery的Dave Methvin在Query Foundation网站上写道，“我们有jQuery1.x版本处理旧版浏览器，并且期望他可以支持好几年。” 如果你想要同时兼容新旧版浏览器，你可以使用条件注释，让2.0在新浏览器上使用，而旧版本使用1.9，但是更简单的方法则是沿用jQuery1.x版本。至少目前2.0的主要用例，对IE的支持是不再考虑范围内了，而是Chrome或者Firefox的附加组件，PhoneGap应用程序或是node.js。

> 文章引用：http://www.webmonkey.com/2013/04/webs-most-popular-javascript-library-drops-support-for-older-versions-of-ie/