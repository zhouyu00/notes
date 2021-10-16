# redis

## 1. Redis缓存穿透，缓存击穿，缓存雪崩原因及解决方案
1. 缓存穿透：redis和数据库均不存在某key，每次请求都到数据源
    解决方法：1.布隆过滤器；2.短期缓存key-null在redis；3.接口层校验
2. 缓存击穿：key对应的数据存在，但在redis中过期，此时若大量并发请求过来，会请求数据源，瞬间把后端击垮
    解决方法：1.使用互斥锁
3. 缓存雪崩：当缓存服务器重启，或者大量key在同个时段失效。
    解决方法：1.失效时间增加随机值；2.分布式部署时，热点数据分散缓存；3.设置热点数据永远不过期

### 布隆过滤器
https://www.cnblogs.com/liyulong1982/p/6013002.html

## 2. redis 持久化策略 RDB,AOF
https://baijiahao.baidu.com/s?id=1654694618189745916&wfr=spider&for=pc

## 3. redis 淘汰策略
https://www.cnblogs.com/leeego-123/p/12577136.html



# kafka


# redis 设计与实现
## 2 简单动态字符串SDS
### 2.1 SDS的定义
```
struct sdshdr{
    //记录buf数组中已经使用的字节的数量
    //等于SDS所保存的字符串的长度
    int len;
    //记录buf数组中未使用的字节的数量
    int free;
    //字节数组，用户保存字符串
    char buf[];
}
```

### 2.2 SDS与字符串的区别
#### 2.2.1 常数复杂度获取字符串长度
#### 2.2.2 杜绝缓冲区溢出
#### 2.2.3 减少修改字符串带来的内存重分配次数
#### 2.2.4 二进制安全
#### 2.2.5 兼容部分C字符函数

## 3 链表
```
typedef struct listNode{
    //前置节点
    struct listNode *prev;
    //后置节点
    struct listNode *next;
    //节点的值
    void *value;
}listNode;

typedef struct list{
    //表头节点
    listNode *head;
    //表尾节点
    listNode *tail;
    //链表所包含的节点数量
    unsigned long len;
    //节点值复制函数
    void *(*dup)(void *ptr);
    //节点值释放函数
    void *(*free)(void *ptr);
    //节点值对比函数
    int (*match)(void *ptr,void *key);
} list;
```

## 4 字典
### 4.1字典的实现
#### 4.1.1 哈希表
```
typedef struct dictht{
    //哈希表数组
    dictEntry **table;
    //哈希表大小
    unsigned long size;
    //哈希表大小掩码，用于计算索引值
    //总是等于size-1
    unsigned long sizemask;
    //该哈希表已有节点的数量
    unsigned long used;
}dictht;
```
#### 4.1.2 哈希表节点
```cpp
typedef struct dictEntry{
    //键
    void *key;
    //值
    union{
        void *key;
        uint64_t u64;
        int64_t s64;
    } v;
    struct dictEntry *next;
} dictEntry;
```

#### 4.1.3 字典
```
typedef struct dict{
    //类型特定函数
    dictType *type;
    //私有数据
    void *privdata;
    //哈希表
    dict ht[2];
    //rehash索引
    //当rehash不在进行时，值为-1
    int trehashidx;
}

typedef struct dictType{
    //计算哈希值的函数
    unsigned int (*hashFunction)(const void *key);
    //复制键的函数
    void *(*keyDup)(void *privdata,const void *key);
    //复制值的函数
    void *(*valDup)(void *privdata,const void *Obj);
    //对比键的函数
    void (*keyCompare)(void *privdata,const void *key1,const void *key2);
    //销毁键的函数
    void (*keyDestructor)(void *privdata, void *key);
    //销毁值的函数
    void (*valDestructor)(void *privdata,void *obj);
}
```

### 4.2 哈希算法
### 4.3 解决键冲突
### 4.4 rehash
** 哈希表的扩张与收缩
当下面的条件满足时，哈希表进行扩展为2*ht[0].used
1) 服务器目前没有在执行BGSAVE命令或者BGREWRITEAOF命令，并且哈希表的负载均衡大于等于1
2) 服务器目前正在执行BGSAVE命令或者BGREWRITEAOF命令，并且哈希表的负载因子大于等于5

当哈希表的负载因子小于0.1时，程序自动开始对哈希表执行收缩操作
### 4.5 渐进式rehash

## 5 跳跃表
### 5.1 跳跃表的实现

