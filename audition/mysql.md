# mysql

# 1 MySQL体系结构和存储引擎
## 1.1 定义数据库和实例
* 数据库：物理操作系统文件和其他形式文件类型的集合
* 实例：MySQL数据库由后台线程及一个共享内存区组成

## 1.2 

# 2 InnoDB 存储引擎
## 2.1 InnoDB 存储引擎概述

## 2.2 InnoDB 存储引擎的版本

## 2.3 InnoDB 体系结构
### 2.3.1 后台线程
1.Master Thread：主要负责将缓冲池中的数据异步刷新到磁盘，保证数据的一致性 
2.IO Thread     :write,read,insert buffer,log io thread     
3.Purge Thread  :undo log回收
4.Page Cleaner Thread： 脏页刷新操作

### 2.3.2 内存
1.缓冲池 缓冲池中缓存的数据页类型有：索引页，数据页，undo页，插入缓冲，自适应哈希索引，InnoDB存储的锁信息，数据字典信息等
2.LRU List，Free List，Flush List
3.重做日志缓冲
4.额外的内存池

## 2.6 InnoDB关键特性
### 2.6.1 插入缓冲 性能上的提升
1. Insert Buffer
2. Change Buffer
需要满足两个条件:a. 索引是辅助索引;b. 索引不是唯一的
3. Insert Buffer的内部实现


### 2.6.2 两次写 数据的可靠性

### 2.6.3 自适应哈希索引
### 2.6.4 异步IO
### 2.6.5 刷新邻接表

## 5.1 InnoDB 存储引擎索引概述
1. B+树索引
2. 全文索引
3. 哈希索引

## 5.2 数据结构与算法
### 5.2.1 二分查找法
### 5.2.2 二叉查找树和平衡二叉树

## 5.3 B+树
### 5.3.1 B+树的插入操作
### 5.3.2 B+树的删除操作
## 5.4 B+树索引
### 5.4.1 聚集索引


# mysql 常问面试题目