---
title: jQuery获取各种input属性的方法
tags:
  - jquery
  - 代码
  - 技巧
  - 编程
id: '24'
categories:
  - - 笔记
date: 2012-11-15 10:05:02
---

if($("input\[name=item\]\[value='val'\]").attr('checked')==true) //判断是否已经打勾

name即控件name属性,value即控件value属性。 可以不指定属性值，因一组checkbox的value值都会保存其在数据库中对应的id，最好写成如下方式

if($("input\[name=row\_checkbox\]").attr('checked')==true)
{
alert("j");
}
else
{
alert("请选择数据！");
}

另，还可以写成

if($("\[name=row\_checkbox\]").attr('checked')==true)

jquery radio取值,checkbox取值,select取值,radio选中,checkbox选中,select选中,及其相关

获取一组radio被选中项的值

var item = $('input\[name=items\]\[checked\]').val();

获取select被选中项的文本

var item = $("select\[@name=items\] option\[@selected\]").text();

获取select被选中项的文本

var item = $("select\[name=items\] option\[selected\]").text();
//或
$("select\[name=items\]").find("option:selected").text();

select下拉框的第二个元素为当前选中值

$('#select\_id')\[0\].selectedIndex = 1;

select下拉框value = 'val'的元素为当前选中项

$("select\[name=items\] option\[value='val'\]").attr("selected","selected");

radio单选组的第二个元素为当前选中项

$('input\[@name=items\]').get(1).checked = true;
//或
$('input\[name=items\]').attr("checked", '1′);

radio的value = 'val'的元素为当前选中项:

$('input\[name=items\] \[value='val'\]').attr("checked","checked");

文本框text获取值

$("#txt").attr("value");

多选框checkbox获取值

$("input\[name='checkbox':checked\]").each(function(){
var val = $(this).val();
});

单选组radio获取值

$("input\[type=radio\]\[checked\]").val();

下拉框select的value值

$('select').val();

下拉框select选中的text值

$("select").find("option:selected").text();

文本框,文本区域:

$("#txt").attr("value","); //清空内容
$("#txt").attr("value",'11′); //填充内容

多选框checkbox获取值 checkbox的第二个元素被打勾:

$("input\[name=items\]").get(1).checked = true; //打勾
$("input\[name=items\]").get(1).checked = false; //不打勾

checkbox的value='val'的元素前打勾:

$("input\[name=item\]\[value='val'\]").attr("checked",true);
//或
$("input\[name=item\]\[value='val'\]").attr("checked","checked");
if($("input\[name=item\]\[value='val'\]").attr('checked')==true) //判断是否已经打勾

单选组radio获取值

$("input\[type=radio\]").attr("checked",'2′);//设置value=2的项目为当前选中项

下拉框select获取值

$("#sel").attr("value",'-sel3′);//设置value=-sel3的项目为当前选中项
$("<option value='1′>1111</option><option value='2′>2222</option>").appendTo("#sel")//添加下拉框的option
$("#sel").empty();//清空下拉框

jQuery获取Radio选择的Value值

$("input\[name='radio\_name'\]\[checked\]").val(); //选择被选中Radio的Value值
$("#text\_id").focus(function(){//code...}); //事件 当对象text\_id获取焦点时触发
$("#text\_id").blur(function(){//code...}); //事件 当对象text\_id失去焦点时触发
$("#text\_id").select(); //使文本框的Vlaue值成选中状态
$("input\[name='radio\_name'\]\[value='要选中Radio的Value值'").
attr("checked",true); //根据Value值设置Radio为选中状态

jQuery获取CheckBox选择的Value值

$("input\[name='checkbox\_name'\]\[checked\]"); //选择被选中CheckBox元素的集合 如果你想得到Value值你需要遍历这个集合
$($("input\[name='checkbox\_name'\]\[checked\]"));
each(function(){arrChk+=this.value + ',';});//遍历被选中CheckBox元素的集合 得到Value值
$("#checkbox\_id").attr("checked"); //获取一个CheckBox的状态(有没有被选中,返回true/false)
$("#checkbox\_id").attr("checked",true); //设置一个CheckBox的状态为选中(checked=true)
$("#checkbox\_id").attr("checked",false); //设置一个CheckBox的状态为不选中(checked=false)
$("input\[name='checkbox\_name'\]").attr("checked",$("#checkbox\_id").attr("checked"));//根据3,4,5条,你可以分析分析这句代码的意思
$("#text\_id").val().split(","); //将Text的Value值以','分隔 返回一个数组