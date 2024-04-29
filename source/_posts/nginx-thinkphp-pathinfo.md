---
title: 解决 nginx 服务器不支持 ThinkPHP 框架 pathinfo 的解决办法
link: nginx-thinkphp-pathinfo
tags:
  - nginx
  - php
  - thinkphp
id: '854'
categories:
  - - 笔记
date: 2013-09-12 10:32:22
---

最近在用 **ThinkPHP** 做一个项目，基本完成后部署到 nginx 服务器上才发觉 nginx 是不支持 pathinfo 的，网上搜索了别人的解决方法，有两种思路： 1、修改 ThinkPHP 让他可以在 nginx 上运行 2、修改 nginx 让它支持 pathinfo 网上说 nginx 开启 pathinfo 是有一定风险的，能不用 pathinfo 最好不用，所以还是折腾 ThinkPHP 吧，个人觉得这种方法相对第2种方法来得简单。 修改 nginx 的 rewrite

location / { 
    if (!-e $request\_filename) { 
        rewrite ^(.\*)$ /index.php?s=$1 last; 
        break; 
    } 
}

然后项目配置下 url 模式改为2

'URL\_MODEL'=>2,

如果是多个项目，布署项目时要把项目布署到目录里，如后台的项目放到 Admin 目录里，那么在 nginx 的 rewrite 里再写一条

location /Admin/ { 
    if (!-e $request\_filename) { 
        rewrite ^/Admin/(.\*)$ /Admin/index.php?s=$1 last; 
        break; 
    } 
}

最后也不要忘记把这个项目的 url 模式改为2。