---
title: 符合网页标准的CSS表格制作
tags:
  - CSS
  - 代码
  - 学习
  - 开发
  - 排版
id: '50'
categories:
  - - 分享
date: 2013-01-07 17:09:51
---

在加内容的时候，有些数据必须要用表格才能展示出来，所以，了解标准化表格的制作，是一个编辑一定要知道的。 这些貌似以前还真不知道。 css代码：

table.extbl{
border-collapse: collapse;
font-size:12px;
}
table.extbl td,table.extbl th{
border: 1px solid black;
padding: 4px;
}
table.extbl tr.headers{
font-weight: bold;
}

html代码

公司

雇员

成立于

ACME Inc

1000

1947

XYZ Corp

2000

1973