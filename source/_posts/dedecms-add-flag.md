---
title: dedecms 添加文档自定义属性
link: dedecms-add-custom-attributes
tags:
  - dedecms
  - php
  - 二次开发
  - 代码
  - 功能
  - 笔记
id: '757'
categories:
  - - 笔记
date: 2013-08-11 10:46:12
---

**dedecms** 里面默认的文档属性有些时候满足不了网站上的需要，那么我们就要想办法自己添加文档自定义属性，从而来达到我们的目的。 这个用SQL实现起来很简单，只是不明白官方为什么不在后台加上这个小功能，如果加上了，那样会方便很多。只要了解 dedecms 默认的数据表结构，就能够轻松实现。分别对 `dede_arcatt` `和 dede_archives` 这两张表来操作，下面把代码贴上来：

```sql
insert into sc_arcatt values(9,'ad1','首页广告位一');
```

9是自定义属性的排序ID，因为 dedecms 系统默认的属性有8个，所以从第9个开始。ad1是在标签调用的时候需要用到的，比如`：flag="ad1"`。“首页广告位一”是这个属性的名字，最好是用较少的文字来描述，因为它会显示在编辑文档的自定义属性那。

```sql
alter table `dede_archives` modify `flag` set ('c','h','p','f','s','j','a','b','ad1') default NULL;
```

修改 `dede_archives` 的 `flag` 字段默认值。
