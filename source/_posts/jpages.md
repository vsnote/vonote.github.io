---
title: jPages - 一个超酷的jQuery分页插件
tags:
  - HTML
  - javascript
  - jquery
  - 插件
id: '486'
categories:
  - - 笔记
date: 2013-06-16 08:30:54
---

有时候在网站开发中会遇到一些在逻辑外的需求，比如说在一个单网页里，图片太多，可能分页显示会友好一点。第一想法就是先Google一下，找找解决方案。于是，**Jpages**插件的出现让我喜出望外。 Jpages是一个基于JQuery框架的客户端(PS:一般我们都是在服务器端分页)分页插件，使用方法之非常简单，自带很多超酷的特效和功能，还有非常丰富的自定义参数！

#### 功能特性

*   自动翻页
*   键盘和鼠标滚动浏览
*   延缓页面内容显示
*   完全自定义的分页导航支持
*   如果需要特效或者lazyload，可和其它js类库整合：[Animate.css](http://daneden.me/animate/) 和 [Lazy Load](http://www.appelsiini.net/projects/lazyload)
*   支持各种类型的页面导航菜单，可供大家选择
*   兼容主流浏览器及其IE7+

#### 使用方法

把下面这段代码放到标签前面

如果你想使用Animate动画，你还需要添加文件：

下面是HTML演示代码，容器除了UL之外也可是其他结构相同的标签，holder是分页，它会自动生成HTML代码。你只要给它一个位置就可以了。

*   ...
*   ...
*   ...
*   ...
*   ...
...

初始Jpages化插件

$(function(){
  $("div.holder").jPages({
    containerID : "itemContainer"
  });
});

#### 更多自定义参数

*   containerID：需要实现分页的容器元素，可以是div或者UL，OL
*   first： 自定义”首页“button是否显示，缺省为false，如果传递字符串，则显示为“首页”文字。
*   previous：自定义”上一页“button是否显示
*   next：同上是否显示”下一页“button
*   last：是否显示”尾页“button
*   startPage：需要显示的开发页数，缺省为”1“
*   perPage：每页显示的项目数，缺省为”10“
*   midRange：显示包含当前页数显示页面数量，缺省为”5“
*   startRange：显示开始显示的页面数，无论目前你处于哪个页面，缺省”1”。
*   endRange：显示末尾显示的页面数，无论目前你处于哪个页面，缺省”1”。
*   callback：回调函数function(page, items){}，pages对象属性，pages.current，pages.interval，pages.count
*   animation：使用Animate.css的动画效果，当然需要添加css3类库支持。
*   fallback：如果不使用CSS3动画，你可以使用fallback来设定jQuery的淡入效果的速度。

> 来源：[分享一个jQuery的超酷分页插件 - jPages](http://www.gbin1.com/technology/jquerynews/20120418jquerypluginjpages/)