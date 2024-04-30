---
title: 小白对网页布局的一些看法
link: web-idea
tags:
  - web
  - HTML
  - CSS
id: '36'
categories:
  - - 分享
date: 2012-12-08 08:04:21
---

## 网页布局的未来展望

随着 **HTML5** 的崭露头角和移动 APP 的横行，我相信，WEB3.0 的普及很快就会到来！这将标志着网页布局不再需要纠结于使用表格还是 DIV+CSS 了。

使用 DIV+CSS 时，一些较复杂的图文排版在IE浏览器里可能会错位，这常常迫使设计者不得不选择表格来实现布局。但当 WEB3.0 到来时，对于我的个人网站设计来说，这将是从天堂到地狱的转变！

我们将不再需要设置各种 hack，也不必担心网站出现错位问题。网站制作出来的效果将会是精确的，这种改变带来的满足感，如同四季更替带来的美好。

## 我的布局偏好

我记得最初学习网站制作时，我采用的是 DIV+CSS。虽然表格布局方便，但 DIV 的灵活性让我更为喜爱。因此，我在布局时，只要可能，就尽量使用 DIV。

我喜欢 DIV 的原因之一是它带来的自由感，同时也方便区分网站的各个部分。使用表格布局的人如果不习惯写注释，那么他们的代码可能会让人摸不着头脑。而我在命名 DIV 的类时，通常会使用容易理解的英文或拼音，即便不写注释，其他人也能大致理解我的代码。

## 讨论两栏布局的实现方法

前不久我阅读了一篇文章，讨论如何实现两栏布局。当然，兼容性是必须考虑的。

### 代码示例

html代码：
```html
<div class="content">
    <div class="aside"></div>
    <div class="main"></div>
</div>
```

css代码：
```css
/* Qzone版 */
.aside{float: left;width: 170px;}
.main{float: left;width: 790px;}
/* 朋友网版 */
.aside{float: left;width: 170px;}
.main{overflow: hidden;#zoom:1;}
/* Fackbook版 */
.aside{float: left;width: 170px;}
.main{margin-left: 170px;zoom:1;}
/* Yahoo版 */
.content{position: relative;zoom:1;}
.aside{position: absolute;left: 0;top: 0;width: 170px;}
.main{margin-left: 170px;zoom:1;}
/* Google版 */
.aside{display: inline-block;width: 170px;}
.main{display: inline-block;}
```

很明显在保持同样 HTML 结构的情况下，实现两栏布局可以有多种 CSS 方案实现（左栏定宽），主要方向是用浮动或不用浮动，右栏定宽或者不定宽： Qzone、朋友网、Facebook 都给左栏浮动，唯一不同的是右栏的写法，Qzone 给右栏定宽并且浮动，而朋友网和 Facebook 则并没有给右栏定宽也未浮动，而是利用了创建 BFC 并且为低版本 IE 触发 hasLayout 的原理让右栏自适应宽度。Yahoo 和 Google 两栏都未用浮动，唯一不同的是 Yahoo 用了绝对定位的方法，而谷歌用了 inline-block，Google 已经宣布旗下一些产品放弃对 IE8 的支持，所以 Google 可以大胆的使用 inline-block 去实现布局，不用去为其他低版本浏览器写一大堆的hack。 当然，没有更好的办法，只有适合自己的办法，尽管每个人的喜好不同，但是目的都是一样的。现在网站建设的方案是越来越多，鱼目混珠，分不清楚真假。

但是我相信我看到的就是真的！个人网站设计也比较多，毕竟一个人一个性格，一个人一个想法。只能尽量的满足不同人的需求，才能在这个苦逼的行业呆下去！
