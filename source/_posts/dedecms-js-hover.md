---
title: dedecms使用js控制导航hover效果
link: dedecms-js-hover
tags:
  - dedecms
  - js
  - 导航
  - 模板修改
id: '947'
categories:
  - - 笔记
date: 2013-12-30 17:52:02
---

**HTML代码：**

```html
[首页](#)
[栏目页](#)
[栏目页](#)
[栏目页](#)
[栏目页](#)
[栏目页](#)
```

**JS代码：**

```javascript
//导航
$(document).ready(function() {
    var url = window.location.href;
    $(".home").addClass("menu_dq");
    $("#nav li a").each(function(){
        if(url.indexOf($(this).attr("href")) >= 0 && $(this).attr("href") != "/"){  
            $(this).addClass("menu_dq");
            $(".home").removeClass("menu_dq");
        }
    });
});
```