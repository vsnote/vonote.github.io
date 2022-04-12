---
title: JS判断时间段的函数
tags:
  - javascript
  - js
  - 代码
  - 笔记
id: '951'
categories:
  - - 笔记
date: 2013-12-31 10:55:49
---

用JS来判断时间范围真的有种蛋疼的感觉，一大串的TIME函数，好好工作吧~

//判断是否在一个时间断
var fun = function (beginTime,endTime){
    var strb=beginTime.split(":");
    if(strb.length!=2){
     return false;
    }
    var stre=endTime.split(":");
    if(stre.length!=2){
     return false;
    }
    var b = new Date();
    var e = new Date();
    var n = new Date();
    b.setHours(strb\[0\]);
    b.setMinutes(strb\[1\]);
    e.setHours(stre\[0\]);
    e.setMinutes(stre\[1\]);

    if(n.getTime()-b.getTime()>0 && n.getTime()-e.getTime()<0){
        if(n.getDay()!=0 && n.getDay()!=6){//判断是否工作日
            return true;
        }else{
            return false;
        }
    }else{
        return false;
    }
}
if(fun("8:30","18:00")){
    document.write("工作时间，请不要浏览网页;-)");
}