---
title: Dedecms 用 Count 方法实现在模板得到 Arclist 标签的文章总数
tags:
  - dedecms
  - 代码
  - 功能
  - 开发
id: '218'
categories:
  - - 分享
date: 2013-04-10 21:13:55
---

今天碰到了一个比较蛋疼的问题，用dedecms系统做的一个项目，首页用js写的一个类似Tab选项卡切换的功能

> onmouseover="setTab('tab',1,2,'hover');" onmouseover="setTab('tab',2,2,'hover');"

上面红色部分的字，也就是决定有几个切换选项的值。在不知道到底会有几个的情况下如何去写呢。dedecms的arclist标签里面并没有统计调用文章的总数。所以，还是需要自己去扩展。 找到include/common.func.php这个文件，在文件末尾加上一个自定义的函数

> function GetAc($tid){ global $dsql; $sql = GetSonIds($tid); $row = $dsql->GetOne("Select count(id) as acount from @#\_archives where typeid in({$sql})"); return $row\['acount'\]; }

把上面红色的部分换成你的数据库前缀。然后在模板里面调这个方法:

> \[field:typeid function="GetAc(@me)"/\]

OK，这样这得到调用这个分类文章的总数了。