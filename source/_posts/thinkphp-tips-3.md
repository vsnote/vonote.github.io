---
title: ThinkPHP使用技巧经验分享(三)
link: thinkphp-tips-3
tags:
  - php
  - PHP框架
  - thinkphp
  - 二次开发
  - 代码
  - 学习
  - 笔记
id: '790'
categories:
  - - 笔记
date: 2013-08-20 15:33:03
---

## add方法返回主键（id）的值

在往数据表中添加数据时调用 `add` 方法，默认返回值就是刚添加的 id 值，就不用再去查询了.

## save方法返回值的判断

在修改数据时，如果修改成功返回的是被修改的记录数 0，1，2，3...... 注意：以下几种情况返回 `false`，所以判断更新失败应使用 `if(false === $this->save())` (1)更新的数据为空 (2)_before_update() 方法返回 false (3)没有任何更新条件(没有定义 where() 里的条件，或者保存的数据里没有主键的值)

## 查询后置方法详解

如 `_after_select`,`_after_insert`,`_after_update`,`_after_delete`,`_after_find等` 巧妙地利用这些方法可以简化开发。
用 `_after_select(&$result,$options)` 举例： 参数：`$result`，这是 `select` 出的结果数组。
注意这里是一个引用传参，也就是说我们可以直接改变传递过来的值而不需要返回 `$options`,这是查询的条件，也就是`where()`里面的条件 假如你查询出的数据有 `time` 这一字段，并且是以 `int` 型保存的，那么可以在这个方法里进行时间格式化的操作

```php
protected function _after_select(&$result,$options) {
      foreach($result as $key=>$value){
          $result[$key]['time'] = date('Y-m-d H:i:s', $value['time']);
      }
}
```

这样就不需要每次在模板上显示的时候，再用函数来处理了。 同样地，可以用 `_after_insert` 来代替关联操作，在新增完一条数据后再根据参数更新一些关联的数据。 当然，除了后置方法，还有前置方法。可以用来代替一些复杂的数据验证或者进行数据的预处理，类似于自动完成和自动验证。

```php
protected function _before_insert(&$data,$options) {
    //对新增前的数据进行处理
    foreach ($data as $key=>$value){
        $value['status'] = 1;//类似于自动完成
        if($value['age'] > 100){//类似于自动验证
            return false;
        }
    }
}
```

最后，有几点需要注意的：

*   这些方法都是必须写在 model 里面的
*   这些方法所接收的参数，有些是引用传参，有些是传值，得注意区分。具体可参考手册
*   在后置方法里不需要返回值。而前置方法里可以返回 false 来阻止进行下一步的操作

## 打印sql语句

```php
$User = D('User');
$User->select();
echo $User->getLastSql();或者echo $User->_sql();
```

获取最后执行的sql语句，方便查看调试

## 跨模板主题调用模板

假如 Tpl 下有 new 主题，该主题下有 User 文件夹，文件夹下有 `index.html` 你当前的模板主题是 Tpl 下的 default，那么可以用 `$this->display('new:User:index');` 或者用全路径输出 `$this->display('./Tpl/new/User/index.html');`

## 路由规则^符号的使用

这个符号在手册中没有提及，但是作用却不可忽视。 用法：`'user/^getlisttag' => 'user/index'` 作用：在 `user` 模块中，除了 `getlist` 和 `tag` 方法，其他存在的方法全部指向 `index` 方法。参数之间用 间隔 这样可以屏蔽一些不想让用户访问到但是又必须定义成 `public` 的方法。

> 引用地址：http://www.thinkphp.cn/document/236.html