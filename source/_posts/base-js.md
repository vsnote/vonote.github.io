---
title: 自己写的一个原生态JS选项卡
link: base-js-tab-control
tags:
  - javascript
  - 代码
  - 学习
  - 开发
id: '51'
categories:
  - - 分享
date: 2013-01-12 19:14:20
---

// <!\[CDATA\[
function changediv(id){ 
    var thisid = document.getElementById("div"+id); 
    for(var i=1;i>0;i++){
    var getid = document.getElementById("div"+i);
    if(getid){
        if(getid==thisid){
    document.getElementById("div"+i).style.display="block";
}else{
    document.getElementById("div"+i).style.display="none";
}
    }else{
        break;
    }
}
}
// \]\]>