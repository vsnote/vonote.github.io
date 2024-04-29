---
title: 小白对网页布局的一些看法
link: web-idea
tags:
  - idea
  - web
  - 看法
id: '36'
categories:
  - - 分享
date: 2012-12-08 08:04:21
---

现如今随着HTML5崭头露角、移动APP横行，我相信，WEB3.0的普及很快就会到来！那么网页布局再也不要纠结于用表格还是用DIV+CSS了，用DIV+CSS的时候一些比较复杂的图文排版在IE里面可能会错位，不得不选择表格的方式表现出来。当WEB3.0到来的时候，对我的[个人网站设计](http://vsnote.test)来讲，就像是从天堂到地狱的差别！再也不需要设置各种hack！再也不要担心网站做出来会错位！[网站制作](http://vsnote.test)出来是啥样就是咐样，那种感觉，是多么的美丽！啊，就像是闻到了春天的芬芳，夏天的清凉，秋天的醇香，冬天的寂静。 我记得我最开始学习网制作的时候，就是用的DIV+CSS。虽然表格布局很方便，但是我更喜欢DIV的自由。所以，我布局的时候，通用DIV的就用DIV，不能用DIV的尽量用DIV。好吧，我承认我很固执！我为什么这么喜欢用DIV呢，前面说到的自由是一个方面，还有一个就是容易区分网站的各个部分。要是有些不习惯写注释的人用表格写一个网站，那么别人去查看他的网站的时候就会看到一头雾水，比孙悟空还空。 比如我写代码，我一般DIV的类名都会用一些比较容易看懂的英文或者拼音去命名。这样我就算是不写注释别人来看我的代码也能一眼看个大概。 前两天我看到一篇文章，他讨论的是一个两栏布局，用什么方法去实现。当然，兼容性是要考虑到的。第一种是用浮动，就是两个DIV都用float:left来实现左右布局，代码如下。 html代码：

<div class="content"><div class="aside"></div><div class="main"></div></div>

css代码：

/\*Qzone版\*/
.aside{float: left;width: 170px;}
.main{float: left;width: 790px;}
/\*朋友网版\*/
.aside{float: left;width: 170px;}
.main{overflow: hidden;#zoom:1;}
/\*Fackbook版\*/
.aside{float: left;width: 170px;}
.main{margin-left: 170px;zoom:1;}
/\*Yahoo版\*/
.content{position: relative;zoom:1;}
.aside{position: absolute;left: 0;top: 0;width: 170px;}
.main{margin-left: 170px;zoom:1;}
/\*Google版\*/
.aside{display: inline-block;width: 170px;}
.main{display: inline-block;}

很明显在保持同样html结构的情况下，实现两栏布局可以有多种CSS方案实现（左栏定宽），主要方向是用浮动或不用浮动，右栏定宽或者不定宽： Qzone、朋友网、Facebook都给左栏浮动，唯一不同的是右栏的写法，Qzone给右栏定宽并且浮动，而朋友网和Facebook则并没有给右栏定宽也未浮动，而是利用了创建BFC并且为低版本IE触发hasLayout的原理让右栏自适应宽度。 Yahoo和Google两栏都未用浮动，唯一不同的是Yahoo用了绝对定位的方法，而谷歌用了inline-block，Google已经宣布旗下一些产品放弃对IE8 的支持，所以Google可以大胆的使用inline-block去实现布局，不用去为其他低版本浏览器写一大堆的hack。 当然，没有更好的办法，只有适合自己的办法，尽管每个人的喜好不同，但是目的都是一样的。现在[网站建设](http://vsnote.test)的方案是越来越多，鱼目混珠，分不清楚真假。但是我相信我看到的就是真的！[个人网站设计](http://vsnote.test)也比较多，毕竟一个人一个性格，一个人一个想法。只能尽量的满足不同人的需求，才能在这个苦逼的行业呆下去！