#### 5.1.1 跳跃表结点
```
typedef struct zskiplistNode{
    //后退指针
    struct zskiplistNode *backward;
    //分值
    double score;
    //成员对象
    robj *obj;
    //层
    struct zskiplistLevel{
        //前进指针
        struct zskiplistNode *forward;
        //跨度
        unsigned int span;
    }level[];
}zskiplistNode;
```
1. 层

#### 5.1.2 跳跃表
```
typedef struct zskiplist{
    //表头结点和表尾结点
    struct skiplistNode *header, *tail;
    //表中节点的数量
    unsigned long length;
    //表中层数最大的节点层数
    int level;
}zskiplist;
```

## 6 整数集合
### 6.1 整数集合的实现
```
typedef struct intset{
    //编码方式
    uint32_t encoding;
    //集合包含的元素数量
    uint32_t length;
    //保存元素的数组
    int8_t contents[];
}intset;
```

### 6.2 升级
升级步骤
1. 根据新的元素类型，扩展整数集合底层数组空间大小，并为新元素分配空间
2. 将底层数组现有的所有元素转换成与新元素相同的类型，并将类型转换后的元素放在正确的位置上
3. 将新元素添加到底层数组中

### 6.3 升级的好处
#### 6.3.1 提升灵活性
#### 6.3.2 节省内存
### 6.4 降级
不支持降级

## 7 压缩列表
### 7.1 压缩列表的构成
|zlbytes|zltail|zllen|entry1|...|entryN|zlend|

### 7.2 压缩列表节点的构成
|previous_entry_length|encoding|content|

#### 7.2.1 previous_entry_length
1字节或者5字节

#### 7.2.2 encoding
* 一字节，两字节或者五字节长，值的最高位为00，01，10的是字节数组编码
* 一字节长 值的最高位以11开头的是整数编码

#### 7.2.3 content

### 7.3 连锁更新

## 8 对象
### 8.1 对象的类型与编码
```
typedef struct redisObject{
    //类型
    unsigned type:4;
    //编码
    unsigned encoding:4;
    //指向底层实现数据结构指针
    void *ptr;
    //...
}
```
#### 8.1.1 类型

#### 8.1.2 编码和底层实现

### 8.2 字符串对象
1. 如果字符串对象保存的是整数，并且这个整数可以用long类型来表示，那么字符串对象会使用int实现
2. 如果字符串对象保存的是一个字符串值，并且字符串长度大于39字节，那么使用SDS实现
3. 如果字符串对象保存的是字符串值，并且字符串值小于39字节，那么使用embstr编码实现

embstr实现的好处有：
1. 一次内存分配，
2.一次内存释放
3.保存在一块连续的内存里，能更好的利用缓存的优势

注意：
long double 类型的保存在redis里也是作为字符串来保存的

#### 8.2.1 编码的转换

#### 8.2.2 字符串命令的实现

### 8.3 列表对象
#### 8.3.1 编码转换
当列表对象同时满足下面两个条件时，列表对象使用ziplist编码：
* 列表对象保存的所有字符串对象的长度都小于64字节
* 列表对象保存的元素数量小于512个；不能满足这两个条件的列表对象需要使用linkedlist编码

### 8.4 哈希对象
#### 8.4.1 编码转换
当列表对象同时满足下面两个条件时，列表对象使用ziplist编码：
* 列表对象保存的所有字符串对象的长度都小于64字节
* 列表对象保存的元素数量小于512个；不能满足这两个条件的列表对象需要使用ziplist编码

#### 8.4.2 哈希命令的实现

### 8.5 集合对象

#### 8.5.1 编码的转换
当集合对象可以满足以下两个条件时，对象使用intset编码
* 集合对象保存的所有元素都是整数值
* 集合对象保存的所有元素数量不超过512个

#### 8.5.2 集合命令的实现

### 8.6 有序集合的实现
#### 8.6.1 编码的实现
当有序集合满足以下两个条件时，使用ziplist编码：
* 有序集合保存的元素数量小于128个
* 有序集合保存的所有元素成员长度都小于64字节

#### 8.6.2 有序集合命令的实现

## 8.7 类型检查与命令多态
* 对任何类型的键都可执行的命令DEL,EXPIRE,RNAME,TYPE,OBJECT
* 对特定类型的键执行
1. SET,GET,APPEND,STRLEN等只能对字符串键执行
2. HDEL,HSET,HGET,HLEN等只能对哈希键执行
3. RPUSH,LPOP,LINSERT,LLEN等只能对列表键执行
4. SADD,SPOP,SINTER,SCARD等只能对集合键执行
5. ZADD,ZCARD,ZRANK,ZSCORE等只能对有序集合键执行

