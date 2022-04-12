---
title: ThinkPHP使用技巧经验分享(二)
tags:
  - php
  - PHP框架
  - thinkphp
  - 笔记
id: '773'
categories:
  - - 笔记
date: 2013-08-13 12:37:15
---

循环输出

volist 还有别名 iterate

模版赋值:

$User = D('User')
$list = $User->findAll()
$this->assign('list',$list)

模版定义:

 {$vo.name} 

注意 name 和 id 表示的含义

// 输出 list 的第 5～15 条记录
 {$vo.name} 

// 输出偶数记录
 {$vo.name} 

// 输出 key
 {$k}.{$vo.name} 

//子循环输出
 {$sub.name} 

Switch 标签

 value1
value2
default 

其 中 name 属性可以使用函数以及系统变量，例如：

 admin
default 

也 可以对 case 的 value 属性使用变量，例如：

 admin
member
default 

比较标签

value // name 变量的值等于 value 就输出
value // name 变量的值不等于 value 就输出
value // name 变量的值大于 5 就输出
value // name 变量的值大于等于 5 就输出
value // name 变量的值小于 5 就输出
value // name 变量的值小于等于 5 就输出

//其实上面的所有标签都是 compare 标签的别名
// 其中 type 属性的值就是上面列出的判断标签名称
value // name 变量的值等于 5 就输出

If标签

 value1
value2
 value3 

C操作 操作(动态)配置: 主要用于Action方法里面 获取: C('配置参数') 设置: C('配置参数 ',新值) A操作 快速创建Action对象:

$action = A('User');

等效于

$action = new UserAction();

D操作 快速创建模型数据对象:

$model = D('User');

等效于

$model = new UserModel();

S操作 快速操作缓存方法 获取:

S('name')

设置:

S('name','value');

删 除:

S('name',NULL);

F操作 快速文件数据保存方法 使用方法与S操作一样 L操作 快速操作语言变量 获取: L('语言变量'); 设置: L('语言变量','值'); 如: L('USER\_INFO','用户信息'); //设置名称为USER\_INFO的语言变量 批量赋值: $arr\['语言变量1'\] = '值1'; $arr\['语言变量2'\] = '值2'; L($arr); ThinkPHP系统常量

THINK\_PATH // ThinkPHP 系统目录
APP\_PATH // 当前项目目录
APP\_NAME // 当前项目名称
MODULE\_NAME //当前模块名称
ACTION\_NAME // 当前操作名称
TMPL\_PATH // 项目模版目录
LIB\_PATH // 项目类库目录
CACHE\_PATH // 项目模版缓存目录

CONFIG\_PATH //项目配置文件目录
LOG\_PATH // 项目日志文件目录
LANG\_PATH // 项目语言文件目录
TEMP\_PATH //项目临时文件目录
PLUGIN\_PATH // 项目插件文件目录
VENDOR\_PATH // 第三方类库目录
DATA\_PATH // 项目数据文件目录
IS\_APACHE // 是否属于 Apache
IS\_IIS //是否属于 IIS
IS\_WIN //是否属于Windows 环境
IS\_LINUX //是否属于 Linux 环境
IS\_FREEBSD //是否属于 FreeBsd 环境
NOW\_TIME // 当前时间戳
MEMORY\_LIMIT\_ON // 是否有内存使用限制

MEMORY\_LIMIT\_ON // 是否有内存使用限制
OUTPUT\_GZIP\_ON // 是否开启输出压缩
MAGIC\_QUOTES\_GPC // MAGIC\_QUOTES\_GPC
THINK\_VERSION //ThinkPHP 版本号
LANG\_SET // 浏览器语言
TEMPLATE\_NAME //当前模版名称
TEMPLATE\_PATH //当前模版路径
\_\_ROOT\_\_ // 网站根目录地址
\_\_APP\_\_ // 当前项目（入口文件）地址
\_\_URL\_\_ // 当前模块地址
\_\_ACTION\_\_ // 当前操作地址
\_\_SELF\_\_ // 当前 URL 地址
TMPL\_FILE\_NAME //当前操作的默认模版名（含路径）
WEB\_PUBLIC\_URL //网站公共目录
APP\_PUBLIC\_URL //项目公共模版目录

预定义常量

WEB\_LOG\_ERROR=0 // 错误日志类型
WEB\_LOG\_DEBUG=1 // 调试日志类型
SQL\_LOG\_DEBUG=2 // SQL 日志类型
SYSTEM\_LOG=0 // 系统方式记录日志
MAIL\_LOG=1 // 邮件方式记录日志
TCP\_LOG=2 // TCP 方式记录日志
FILE\_LOG=3 // 文件方式记录日志
DATA\_TYPE\_OBJ=1 // 对象方式返回
DATA\_TYPE\_ARRAY=0 // 数组方式返回
URL\_COMMON=0 // 普通模式 URL
URL\_PATHINFO=1 // PATHINFO URL
URL\_REWRITE=2 // REWRITE URL
HAS\_ONE=1 // HAS\_ONE 关联定义
BELONGS\_TO=2 // BELONGS\_TO 关联定义
HAS\_MANY=3 // HAS\_MANY 关联定义
MANY\_TO\_MANY=4 // MANY\_TO\_MANY 关联定义
EXISTS\_TO\_VAILIDATE = 0 // 表单存在字段则验证
MUST\_TO\_VALIDATE = 1 // 必须验证
VALUE\_TO\_VAILIDATE = 2 // 表单值不为空则验证DATE = 1 // 必须验证
VALUE\_TO\_VAILIDATE = 2 // 表单值不为空则验证