---
title: 怎么开启 ThinkPHP 语言包的功能的方法
link: thinkphp-lang-pack-enable
tags:
  - thinkphp
  - 代码
  - 笔记
id: '850'
categories:
  - - 笔记
date: 2013-09-11 15:00:40
---

**ThinkPHP** 可以很方便的配置**多语言功能**，只需修改一下配置文件就能轻松搞定！

#### 首先在配置文件 config.php 中开启语言包功能：

returnarray{
    'LANG\_AUTO\_DETECT'=> false,//是否自动检测语言
    'LANG\_SWITCH\_ON'=> true,//开启语言包功能
    'DEFAULT\_LANG'=>'cn',//默认语言的文件夹是cn 
}

#### 在配置文件的目录 Conf 目录下新建一个 tags.php 文件

returnarray(
    'app\_begin'=>array(  //因为项目中也可能用到语言行为,最好放在项目开始的地方
        'CheckLang'     //检测语言
    ),
);

#### 在默认语言文件夹下新建一个 common.php 文件

returnarray(
    'site\_name'=>'我的网站',
    'site\_keywords'=>'网站,SEO',
)

现在就可以调用自定义的语言变量了,如果是在 Action 里调用，格式是 L('site\_name')；如果是在模版文件里调用，格式为 {:L('site\_name')}。

> PS:若要是定义针对某个 Action 的语言文件，就在语言包文件夹下新建一个与 Action 同名的 php 文件，这里边定义的语言常量只能在对应的 Action 里应用。