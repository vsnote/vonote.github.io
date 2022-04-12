---
title: yourphp文章上一篇下一篇代码分享
tags:
  - php
  - Yourphp
  - 代码
  - 学习
  - 开发
id: '52'
categories:
  - - 分享
date: 2013-01-15 20:18:34
---

前两天用Yourphp做一个项目，从优化的角度来考虑，要给文章加上上一篇和下一篇，可偏偏Yourphp里面没有这个标签，无奈只好从网上面搜索，还真让我找到一点有用的东西。 文章页的模版是通过Yourphp>Lib>Action>BaseAction.class.php里面的一个show()方法解析的。 在这个方法里面加上两个变量，我这里用$pre代表上一篇，$next代表下一篇。 为了方便，把代码贴出来。

$pre = M($module)->where("id<$id and catid=$catid")->find();
$next = M($module)->where("id>$id and catid=$catid")->find();
$this->assign('pre',$pre);
$this->assign('next',$next);

这段代码我是放在了分页代码的后面。 还有模版里面的标签引用也一起贴出来吧。

    上一篇：{if $pre}[{$pre\[title\]}]({$pre[url]}){else}木有了{/if}
    下一篇：{if $next}[{$next\[title\]}]({$next[url]}){else}木有了{/if}
    

之上就是全部的代码。