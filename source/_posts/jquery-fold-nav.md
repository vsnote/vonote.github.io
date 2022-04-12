---
title: 非常简洁的jquery折叠菜单代码
tags:
  - jquery
  - nav
  - 代码
  - 学习
  - 编程
id: '55'
categories:
  - - 分享
date: 2013-01-23 18:19:20
---

html代码

    *   [导航一](#)
    

        *   [菜单一](#)
        *   [菜单二](#)
        *   [菜单三](#)
    

    *   [导航二](#)
    

        *   [菜单一](#)
        *   [菜单二](#)
        *   [菜单三](#)
    

    *   [导航三](#)

js代码

$(document).ready(function()
{
    $(".jq>li").eq(0).addClass("on");//初始化第一个菜单
    $(".jq>li").next("div.box").eq(0).show();//初始化第一个菜单
    $(".jq>li").mouseover(function()
    {
        $(this).addClass("on").next("div.box").slideDown(300).siblings("div.box").slideUp("slow");
        $(this).siblings().removeClass("on");
    });
});

说实话mouseover这个我不是很常用。看来有时间还是要多多看看手册！