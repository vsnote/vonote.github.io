---
title: jquery $.ajax $.post或者$.get如何提交checkbox的值
link: jquery-ajax-post-get-checkbox
tags:
  - ajax
  - checkbox
  - jquery
id: '960'
categories:
  - - 笔记
date: 2014-03-08 08:58:36
---

form表单中包含有checkbox这种表单项的时候，直接提交处理很简单，只需在程序中处理结果即可。但使用jquery的ajax提交时该如何处理呢？下面通过一个例子说明一下。

jquery $.ajax $.post或者$.get如何提交checkbox的值// <!\[CDATA\[
function submitForm(){
    var str='';
    $("#phpernote>\[type=checkbox\]").each(function(){
        if($(this)\[0\].checked) {
            str+=$(this).val()+',';
        }
    });
    alert(str);
}
// \]\]>

1 2 3 4 5 

  思路很简单，就是把选中的值都取出来，通过循环处理成字符串，然后传递出去。

> 来源：[php程序员的笔记](http://www.phpernote.com/)