---
title: YourPHP 提示 PHP Fatal error 解决方法
tags:
  - Yourphp
  - 代码
  - 问题
id: '517'
categories:
  - - 笔记
date: 2013-06-21 15:05:56
---

yourphp 这个系统总是会有一些意想不到的问题出现，而官方又没有很明确的解决方法，只能在自己不断的使用中发现问题，解决问题。 今天，又遇到了一个非常奇葩的问题，上传缩略图之后，打开该内容所在的栏目，提示：

> PHP Fatal error: Allowed memory size of 33554432 bytes exhausted (tried to allocate 9000 bytes) in H:\\root\\home\\ghdqlz-004\\www\\site1\\Cache\\~runtime.php on line 1

按照正常的解决过程应该是PHP内存大小的限制，只需要重新定义一个合适的大小就行了。但是我改了之后还是没解决这个问题，于是，在一个交流群里面找到了方法，原因是因为我上传的缩略图太大，重新上传一个小一点的图片，问题终于得到解决。 以后上传图片一定要注意图片尺寸不要过大，最好是上传之前做一些优化。尽量不要超过300Kb。