#### 8.7.1 类型检查的实现
类型检查命令所进行的类型检查是通过redisObject结构的type属性来实现的：
* 在执行一个类型特定命令之前，服务器会先检查输入数据库键的值对象是否为执行命令所需的类型
* 否则，服务器将拒绝执行命令，并向客户端返回一个类型错误

#### 8.7.2 多态命令的实现
基于类型的多态->基于编码的多态

### 8.8 内存回收
refcount
引用计数

### 8.9 对象共享


### 8.10 对象的空转时长
unsigned lru
空转时长=当前时间-值对象的lru时间

## 二 单机数据库的实现
## 9 数据库
### 9.1 服务器中的数据库
```
struct redisServer{
    //...
    //一个数组保存着服务器中的所有数据库
    redisDb *db;
    //服务器的数据库数量
    int dbnum;
    //...
}
```
### 9.2 切换数据库
默认情况下，redis客户端的目标数据库为0号数据库，但是客户端可以通过SELECT命令来切换目标数据库
```
typedef struct redisClient{
    //记录客户端指向的数据库
    redisDb *db;
}
```
### 9.3 数据库键空间
redis是一个键值对，服务器中的每个数据库都由一个redisDb保存数据库中的所有键值对：
```
typedef struct redisDb{
    //数据库键空间，保存着数据库中的所有键值对
    dict *dict;
}
```
#### 9.3.1 添加新键

#### 9.3.2 删除键

#### 9.3.3 更新键

#### 9.3.4 对键取值

#### 9.3.5 其他键空间操作

#### 9.3.6 读写键空间的维护操作
* 读取一个键后，会根据键是否存在来更新服务器中的键空间命中次数和不命中次数
* 更新LRU时间
* 如果有客户端使用WATCH命令监视了某个键，服务器修改键之后会将键标记为dirty
* 每次修改一个键后dirty键计数器加1，计数器会触发服务器的持久化及复制操作
* 如果开启了数据库通知功能，那么对键修改之后，服务器将按配置发送响应的数据库通知

### 9.4 设置键的生存时间或过期时间 
TTL key 获取key的生存时间
PTTL key

#### 9.4.1 设置过期时间
EXPIRE key
PEXPIRE key 毫秒为单位
EXPIREAT key
PEXPIREAT key

#### 9.4.2 保存过期时间
typedef struct redisDb{
    //...
    //过期字典，保存着键的过期时间
    dict *expires;
} redisDb;

#### 9.4.3 移除过期时间
PERSIST key

#### 9.4.4 计算并返回剩余生存时间
TTL key

#### 9.4.5 过期键的判定
1)检查给定键是否存在于过期字典
2)检查当前UNIX时间是否大于键的过期时间

### 9.5 过期键删除策略
1.定时删除
2.惰性删除
3.定期删除

#### 9.5.1 定时删除
1. 内存友好
2. 占用大量的CPU时间
3. 实现困难

#### 9.5.2 惰性删除
1. 对CPU时间友好，对内存不友好
2. 造成内存泄露

#### 9.5.3 定期删除
1.

难点：确定删除操作执行的时长和频率

### 9.6 Redis的过期键删除策略

#### 9.6.1 惰性删除策略的实现
1. 所有读写数据库的

#### 9.6.2 定期删除策略的实现
1. 函数每次运行的时候从数据库里取出一定数量的随机键进行检查，并删除其中的过期键
2. 全局变量current_db会记录当前函数检查的进度
3. 随着activeExpireCycle函数的不断执行，服务器中所有的数据库都会被检查一遍

### 9.7 AOF，RDB和复制功能对过期键的处理
#### 9.7.1 生成RDB文件
不会保存过期的键
#### 9.7.2 载入RDB文件
* 主服务器模式不会载入过期键
* 从服务器模式全部载入

#### 9.7.3 AOF文件写入
当过期键被惰性删除或者定期删除后，程序会向AOF文件追加一条DEL命令

#### 9.7.4 AOF重写
执行AOF重写的过程中，已经过期的键不会保存到AOF文件中

#### 9.7.5 复制
当服务器运行在复制模式下时，从服务器的过期键删除动作由主服务器控制：
* 主服务器在删除一个过期键之后，会显式地向所有从服务器发送一个DEL命令，通知从服务器删除这个过期键
* 从服务器在执行客户端发送的读命令中，即使碰到过期键也不会删除
* 只有收到了主服务器的DEL命令后才删除过期键

