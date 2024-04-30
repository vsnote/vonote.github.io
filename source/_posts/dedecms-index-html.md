---
title: dedecms 去掉首页链接的index.html
link: dedecms-index-html
tags:
  - dedecms
  - php
  - 二次开发
  - 笔记
  - 菜鸟
id: '688'
categories:
  - - 笔记
date: 2013-07-24 17:16:38
---

dedecms 最大的亮点就是生产Html非常方便、快捷，但是它默认生成的index.html会自动在首页链接后面显示。有时候由于网站优化的需要，要去掉这个index.html文件名。 只需在.hatccess文件里面加一个规则就可以了

```apache
DirectoryIndex index.html index.php index.htm
```