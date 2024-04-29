---
title: 深入了解 Mysql 表引擎优化
link: mysql-engine
tags:
  - mysql优化
id: '1024'
categories:
  - - 分享
date: 2014-08-26 16:07:45
---

# MyISAM：

## 一、优化参数

这个表引擎只存储索引的缓存，而不存储数据的缓存。可以通过设置KEY\_BUFFER\_SIZE设置缓存大小，通过KEY\_BUFER\_BLOCK\_SIZE设置cache block的size。 KEY\_CACHE\_DIVISION\_LIMIT是设置LRU链表中hot area和warm area的分界值，为1-100之间。系统默认为100，也就是只有warm chain。KEY\_CACHE\_DIVISION\_LIMIT告诉mysql该如何将整个cachechain划分为hot area和warm area。 KEY\_CACHE\_AGE\_GHRESHOLD，控制cacheblock从hotarea降级到warmarea的限制，系统默认为300，最小设置为100.值越小，被降级的可能性越大。

### 多key cache的使用

msyql4.1.1开始，myisam支持多个key cache。可以根据不同的需求，设置多个keycache 了。如，将使用非常频繁但是更新操作很少的数据放入一个keycaceh中以防止在公共keycache中被清除出去。那些使用不是很频繁而且经常会更新 的数据放在另外一个keycache中。 mysql官方建议在比较繁忙的系统上使用三个keycache【key cache就是索引缓存】:

*   hotcache：使用20%的大小，用来存放使用非常频繁而且更新少的表索引
*   coldcache：使用20%的大小，用来存放更新很频繁的表索引
*   warmcache：使用剩下的60%空间，作为整个系统的默认keycache。

## 二、预加载

在一个新系统刚上线的时候，系统会因为cache中没有任何数据而出现短时间的负载过高。可以使用预加载机制将指定表的所有索引都加载到内存中。

## 三、null值对统计信息的影响

myisam索引中会记录值为null的列信息，只不过null值的索引键占用的空间 非常少。所以，null会影响到mysql查询优化器对执行计划的选择。于是，mysql提供了MYISAM\_STATS\_METHOD参数让我们自行决 定对索引中的null值的处理方式。如果MYISAM\_STATS\_METHOD=nulls\_unequal，那么myisam在搜集统计信息的时候会认为每个null都是不同的，则给予该字段的索引就会更大，也就是说，myisam会认为distinct的值会更多。MYISAM\_STATS\_METHOD=nulls\_equal则相反。

## 四、并发优化

*   打开concurrent\_insert，如果concurrent\_insert为1，则当表中没有删除记录留下的空余空间时候可以在尾部进行并行插入。concurrent\_insert为2的时候，不管有没有因为删除而留下的空间，都会在尾部进行并行插入。
*   控制写入操作的大小以防止过长的时间拥塞。
*   通过牺牲读取性能来提高写入性能。将写入的优先级提高。

## 五、其他优化

通过optimize命令整理myisam表的文件，是文件占用的空间连续。一般来说，每次做了较大的数据删除操作之后，都要做此命令。

# Innodb：

innodb和myisam最大区别有四点：

*   缓存机制
*   事务支持
*   锁定实现
*   数据存储方式

整体性能上的差异innodb和myisam会因为不同场景而表现出很大差异，正是因为这四点。

## 第一、innodb缓存优化

innodb和myisam的最大区别就是innodb不仅仅缓存了索引，同时还缓存实际的数据。所以，完全相同的数据库，innodb可以使用更多的内存来缓存数据库相关信息。前提是有足够的内存。 innodb\_buffer\_pool\_size设置了InnoDB存储引擎需求最大 的一块内存区域的大小，直接关系到InnoDB存储引擎的性能，所以如果我们有足够的内存，尽可将该参数设置到足够大，将尽可能多的InnoDB的索引及 数据都放入到该缓存区域中，直至全部。 我 们可以通过(Innodb\_buffer\_pool\_read\_requests – Innodb\_buffer\_pool\_reads) / Innodb\_buffer\_pool\_read\_requests \* 100%计算缓存命中率，并根据命中率来调整innodb\_buffer\_pool\_size参数大小进行优化。 innodb\_log\_buffer\_size (global)　　这是InnoDB存储引擎的事务日志所使用的缓冲区。在mysql写入负载很高的情况下，可以增大这个参数来提高IO性能。

## 第二、事务优化

innodb支持的事务隔离级别如下：

*   read uncommited：常被称为脏读
*   read commited：在这一隔离级别下，不会出现dirty read。但是可能会出现non-repeatable read或者phantom read。
*   repeatable read：innodb的默认事务隔离级别。不会出现dirty read。也不会出现non-repeatable read，但是可能会出现phantom read。
*   serializable：serializable是标准事务隔离级别中的最高级。在事务中的任何时候看到的数据都是事务启动时候的状态。不论这期间是不是有其他事务已经修改了某些数据并提交。所以，在serializable下，phantom reads也不会出现。

innodb在修改数据的时候，只是修改buffer pool中的数据。并不是在一个事物提交之后就将buffepool中的数据同步到磁盘上。这里要理解连续读写和随机读写。写入磁盘的 过程是需要磁头寻址的。连续读写是指将要写入的东西写入到一个连续地址空间。innodb不是每一次都将数据同步到磁盘，就是为了攒多数据之后，进行连续 读写来减少磁盘IO。 系统崩溃之后，innodb是如何利用事务日志进行数据恢复的呢？ 假设在某一时间，mysql crash了，那么，所有的bufferpool的数据都会丢失。包括已经修改了但是没来得及刷新到磁盘上的数据。在mysql从crash之后再次启 动，innodb会通过比较事务日志中的所有记录的checkpoint的信息和各个数据文件中的checkpoint信息，找到最后一次 checkpoint所对应的log sequence number。然后通过事务日志中的变更记录，将从崩溃之前最后一次checkpoint往后的所有变更重新应用一次。同步所有的数据文件到一致状态。当 然，对于logbuffer中未来得及同步到日志文件的变更数据，就再也无法找回了。总的来说，事务日志文件设置的越大，系认io性能越好，但是遇到 crash，那么恢复的时间也越长。 innodb\_flush\_log\_at\_trx\_commit默认设置为1，表示每 次失误的结束都会触发log thread将logbuffer中的数据写入文件，并通知文件系统同步文件。这个设置是安全的，能够保证不论是mysql crash，还是os崩溃，还是主机断电，都不会丢失任何已经提交的数据。

## 三、数据存储优化

innodb的聚簇主键已经了解了。但是聚簇主键也是有不好的地方的，不然其他数据库厂商也大力推广了。聚簇的最大问题就是索引键被更新造成的成本，并不只是索引数据可能会移动，而是相关的所有记录数据都要移动。所以，为了性能考虑，尽量不要更新innodb的主键值。 innodb中的数据，不论是表 还是索引，或者是存储引擎的各种数据结构，都以page作为最小物理单位来存储。每个page大小默认16K。extent由多个连续的page组成的一 个物理存储单位。一般来说每个extent64个page。每个segment有一个或者多个extent组成。每个segment都存放同一种数据。一 般来说，每个表都会存放在一个单独的segment中。 page>extent>segment>tablespace，后面的每一个都是由前面的一个或者多个组成。tablespace是innodb的最大结构单位。 在主键上的优化建议，

*   为了减小secondary index的大小，主键字段所占用的存储空间越小越好。最好是integer。当然这并不绝对。
*   尽可能不要做主键的更新。
*   尽可能根据主键进行查询操作。

## 四、其他优化

autocommit相信都了解，根据自己的实际情况设置autocommit。