### 9.8 数据库通知
1. 键空间通知
2. 键事件通知

#### 9.8.1 发送通知
void notifyKeyspaceEvenet(int type,char *event,robj *key,int dbid);

#### 9.8.2 发送通知的实现

## 10 RDB持久化
### 10.1 RDB文件的创建与载入
* 创建 SAVE/BGSAVE
* 载入 启动时检测RDB文件
因为AOF的更新频率比RDB文件更高：
* 如果服务器开启了AOF持久化功能，那么服务器会优先使用AOF文件来还原数据
* 只有AOF持久化功能处于关闭状态时，服务器才会使用RDB文件来还原数据库

#### 10.1.1 SAVE命令执行时的服务器状态
执行SAVE命令时，客户端发送的而所有命令阻塞

#### 10.1.2 BGSAVE命令执行时的服务器状态
1. 执行BGSAVE期间 SAVE和BGSAVE 都会被服务器拒绝，避免产生竞争条件
2. BGREWRITEAOF和BGSAVE两个命令不能同时执行


#### 10.1.3 RDB文件载入时的服务器状态
RDB文件载入期间，服务器一直处于阻塞状态

### 10.2 自动间隔性保存
#### 10.2.1 设置保存条件
#### 10.2.2 dirty计数器和lastsave属性
|REDIS|db_version|databases|EOF|check_sum|

### 10.3 RDB文件结构
#### 10.3.1 databases部分
|SELECTDB|db_number|key_value_pairs|

#### 10.3.2 key_value_pairs部分
不同的键值对由TYPE，key，value三部分组成
程序根据TYPE的值来决定如何读入和解释value的数据

|TYPE|key|value|

带有过期时间时间的键值对
|EXPIRETIME_MS|ms|TYPE|key|value|

#### 10.3.3 value的编码
1. 字符串对象 REDIS_RDB_TYPE_STRING
字符串对象的编码:
保存整数：|ENCODING|integer|
保存字符串：
未压缩|len|string|
压缩|REDIS_RDB_ENC_LZF|compressed_len|orgin_len|compressed_string|

2. 列表对象 REDIS_RDB_TYPE_LIST
|list_length|item1|item2|...|itemN|

3. 集合对象 REDIS_RDB_TYPE_SET
|set_size|elem1|elem2|...|

4. 哈希表对象 REDIS_RDB_TYPE_HASH
|hash_size|key_value_pair_1|key_value_pair_2|...|

5. 有序集合对象
|sorted_set_size|element1|element2|...|elementN|

6. INTSET编码的集合
整数集合转换成字符串对象

7. ZIPLIST编码的列表、哈希表或者有序集合
压缩列表转换成字符串对象进行存储

### 10.4 分析RDB文件
#### 10.4.1 不包含任何键值对的RDB文件

#### 10.4.2 包含字符串键的RDB文件

#### 10.4.3 包含带有过期时间的字符串键的RDB文件

#### 10.4.4 包含一个集合键的RDB文件

#### 10.4.5 关于分析RDB文件的说明

1.redis-check-dump
2.od -cx dump.rdb

### 10.5 重点回顾

## 11 AOF持久化
### 11.1 AOF持久化的实现
#### 11.1.1 命令追加
```
struct redisServer{
    //...
    //AOF缓冲区
    sds aof_buf;
    //...
}
```
#### 11.1.2 AOF文件的写入与同步
appendfsync ：always/everysec/no 默认为everysec

### 11.2 AOF文件的载入与数据还原
1.创建伪客户端
2.从AOF文件中分析并读取一条写命令
3.使用伪客户端执行写命令
4.重复2，3直到命令执行完毕


### 11.3 AOF重写
#### 11.3.1 AOF文件重写的实现
实现原理：读取Redis现在的值，然后用一条命令记录替代之前的多条命令

#### 11.3.2 AOF后台重写 BGWRITEAOF
如何解决后台重写导致的数据不一致问题？
AOF重写缓冲区

当子进程完成AOF重写工作之后:
1.将AOF重写缓冲区内容写入新AOF文件中
2.原子地将新AOF文件覆盖现有的AOF文件

## 12 事件
file event
time event

### 12.1 文件事件

#### 12.1.1 文件事件处理器的构成

套接字 -> io多路复用 -> 文件事件分派器 -> 事件处理器

#### 12.1.2 io多路复用程序的实现
通过封装select,epoll,evport,kequeue等来实现

