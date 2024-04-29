---
title: 8种用CSS3实现的图片瀑布流动画加载效果
tags:
  - CSS
  - CSS3
  - CSS3特效
  - 分享
  - 动画效果
id: '626'
categories:
  - - 分享
date: 2013-07-13 17:59:29
---

不得不说 **CSS3** 的应用性确实很强大，可以实现各种绚丽的动画效果。这次分享的这个是通过 CSS3 实现的加载不同图片的动画效果，支持响应式，是通过瀑布流的方式来动态展示的。 HTML 代码

    *   [![](images/1.jpg)](http://drbl.in/fWMM)
    *   [![](images/2.jpg)](http://drbl.in/fWPV)
    *   [![](images/3.jpg)](http://drbl.in/fWMT)
    *   [![](images/4.png)](http://drbl.in/fQdt)
    

CSS代码

```css
/\* Effect 4: fall perspective \*/
.grid.effect-4 {
    perspective: 1300px;
}
 
.grid.effect-4 li {
    transform-style: preserve-3d;
}
 
.grid.effect-4 li.animate {
    transform: translateZ(400px) translateY(300px) rotateX(-90deg);
    animation: fallPerspective .8s ease-in-out forwards;
}
 
@keyframes fallPerspective {
    100% { transform: translateZ(0px) translateY(0px) rotateX(0deg); opacity: 1; }
}
```

[查看演示](http://tympanus.net/Development/GridLoadingEffects/)

> 来源网站：http://tympanus.net/codrops/2013/07/02/loading-effects-for-grid-items-with-css-animations/