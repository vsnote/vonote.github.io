---
title: 让某个块跟随滚动的JS
tags:
  - js
  - 代码
  - 分享
id: '908'
categories:
  - - 分享
date: 2013-10-23 09:41:09
---

现在基本上每个网站上面都会有某个块跟随滚动的效果，这样可以很充足的使用整个电脑屏幕，让更多的内容给别人看到。分享一个兼容性比较好的封装好的JS代码。 代码如下：

$.fn.smartFloat = function() {
var position = function(element) {
var top = element.position().top,
pos = element.css("position");
$(window).scroll(function() {
var scrolls = $(this).scrollTop();
if (scrolls & gt; top) {
if (window.XMLHttpRequest) {
element.css({
position: "fixed",
top: 0
});
} else {
element.css({
top: scrolls
});
}
} else {
element.css({
position: "",
top: top
});
}
});
};
return $(this).each(function() {
position($(this));
});
};
//绑定
$("#listbanner").smartFloat();

使用是只需要$("#listbanner").smartFloat()，#listbanner 改成自己的元素就成。