#### 12.1.3 事件的类型
IO多路复用产生可读事件与可写事件，

#### 12.1.4 API

#### 12.1.5 文件事件的处理器
1. 连接应答处理器
2. 命令请求处理器
3. 命令回复处理器
4. 一次完整的客户端与服务器连接事件示例

### 12.2 时间事件
Redis时间事件分为以下两类：
* 定时事件
* 周期性事件

一个时间事件：
* id:
* when:时间时间的到达时间
* timeProc:时间处理器，一个函数

一个时间事件是定时事件还是周期性事件取决于时间事件处理器的返回值：
* 如果事件处理器返回ae.h/AE_NOMORE，那么这个事件为定时事件
* 如果返回一个非AE_NOMORE的整数值，那么这个事件为周期性时间

#### 12.2.1 实现
服务器将所有时间事件放在一个无序链表中，每当时间事件执行器运行时，它就遍历整个链表，查找所有已到达的时间事件，并调用相应的事件处理器

#### 12.2.2 API

#### 12.2.3 时间事件应用实例：serverCron实例
* 更新服务器的各类统计信息
* 清理数据库中的过期键值对
* 关闭和清理连接失败的客户端
* 尝试进行AOF和RDB持久化操作
* 如果服务器是主服务器，那么对从服务器进行定期同步
* 如果处于集群模式，对集群进行定期同步和连接测试

### 12.3 事件的调度与执行
1. aeApiPoll函数的最大阻塞时间由到达时间最接近当前时间的时间事件决定
2. 因为文件事件是随机出现的，如果等待并处理一次文件事件后，仍未有任何的时间事件到达，那么服务器将再次等待并处理文件事件
3. 对文件事件和时间事件的处理都是同步、有序、原子地执行的，服务器不会中途中断时间处理，也不会对时间进行独占
4. 因为时间事件在文件事件之后执行，并且事件之间并不会出现抢占，所以时间事件实际处理时间，通常比时间事件设定的到达时间稍晚一些

## 13 客户端
Redis服务器为客户端建立相应的redisClient，这个结构保存了客户端当前的状态信息。
* 客户端的套接字描述符
* 客户端的名字
* 客户端的标志值(flag)
* 指向客户端正在使用的数据库指针，以及该数据库的号码
* 客户端当前要执行的命令、命令的参数、命令参数的个数，以及指向命令实现函数指针
* 客户端的输入缓冲区和输出缓冲区
* 客户端的复制状态信息，以及进行复制所需的数据结构
* 客户端BRPOP、BLPOP等列表阻塞命令时使用的数据结构
* 客户端的事务状态，以及执行WATCH命令是用到的数据结构
* 客户端执行发布与订阅功能时用到的数据结构
* 客户端的身份验证标志
* 客户端的创建时间，客户端和服务端最后一次通信时间，以及客户端输出缓冲区大小超出软性限制的时间

### 13.1 客户端属性
客户端属性分为两类：
1. 比较通用的属性
2. 和特定功能相关的属性,db,dictid,mstate,WATCH

#### 13.1.1 套接字描述符
```cpp
typedef struct redisClient{
    //...
    int fd;
    //...
} redisClient;

```
* 伪客户端的fd属性值为-1；伪客户端处理的命令请求来源于AOF文件或者Lua脚本
* 普通客户端的fd属性值为大于-1的整数：服务器用fd记录客户端套接字的描述符

#### 13.1.2 名字
在默认情况下，一个连接到服务器的客户端是没有名字的；但是可以使用CLIENT setname 为客户端设置一个名字

#### 13.1.3 标志
一部分标志记录了客户端的角色:
* REDIS_MASTER
* REDIS_PRE_PSYNC
* REDIS_LUA_CLIENT

另一部分标志记录了客户端目前所处的标志：
* REDIS_MONITOR
* REDIS_UNIX_SOCKET
* REDIS_BLOCKED
* REDIS_UNBLOCKED
* REDIS_MULTI
* REDIS_DIRTY_CAS;REDIS_DIRTY_EXEC
* REDIS_CLOSE_ASAP
* REDIS_CLOSE_AFTER_REPLY
* REDIS_ASKING
* REDIS_FORCE_AOF;REDIS_FORCE_REPL
* REDIS_MASTER_FORCE_REPLY

#### 13.1.4 输入缓冲区
输入缓冲区最大大小不能超过1GB,否则服务器将关闭这个客户端

#### 13.1.5 命令与命令参数

#### 13.1.6 命令的实现函数

