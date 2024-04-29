---
title: ThinkPHP使用技巧经验分享(一)
link: thinkphp-tips-1
tags:
  - php
  - PHP框架
  - thinkphp
  - 二次开发
  - 代码
  - 程序
id: '722'
categories:
  - - 笔记
date: 2013-08-01 15:06:43
---

找了一些使用THinkPHP的心得和技巧,分享给大家 约定: 1.所有类库文件必须使用.class.php作为文件后缀,并且类名和文件名保持一致 2.控制器的类名以Action为后 缀 3.模型的类名以Model为后缀,类名第一个字母须大写 4.数据库表名全部采用小写, 如: 数据表名: 前缀\_表名 模型类名: 表名Model 注:这里的表名第一个字母要大写 创建对象: D('表名') 注:这里的表名第一个字母要大写 定义控制器类

class IndexAction extends Action{
    public function show(){
        echo '这是新的 show 操作';
    }
}

然后在浏览器里面输入

> http://localhost/myApp/index.php/Index/show/

定义模型类:

class 表名Model extends Model{
    \[//手动定义字段\[可选\]
    protected $fields = array(
    'id',
    'username',
    'email',
    'age',
    '\_pk'=>'id', //主键
    '\_autoInc'=>true //是否自增)\]
}

记录的修改:

$User = D("User") // 实例化 User 对象
$User->find(1) // 查找 id 为 1 的记录
$User->name = 'ThinkPHP' // 把查找到的记录的名称字段修改为 ThinkPHP
$User->save() // 保存修改的数据

更新特定字段的值

$User->setField('name','TopThink','id=1')

同 样可以支持对字段的操作

$User->setField('score','(score+1)','id=1')

新建记录,方法1:

$User = new UserModel() //实例化 User 对象
$User->字 段名 = 字段值 //给字段赋值
$User->add() //添加记录

新建记录,方法2:

$data\['字段名'\] = 字段值; //给字段赋值
$User = D('User'); //实例化 User 对象
$User->add($data); //$insertId,Add 方法的返回值就是最新插入的主键值，可以直接获取。

新增多条记录:

$User = new UserModel()
$data\[0\]\['name'\] = 'ThinkPHP'
$data\[0\]\['email'\] = 'sjolzy@chen.com'
$data\[1\]\['name'\] = '流年'
$data\[1\]\['email'\] = 'chen@sjolzy.cn'
$User>addAll($data)

删除记录

$User->find(2)
$User->delete() // 删除查找到的记录
$User->delete('5,6') // 删除主键为 5、6 的数据
$User->deleteAll() // 删除查询出来的所有数据

记录查询

$User->getDbFields() //获取当前数据字段
$User->findAll(); //查找所有记录
$User->findAll('1,3,8') //查询主键为1,3,8的记录集
$User->count() // 获取记录数
$User->max('score') // 获取用户的最大积分
$User->min('score','score>0') // 获取积分大于 0 的用户的最小积分
$User->avg('字段名') // 获取所有记录的字段值的平均值
$User->sum('字段名 ') // 统计字段值

（以下方法的使用需继承高级模型类）

$User->getN(2,array('score>80')) // 返回符合条件的第 2 条记录
$User->getN(-2,array('score>80')) //还可以获取最后第二条记录
$User->first(array('score>80','score desc')) //如果要查询第一条记录，还可以使用
$User->last(array('score>80','score desc')) // 获取最后一条记录
$User->top(5,array('score desc')) // 获取积分最高的前 5 条记录
$User->getBy('name','liu21st') //跟据字段的字段值来查询记录

$Model = new Model() // 实例化一个 model 对象 没有对应任何数据表
$Model->query("select \* from think\_user where status=1")//直接使用原生的sql语句

$objrs = $Model->query("select \* from think\_user where status=1") //自定义查询
$Model->execute("update think\_user set name='thinkPHP' where status=1") //用于更新和写入数据的 sql 操作，返回影响的记录数

$User->startTrans() // 启动事务
$User->commit() // 提交事务
$User->rollback() // 事务回滚

模板:

$this->assign('name',$value); //在 Action 类里面使用 assign 方法对模板变量赋值，无论何种变量类型都统一使用 assign 赋值
$this->display() // 输出模版文件

批量赋值，assign的单参数使用

$array\['name'\] = 'thinkphp'
$array\['email'\] = 'chen@sjolzy.cn'
$array\['phone'\] = '12335678'
$this->assign($array)
$this->display() // 调用 User 模块的 read 操作模版
$this->display('edit') // 调用 User 模块的 edit 操作模版
$this->display('Member:read') // 调用 Member 模块的 read 操作模版
$this->display('Xp@User:edit') // 调用 Xp 主题的 User 模块的 edit 操作模版
$this->display('../Member/read.html') // 直接指定模版文件的全名

模板标签:

{ } 或 {// 注释内容 } //模板注释
{$user\['name'\]} //输出数组变量
{$user:name} //输出对象的属性

为了方便模板定义，无论输出的模板变量是数组还是对象，都可以用下列统一方式输出： {$user.name} 如果是多维数组或者多 层对象属性的输出，请使用下面的定义方式： {$user\['sub'\]\['name'\]} {$user:sub:name} 在模板中使用函数: 格式：{$varnamefunction1function2=arg1,arg2,### } 或者 {:function(参数1，参数2)} 说明： { 和 $ 符号之间不能有空格 ，后面参数的空格就没有问题 ###表示模板变量本身的参数位置 系统变量

{$Think.server.script\_name } //取得$\_SERVER 变量
{$Think.session.session\_idmd5 } // 获取$\_SESSION 变量
{$Think.get.pageNumber } //获取$\_GET 变量
{$Think.cookie.name } //获取$\_COOKIE 变量

系统常量

{$Think.const.\_\_FILE\_\_ }
{$Think.const.MODULE\_NAME }
特殊变量 ，由 ThinkPHP 系统定义的常量
{$Think.version } //版本
{$Think.now } //现在时间

快捷输出（3.0及以后版本已去掉）

{:function(…)} //执行方法并输出返回值
{~function} //执行方法不输出
{@var} //输出 Session 变量
{&var} //输出配置参数
{%var} //输出语言变量
{.var} //输出 GET 变量
{^var} //输出 POST 变量
{\*var} //输出常量

包含外部文件

 // 用变量控制要导入的模版
 // 使用一个完整的文件名包含

注意：不能变量与字符串混用，如： //这样是错误的