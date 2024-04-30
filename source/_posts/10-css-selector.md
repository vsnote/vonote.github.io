---
title: 10个你不可不用的CSS选择器
link: 10-css-selector
tags:
  - CSS
  - 前端开发
  - 技巧
  - 教程
  - 笔记
id: '776'
categories:
  - - 分享
date: 2013-08-14 13:26:58
---

每当我们使用 **CSS** 的时候，我们都会使用选择器。但是尽管如此，**CSS选择器** 是最容易被我们忽视的一部分。人们总是在谈论CSS的巨大变革而忽略了其本质。会使用选择器会使我们日常编程的工作变得简单且讲究。今天我就将介绍10个选择器是我们容易忽略，但确实非常重要且行之有效的。 
## *

`*` 这个选择器应该是你最容易记住的，但是你不一定会记得使用它。它是用来为页面上所有元素进行样式设置，尤其是当你想要设置页面默认样式，或者是创建重置样式的时候，* 就是一个非常方便的选择器。

```css
{
   margin: 0;
   padding: 0;
   font-family: helvetica, arial, sans-serif;
   font-size: 16px;
}
```

## A+B

A+B 选择器称为邻近选择器，它的作用是选择紧邻着前一个元素的元素。例如它的写法是 A+B，那么你所选择的是紧邻在A元素后面的第一个B元素。如果你想要选择 header 元素后面的第一个div元素，你可以按照下面这种写法：

```css
header + div {
   margin-top: 50px;
}
```

## A>B

这个选择器只用于选择直接子元素，相信你知道A B这样的写法，是用来选择A元素下面任意层的B元素，而A>B只会选择A元素下面的直接子元素。当你想要操作父元素的第一层子元素时，就需要用到这个选择器。例如你有一个列表元素，ul嵌套li如下：

```html
<ul>
    <li>List Item With ul
        <ul>
            <li>Sub list item</li>
            <li>Sub list item</li>
            <li>Sub list item</li>
        </ul>
    </li>
    <li>List Item</li>
    <li>List Item</li>
</ul>
```

你只想要给ul的直接子元素li元素设定样式，你就可以用这个A>B选择器。如果用A B选择器的话，所有嵌套的li元素都会被应用样式。

```css
ul > li {
   background: black;
   color: white;
}
```

## A[href*="example"]

如果你想要将一个超链接设定一个特定样式的话，那就非这个选择器莫属，用于为任何与引号内的内容匹配的超链接设定样式。假如你想要将所有链接到facebook的超链接加一个蓝色的样式，你就可以写成：

```css
a[href*="facebook"] {
   color: blue;
}
```

当然，还可以不带*，这样就是给完全匹配引号内地址的超链接进行样式设定。

## A:not(B)

这个选择器在特定时候还是挺重要的，它的用意是，选择除了在B元素内的所有A元素。比如你想要选择除了在footer内的所有div元素，那么你就可以写成：

```css
div:not(.footer) {
   margin-bottom: 40px;
}
```

## A:first-child / A:last-child

顾名思义，_first-child_ 和 _last-child_ 是用来选择父元素中的第一个子元素和最后一个子元素的选择器。我们有时候会在一个列表中，希望第一个列表元素和最后一个列表元素有不同于其他元素的表现形式，我们就可以用这个选择器。 比如，移除第一个列表元素的边框，给最后一个列表元素移除右边距：

```css
ul li:first-child {  
   border: none;  
}     
ul li:last-child {  
   margin-right: 0px;
}
```

## A:nth-child(n)

_nth-child_ 是用来按照顺序来选择A元素内的子元素。比如你想要选择第三个列表元素，你可以写成：

```css
ul li:nth-child(3) {
   background: #ccc;
}
```

我们可以使用n来成倍选择子元素，比如我们在括号内写3n的话，那么该选择器会选择第3个，第6个，第9个，12个，按照3n的规律成倍选择子元素。 **A:nth-last-child(n)** _nth-last-child_ 与 _nth-child_ 差不多，不过它不是从前遍历，而是从最后一个元素向前遍历。所以如果你在括号里写3的话，这个选择器是选择了父元素里面的倒数第3个子元素：

```css
ul li:nth-last-child(3) {
   background: #ccc;
}
```

## A:nth-of-type(n)

**从写法来看的话**，不太容易看出来这个选择器是做什么的。但是让我们看一下下面这个例子，你可以理解了。

```css
div p:nth-of-type(3) {
   font-style: italic;
}
```

以上这段代码的意思是，寻找在div元素中的第三个p元素。所以这个选择器是用来选取你的页面内，与你写的类型匹配的元素。 **A:visited** 你应该注意过，当你在 google 上点过的链接，都会变成别的颜色。这个就是 visited 选择器做的。这个选择器很好用，但是很容易被遗忘，但是每当我用 google 的时候，就觉得这个选择器是非常有用的！

```css
a:visited {
   color: blue;
}
```

用这些选择器，会节省很多编程时间，而且可以避免使用太多的ID。当然这些只是CSS选择器的入门，实际上仍有很多选择器，很好用但是经常被我们所忽略。

> 文章来源：http://www.webdesignerdepot.com/2013/08/10-css-selectors-you-shouldnt-code-without/