#### 13.1.7 输出缓冲区
* 固定大小的缓冲区buf 用于保存较短的回复
* 可变大小缓冲区由 list *reply链表和一个或多个字符串对象构成

#### 13.1.8 身份验证 authenticated
0：未通过；1通过

#### 13.1.9 时间
ctime:客户端创建时间
lastinteraction:最后一次与服务器互动时间
obuf_soft_limit_reached_time:输出缓冲区第一次到达软性限制的时间

### 13.2 客户端的创建与关闭
#### 13.2.1 创建普通客户端
#### 13.2.2 关闭普通客户端
服务器使用两种模式来限制客户端输出缓冲区的大小
* hard limit
* soft limit 记录超出软性限制大小的起始时间obuf_soft_limit_reached_time，如果持续时间超出服务器设定的时间，服务器将关闭客户端

client-output-buffer-limit 可以为普通客户端，从服务器客户端，发布与订阅客户端分别设置不同的软性限制和硬性限制

#### 13.2.3 Lua脚本的伪客户端

#### 13.2.4 AOF文件的伪客户端

## 14 服务器
### 14.1 命令请求的执行过程
1. 客户端向服务器发送命令SET KEY VALUE
2. 服务器接收并处理客户端发来的命令请求 SET KEY VALUE，在数据库中中产生命令回复OK
3. 服务器将命令回复OK发送给客户端
4. 客户端接收服务器返回的命令回复OK,并将回复打印给用户观看

#### 14.1.1 发送命令请求
#### 14.1.2 读取命令请求
#### 14.1.3 命令执行器
#### 14.1.4 命令执行器（2）执行预备操作
* 检查客户端的cmd指针是否指向NULL
* 根据cmd属性指向的redisCommand结构的arity属性，检查命令属性的


## 多机数据库的实现
## 15 复制
Redis 可以通过执行SLAVEOF 命令或者Slaveof选项，让一个服务器去复制另一个服务器

### 15.1 旧版复制功能的实现
Redis 的复制功能分为同步(sync)和命令传播(command propagate)两个操作：

#### 15.1.1 同步SYNC
#### 15.1.2 命令传播

### 15.2 旧版复制功能的缺陷
从服务器的复制分为两类：
* 初次复制：从服务器从未复制过主服务器或者本次复制的服务器与上一次不同
* 断线后复制：处于命令传播阶段的主从服务器因为网络原因中断了复制，重连后继续复制

两种情况都需要重新执行SYNC的整个过程，对于第二种类型来说可能确实比较低效

### 15.3 新版复制功能的实现
PSYNC 新增了断线后复制的部分重同步

### 15.4 部分重同步的实现
部分重同步功能由以下三个部分构成：
* 主服务器的复制偏移量和从服务器的复制偏移量
* 主服务器的复制积压缓冲区
* 服务器的运行ID

#### 15.4.1 复制偏移量
复制双方分别维护一个复制偏移量（复制积压缓冲区的）

#### 15.4.2 复制积压缓冲区
复制积压缓冲区的默认大小为1MB

* 如果offset偏移量之后的数据(offset+1)仍然存在与复制积压缓冲区中，那么将进行重同步操作
* 否则将进行完整重同步

复制积压缓冲区的大小估算 = second*write_size_per_second

#### 15.4.3 服务器运行ID
用于确认连接前后是否连接同一个主服务器

### 15.5 PSYNC命令的实现
PSYNC 的调用方法有两种：
* 如果从服务器以前没有复制过任何主服务器，或者之前执行过SLAVEOF no one 命令，那么从服务器向主服务器发送PSYNC ? -1 ,进行完整重同步
* 相反的，那么从服务器发送PSYNC <runid> <offset>

主服务的回复有三种：
* +FULLRESYNC <runid> <offset> 完整重同步
* +CONTINUE 部分重同步
* -ERR 主服务器低于Redis2.8 无法识别PSYNC 

### 15.6 复制的实现
SLAVEOF <master_ip> <master_port>
#### 15.6.1 步骤1：设置主服务器的地址和端口
#### 15.6.2 步骤2：建立套接字连接
#### 15.6.3 步骤3：发送PING命令
作用：
1. 检查套接字的读写状态
2. 检查主处理器是否正常处理命令清秀

从服务器将遇到三种情况
1. 从服务器无法在规定时间内读出主服务器命令回复的内容
2. 如果主服务器向从服务器返回一个错误，那么表示主服务器暂时没办法处理从服务器的命令
3. 如果从服务器读取到PONG回复，那表示主从服务器之间的连接状态正常

