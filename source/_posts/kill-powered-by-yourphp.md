---
title: YourPHP 去除 Powered by Yourphp 标题后缀
link: kill-powered-by-yourphp
tags:
  - php
  - Yourphp
  - 代码
  - 开发
  - 菜鸟设计
id: '342'
categories:
  - - 笔记
date: 2013-06-04 16:50:21
---

YourPHP 是我用过最顺手的一个开源程序，它的易用性、扩展性都比其它的建站程序要方便的多。经常用来做一些小网站，所以，也积累了不少这方面的经验。 我相信，最让人感到不愉快的就是网站标题后面的那个 －Powered by Yourphp 这个虽然是作者用来保护自己版权信息的一个举动，但是我们还是会觉得有点碍眼，最好是可以去掉。既然开源，那就要彻底嘛。 按路径找到“\\Core\\Lib\\Template\\ThinkTemplate.class.php”这个文件，然后搜索“Powered by Yourphp”这个词。 第145行

> $tmplContent =  str\_replace('</title>',' - Powered by Yourphp</title>',$tmplContent);

把上面的代码改成这样

> $tmplContent =  str\_replace('</title>',' </title>',$tmplContent);

保存之后更新缓存就OK了。