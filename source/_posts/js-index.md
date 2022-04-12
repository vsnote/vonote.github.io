---
title: 前端性能优化技巧 - 使用索引对象
tags:
  - javascript
  - js
  - 优化
  - 前端
id: '554'
categories:
  - - 笔记
date: 2013-07-02 23:50:35
---

AJAX和JSON一个最常见的使用案例是接收包含一组对象的数组，然后从这组数组中根据给定的值搜索对象。让我们看一个简单的例子，下面这个例子中，你从用户接收一个数组，然后你可以根据username的值来搜索用户对象：

function getUser(desiredUsername) {
    var searchResult = ajaxResult.users.filter(function(user) {
        return user.username == desiredUsername;
    });
 
    return searchResult.length ? searchResult\[0\] : false;
}
 
// 根据用户名获取用户
var davidwalsh = getUser("davidwalsh");
 
// 根据用户名获取另一个用户.
var techpro = getuser("tech-pro");

上面这段代码可以运行，但是并不是很有效，当我们想要获取一个用户时，我们就要遍历一次数组。那么更好的方法是创建一个新的对象，对每一个唯一的值建立一个索引，在上面这个例子中，用username作为索引，这个数组对象可以写成：

var userStore = {};
ajaxResult.users.forEach(function(user) {
    userStore\[user.username\] = user;
});

现在当你想要找一个用户对象时，我们可以直接通过索引找到这个对象：

var davidwalsh = userStore.davidwalsh;
var techpro = userStore\["tech-pro"\];

这样的代码写起来更好一些，也很简便，通过索引搜索比起遍历整个数组更加快捷。