---
title: 局域网利用 nc 传输文件
tags:
  - linux
  - 工具
id: '1244'
categories:
  - - 分享
date: 2018-01-24 18:00:40
---

操作系统：ubuntu； 操作方式：命令行； 接收端：nc -l -p port > filename 发送端：nc destination\_ip destination\_port < filename 实例： 接收端：nc -l -p 10000 > test.txt 发送端：nc 192.168.0.105 10000 < test.txt 注意事项：先接收端操作，接收端监听后，发送端再发送文件；