#### 15.6.4 步骤4：身份验证
身份验证：
1. 如果从服务器设置了masterauth ，那么进行身份验证
2. 否则不进行身份验证

身份验证从服务器可能遇到的情况有以下几种：
1. 如果主服务器没有设置requirepass选项，并且从服务器也没有设置masterauth，那么主服务将继续执行从服务器发送的命令
2. 如果从服务器AUTH命令发送的密码和主服务器requirepass选项所设置的密码相同，那么可以执行，否则将返回invalid pass错误
3. 如果主服务器设置了requirepass,但是从服务器没有设置masterauth，则主服务器将返回一个NOAUTH错误；相反则返回 no password is set 错误

#### 15.6.5 步骤5：发送端口信息 REPLCONF listening-port <port-number>
主服务器会将从服务器发送的端口号记录在slave_listening_port 中，并可以通过INFO replication 打印出来

#### 15.6.6 步骤6：同步 PSYNC

#### 15.6.7 步骤7：命令传播

### 15.7 心跳检测
命令传播阶段，从服务器默认会以每秒一次的频率向主服务器发送命令

REPLCONF ACK <replication_offset>
作用：
1. 检测主从服务器的网络连接状态
2. 辅助实现min-slaves选项
3. 检测命令丢失

#### 15.7.1 检测主从服务器的网络连接状态
#### 15.7.2 辅助实现min-slaves选项
min-slaves-to-write和min-slaves-max-lag 两个选项可以防止主服务器在不安全的情况下执行写命令
#### 15.7.3 检测命令丢失


## 16 Sentinel
### 16.1 启动并初始化Sentinel
当启动一个sentinel，它需要执行以下步骤:
1. 初始化服务器
2. 将普通Redis服务器使用的代码替换成Sentinel专用代码
3. 初始化Sentinel 状态
4. 根据给定的配置文件，初始化sentinel的监视主服务器列表
5. 创建连向主服务器的网络连接

#### 16.1.1 初始化sentinel
#### 16.1.2 使用sentinel专用代码
#### 16.1.3 初始化Sentinel状态
```cpp
struct sentinelState{
    //当前纪元，用还有实现故障转移
    uint64_t current_epoch;
    //保存了所有被这个sentinel监视的主服务器
    //字典的键是主服务器的名字
    //字典的值则是一个sentinelRedisInstance 的结构的指针
    dict *master;
    //是否进入了TILT模式
    int tilt;
    //目前正在执行的脚本的较量
    int running_scripts;
    //进入TILT模式的时间
    mstime_t previous_time;
    //一个FIFO队列，包含了所有需要执行的用户剧本
    list *script_queue;
} sentinel;
```

#### 16.1.4 初始化Sentinel状态的master属性
```cpp
typedef struct sentinelRedisInstance{
    //标识值，记录了实例的类型，以及该实例的当前状态
    int flags;
    //实例的名字
    //主服务器的名字由用户在配置文件中设置
    //从服务器以及Sentinel的名字由Sentinel自动设置
    //格式为ip:port,例如"127.0.0.1:26379"
    char *name;
    //实例运行的ID
    char *runid;
    //配置纪元，用于实现故障转移
    uint64_t config_epoch;
    //实例地址
    sentinelAddr *addr;
    //SENTINEL down-after-millisenconds 选项设定的值
    //实例无响应多少毫秒之后财汇被判断为主观下线(subjectively down)
    mstime_t down_after_period;
    //SENTINEL monitor <master-name> <IP> <port> <quorum> 选项中的quorum参数
    //判断这个实例为客观下线(objectively down) 所需的支持投票数量
    int quorum;
    //SENTINEL parallel-syncs <master-name> <number> 选项的值
    //在执行故障转移操作时，可以同时对新的主服务器进行同步的从服务器的数量   
    int parallel_syncs;
    //SENTINEL failover-time <master-name> <ms> 选项的值
    //刷新故障迁移状态的最大时限
    mstime_t failover_timeout;

    //...
} sentinelRedisInstance;

typedef struct sentinelAddr{
    char *ip;
    int port;
} sentinelAddr;

```

#### 16.1.5 创建连向主服务器的网络连接
对于每个被Sentinel监视的主服务器来说，Sentinel会创建两个连向主服务器的异步网络连接：
* 一个是命令连接，这个连接专门用于向主服务器发送命令，并接收命令回复
* 另一个是订阅连接，这个连接专门用于订阅主服务器的__sentinel__:hello频道

