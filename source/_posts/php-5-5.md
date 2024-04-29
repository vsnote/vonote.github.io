---
title: PHP 5.5 正式发布，不支持XP和2003?
link: php-5-5
tags:
  - php
id: '527'
categories:
  - - 软件
date: 2013-06-22 10:19:34
---

PHP 开发者正式 发布 5.5 版本，该版本从去年11月开始开发，历经多个测试版本。PHP 5.5 包含一系列的新特性，例如新的 array\_column() 函数以及 foreach() 循环支持标量迭代键；包括 generators 允许开发者实现简单的协程。 同时新版本引入了一个密码哈希函数，可以让开发者轻松实现加盐的安全密码；新增 finally 关键字；foreach 结构支持 list() 构建；其他改进包括 opcode 缓存、代码优化、Zend Optimizer+ 等等，这些对不会对已有代码造成影响，主要是提升语言的性能和稳定性。 新的密码哈希 API 使用了 Bcrypt 方法，示例如下：

$hash = password\_hash($password, PASSWORD\_DEFAULT);

校验方法：

password\_verify($password, $hash);

同时 PHP 开发者也提醒用户，PHP 5.5 也包含一些不向后兼容的内容，包括：不再支持 Windows XP 和 2003 系统；不区分大小写的匹配函数、类；常数名称跟 Locale 无关，这对一些使用非 ASCII 代码的常量名的开发者需要注意的。完整的关于 PHP 5.5 不向后兼容列表请看 [list of new features and possible incompatibilities](http://www.php.net/manual/en/migration55.incompatible.php) PHP 5.5 的完整改进记录请看 [NEWS file](https://github.com/php/php-src/blob/php-5.5.0/NEWS)

#### 下载地址

[Windows版本](http://windows.php.net/qa/) [Linux版本](http://php.net/downloads.php#v5)