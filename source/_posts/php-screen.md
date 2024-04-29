---
title: PHP 实现即时网站截图
link: php-screen
tags:
  - HTML
  - php
id: '819'
categories:
  - - 分享
date: 2016-03-31 09:51:22
---

转一个通过PHP实现即时网站截图功能 通过一个表单来提交请求

    网站地址 (不带 http://):
    大小:
    px
    px
    图片格式:
    PNG
        JPEG 

处理页面

';
    echo '» **点击图片下载截图！**  
[![](' . $iurl . ')](' . $iurl . ')  
';
} else {
    header("Content-type: {$imt}");
    header("Content-Disposition: attachment; filename= {$ifn}");
    readfile($surl);
}