### 16.2 获取主服务器的信息
sentinel默认会以每十秒一次的频率，通过命令连接向被监视的主服务器发送INFO命令，并通过分析INFO命令的回复来获取主服务器的的当前信息

1. 根据run_id域和role域记录的信息，sentinel将对主服务器的实例结构进行更新
2. 至于主服务器返回的从服务器信息，则会被用于更新主服务器实例结构的的slaves字典，键为从服务器名字 ip:port,值为从服务器的实例结构

### 16.3 获取从服务器的信息
当sentinel发现主服务器有新的从服务器出现时，sentinel除了会为这个新的从服务器创建相应的实例外，sentinel还会创建连接到从服务器的命令连接和订阅连接

创建命令连接之后，sentinel在默认情况下，会以每十秒一次的频率通过命令连接向从服务器发送INFO命令，并获得类似于以下内容的回复

根据INFO命令的回复，sentinel会提取出以下信息:
* 从服务器的运行IDrun_id
* 从服务器的角色role
* 主服务器的IP地址master_host,以及主服务器的端口号master_port
* 主从服务器的连接状态master_link_status
* 从服务器的优先级slave_priority
* 从服务器的复制偏移量slave_repl_offset

### 16.4 向主服务器和从服务器发送信息
默认情况下，sentinel 会以每两秒一次的频率，通过命令连接向所有被监视的主服务器和从服务器发送以下格式的命令:
PUBLISH __sentinel__:hello "<s_ip>,<s_port>,<s_runid>,<s_epoch>,<m_name>，<m_ip>,<m_port>,<m_epoch>"

### 16.5 接收来自主服务器和从服务器的频道信息

### 16.6 检测主观下线状态

### 16.7 检查客观下线状态

### 16.8 选举领头Sentinel

## 17 集群
### 17.1 节点
连接各个节点的工作可以使用CLUSTER MEET <ip> <port>
查看所有节点 CLUSTER NODES 

### 17.1.1 启动节点
根据cluster-enabled配置决定是否开启服务器的集群模式

### 17.1.2 集群数据结构
```
struct clusterNode{
    //创建节点的时间
    mstime_t ctime;
    //节点的名字，由40个十六进制字符组成
    charname[REDIS_CLUSTER_NAMELEN];
    //节点标识
    //使用各种不同的标识值记录节点的角色（比如主节点或者从节点）
    //以及节点目前所处的状态
    int flags;
    //节点当前的配置纪元，用于实现故障转移
    uint64_t configEpoch;
    //节点的ip地址
    char ip[REDIS_IP_STR_LEN];
    //节点的端口号
    int port;
    //保存连接节点所需的有关信息
    clusterLink *link;
    //...
};
```

clusterLink保存了连接相关的信息
```
typedef struct clusterLink{
    //连接的创建时间
    mstime_t ctime;
    //TCP套接字描述符
    int fd;
    //输出缓冲区，保存着等待发送给其他节点的消息（message）
    sds sndbuf;
    //输入缓冲区，保存着从其他节点接收的消息
    sds rcvbuf;
    //与这个连接相关联的节点，如果没有的话就为NULL
    struct clusterNode *node;

}
```
clusterState 记录当前节点的状态
```
typedef struct clusterState{
    //指向当前节点的指针
    clusterNode *myself;
    //集群当前的配置纪元，用于实现故障转移
    uint64_t currentEpoch;
    //集群当前的状态：是在线还是下线
    int state;
    //集群中至少处理一个槽的节点的数量
    int size;
    //集群节点名单（包括myself节点）
    //字典的键为节点的名字，字典的值为节点对应的clusterNode结构
    dict *nodes;
}
```

#### 17.1.3 CLUSTER MEET命令的实现

### 17.2 槽指派
集群的整个数据库被分为16384个槽，数据库中的每个键都属于这个16384个槽中的一个集群中的每个节点可以处理0个或者16384个槽
CLUSTER ADDSLOTS <slot> [slot ..] 可以将一个或者多个槽指派给节点负责

#### 17.2.1 记录节点的槽指派信息
```
//clusterNode 结构的slots属性和numslot属性记录了节点负责处理哪些槽：
struct clusterNode{
    //....
    unsigned char slots[16384/8];
    
    int numslots;
    //...
}
```

#### 17.2.2 传播节点的槽指派信息

#### 17.2.3 记录集群所有槽的指派信息

#### 17.2.4 CLUSTER ADDSLOTS 命令的实现
