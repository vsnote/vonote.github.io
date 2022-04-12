---
title: JQuery 获取 input 值的多种方法
tags:
  - jquery
  - js
  - 代码
  - 开发
  - 技巧
id: '443'
categories:
  - - 笔记
date: 2013-06-13 22:58:25
---

#### 多选控件

checkbox的第二个元素被打勾

 
$("input\[name=items\]").get(1).checked = true; //打勾
$("input\[name=items\]").get(1).checked = false; //不打勾
if($("input\[name=item\]\[value='val'\]").attr("checked")==true)
//判断是否已经打勾

name即控件name属性,value即控件value属性 可以不指定属性值，因一组checkbox的value值都会保存其在数据库中对应的id，最好写成如下方式

 
if($("input\[name=row\_checkbox\]").attr("checked")==true){
    alert("j");
}else{
    alert("请选择数据！");
}

另，还可以写成

 
if($("\[name=row\_checkbox\]").attr("checked")==true);
    checkbox:$("input\[name='checkbox':checked\]").each(function(){
    var val = $(this).val();
});

#### 单选控件

获取一组radio被选中项的值

 
var item = $("input\[name=items\]\[checked\]").val();
//radio单选组的第二个元素为当前选中项
$("input\[@name=items\]").get(1).checked = true;
$("input\[name=items\]").attr("checked", "1");
//radio的value=’val’的元素为当前选中项

$("input\[name=items\] \[value='val'\]").attr("checked","checked");
$("input\[type=radio\]\[checked\]").val();
$("input\[type=radio\]").attr("checked","2");//设置value=2的项目为当前选中项、

#### 下拉控件

获取select被选中项的文本

 
var item = $("select\[name=items\] option\[selected\]").text();
$("select\[name=items\]").find("option:selected").text();

//select下拉框的第二个元素为当前选中值
$("#select\_id")\[0\].selectedIndex = 1;

//select下拉框value = 'val'的元素为当前选中项
$("select\[name=items\] option\[value='val'\]").attr("selected","selected");
$("select").val();//select的value值
$("select").find(“option:selected”).text();//select选中的text 值
$("#sel".attr("value","-sel3");//设置value=-sel3的项目为当前选中项
$("11112222").appendTo("#sel")//添加下拉框的option
$("#sel").empty();//清空下拉框