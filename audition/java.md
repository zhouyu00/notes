数据结构

    红黑树

    http://www.360doc.com/content/18/0904/19/25944647_783893127.shtml
    https://www.jianshu.com/p/6f6642b982af
    https://github.com/julycoding/The-Art-Of-Programming-By-July/blob/master/ebook/zh/03.01.md

    hashmap底层实现

    8之前是链表+entrySet，1.8之后使用链表+红黑树

    hashmap的扩容机制

    https://www.cnblogs.com/yanzige/p/8392142.html

    一致性哈希

    https://www.cnblogs.com/study-everyday/p/8629100.html
    https://www.jianshu.com/p/e968c081f563

    布隆过滤器

    https://segmentfault.com/a/1190000015482091
    https://my.oschina.net/LucasZhu/blog/1813110
    https://www.jianshu.com/p/2104d11ee0a2

    跳表

    https://www.jianshu.com/p/dd01e8dc4d1f
    https://blog.csdn.net/pcwl1206/article/details/83512600

    为什么求解String的哈希值要乘31

    https://blog.csdn.net/zhanjia/article/details/84923530

网络

    各类协议头部

    https://blog.csdn.net/winbobob/article/details/41475959

    漏桶算法

    InetAddress IP协议/URL/URLConnection/HTTPURLConnection/Socket/ServerSocket

    https://www.cnblogs.com/kuangzhisen/p/7053689.html

    UrlConnection连接和Socket连接的区别

    https://blog.csdn.net/iteye_1429/article/details/82168974
    https://blog.csdn.net/bibi1314123/article/details/17090927

    五层模型及协议

    https://blog.csdn.net/qq_22238021/article/details/80279001

    列举几个网络攻击
    SYN攻击（DDOS攻击）

    https://baijiahao.baidu.com/s?id=1622812984571131456&wfr=spider&for=pc

    HTTP，TCP，IP 报文头

    https://www.cnblogs.com/CodingUniversal/p/7524088.html
    https://blog.csdn.net/ythunder/article/details/65664309

    网页访问全过程
    https://blog.csdn.net/u012862311/article/details/78753232

    优化网页访问方案

    https://www.cnblogs.com/xg1010831107/p/optimization.html
    https://www.cnblogs.com/propheterLiu/p/5935622.html

    各协议的默认端口号

    https://blog.csdn.net/qiucheng_198806/article/details/87375505

    MSL/TTL/RTT

    https://blog.csdn.net/u013074465/article/details/45097183

    MTU/MSS

    https://blog.csdn.net/scythe666/article/details/51965782

    各层的中继设备

    a. 物理层：中继器或集线器

    b. 数据链路层：网桥或者交换机

    c. 网络层： 路由器

    d. 网络层之上：网关

物理层
数据链路层

    ARP协议的原理过程

    https://www.cnblogs.com/csguo/p/7542944.html

网络层

    网络层的功能：

    a. 异构网络互连

    b. 拥塞控制

    c. 路由选择与转发

    路由算法：距离向量路由算法与链路状态路由算法；RIP算法与OSPF算法

    IP数据报头部固定长度=

    版本（1B）+ 首部长度（1/2B）+ 区分服务（1B) + 总长度（2B）

    标识（2B）+ 标志（3bit) + 片偏移（13bit）

    生存时间TTL（1B） + 协议（1B） + 校验和（2B)

    源地址（4B）

    目的地址（4B）

    ICMP

    https://www.cnblogs.com/iiiiher/p/8513748.html
    https://blog.csdn.net/u011784495/article/details/71743516

传输层

    传输层的功能

    ① 对于整个传输层来说

    a. 提供进程之间的抽象连接

    b. 差错控制（包括首部与数据一起的）

    c. 提供面向连接与无连接的服务

    d. 复用与分用

    ② 对于面向连接的服务

    a. 提供可靠的连接管理

    b. 提供流量控制与拥塞控制

UDP

    UDP伪首部（12B） =
    源IP地址（4B)

    目的IP地址（4B）

    保留字节（1B）+传输协议号（1B）+ 报文长度（2B）

    UDP报文首部（8B）=

    源端口地址（2B）+ 目的端口 （2B）

    长度 （2B）+ 校验和（2B）

TCP

    TCP 报文首部固定部分（20B）=

    源端口地址（2B）+ 目的端口 （2B）

    序号（4B）

    确认号（4B）

    数据偏移（4bit）+ 保留（6bit）+标志位（6bit）+窗口（2B）

    校验和（2B）+ 紧急指针（2B）

    三次握手和四次挥手

    https://blog.csdn.net/qq_38950316/article/details/81087809
    建立连接阶段及数据传输阶段ACK的值的意义
    https://blog.csdn.net/ygm_linux/article/details/79546034
    注意*其中减去的54为 以太网协议头（14B）+TCP协议头（20B）+IP协议头（20B）

    TCP和UDP的区别

    https://www.cnblogs.com/williamjie/p/9390164.html
    https://www.cnblogs.com/twoheads/p/9713936.html

面向报文与面向字节

    https://blog.csdn.net/ce123_zhouwei/article/details/8976006

    TCP如何保证可靠传输

    https://blog.csdn.net/liuchenxia8/article/details/80428157

    TCP如何进行流量控制

    https://blog.csdn.net/u011784495/article/details/72639876

    TCP如何进行拥塞控制

    https://blog.csdn.net/m0_37962600/article/details/79993310

    三次握手中ack的值是什么？SYN攻击与防护

    https://www.cnblogs.com/huskiesir/p/10212053.html
    https://baijiahao.baidu.com/s?id=1627339324399698792&wfr=spider&for=pc

    tcp的time wait 和 close wait

    长连接及心跳连接

    https://www.jianshu.com/p/16c8c9e09feb

    粘包现象及如何处理粘包

    https://blog.csdn.net/zhengzhaoyang122/article/details/81784306
    https://www.cnblogs.com/zhangsanfeng/p/8891149.html

应用层
HTTP

    HTTP非持久连接与持久连接

    https://www.cnblogs.com/shoren/p/http-connection.html

    HTTP协议中常见的contentType类型

    https://www.cnblogs.com/wushifeng/p/6707248.html

    HTTP1.0和HTTP1.1,HTTP2.0的区别

    https://www.cnblogs.com/smlp/p/9779206.html
    https://www.cnblogs.com/heluan/p/8620312.html

    HTTP和HTTPS的区别

    https://www.cnblogs.com/jesse131/p/9080925.html
    https://www.cnblogs.com/shoshana-kong/p/10583760.html

    HTTP状态码

    https://www.cnblogs.com/xflonga/p/9368993.html

    HTTP POST和GET

    https://www.cnblogs.com/liziweiblog/p/11066333.html
    https://blog.csdn.net/bieleyang/article/details/76272699
    https://baijiahao.baidu.com/s?id=1626599028653203490&wfr=spider&for=pc

数据库/MySql

    Mysql的事务隔离级别

    https://www.cnblogs.com/rxbook/p/8975924.html
    设置mysql的事务隔离级别
    https://www.cnblogs.com/huasky/p/11190086.html
    https://www.cnblogs.com/satng/p/7759899.html

    数据库的连接池

    https://blog.csdn.net/qq_39659876/article/details/80958450
    https://blog.csdn.net/qq_34468186/article/details/83892496
    https://baijiahao.baidu.com/s?id=1599699339020031595&wfr=spider&for=pc

    乐观锁悲观锁

    https://www.cnblogs.com/suger43894/p/11024102.html

    数据库分页优化

    https://www.cnblogs.com/geningchao/p/6649907.html
    https://www.cnblogs.com/RunForLove/p/5100009.html
    https://www.cnblogs.com/waterystone/p/9392421.html

    mysql数据引擎知道几种？innodb和mylsam区别
    6种，InnoDB,MyISAM,NDB,Memory,Archive,Federated,Maria

    https://www.cnblogs.com/zhangchaoyang/articles/4214237.html

    索引失效

    复合索引不能跨列或者无序使用；尽量使用全索引匹配
    不要在索引上进行任何操作（计算，函数，类型转换）
    复合索引不能使用不等于或is null，否则自身及右侧全部失效
    复合索引中有>,<,in，之后的索引失效
    like尽量用常量开头，不以“%”开头；如果必须以“%”开头，可以用索引覆盖挽救一部分
    尽量不要用or，否则or左侧的索引也失效

    覆盖索引

    https://blog.csdn.net/qq_15037231/article/details/87891683
    https://www.cnblogs.com/happyflyingpig/p/7662881.html
    https://www.cnblogs.com/pyng/p/9599977.html

    倒排序索引

    https://www.cnblogs.com/gered/p/9561710.html
    https://www.cnblogs.com/luminous1/p/8383777.html
    https://blog.csdn.net/zsd_31/article/details/79979818

    MVCC

    https://blog.csdn.net/rocling/article/details/81193431
    https://www.cnblogs.com/liulvzhong/articles/9242299.html

    索引失效

    https://www.jianshu.com/p/42cfeec20301

redis

    Redis数据结构及持久化机制

    https://www.cnblogs.com/neooelric/p/9621736.html

    Redis持久化机制

    https://www.cnblogs.com/yyjie/p/7487937.html

MyBatis

    mybatis 如何获取自增ID

    https://blog.csdn.net/zonghao123/article/details/78374169

    mybatis 一二级缓存

JavaSE

    根据反射加载一个类的具体步骤

    https://www.cnblogs.com/xiaobiqiang/p/6047146.html
    https://www.cnblogs.com/FanJava/p/9512775.html

    泛型

    https://www.cnblogs.com/coprince/p/8603492.html

    面向对象
    HashMap为什么初始化为16

    https://blog.csdn.net/l18848956739/article/details/85998121

    hashCode 怎么对应桶的位置

    https://blog.csdn.net/yue31313/article/details/77513353

    hashCode的计算

    https://blog.csdn.net/tanggao1314/article/details/51457585
    https://blog.csdn.net/zhucegemingzizheng/article/details/81289479

    字符串快速去重

    Error和Exception的区别

    https://www.cnblogs.com/lcl-dcr/p/7653274.html
    https://www.cnblogs.com/hustzzl/p/7840780.html

    聊一下java里的对象（java里的包）

    HashMap底层转红黑树的时机

    https://www.cnblogs.com/laipimei/p/11282055.html
    https://www.cnblogs.com/laipimei/p/11275235.html

    io类型；nio是其中哪一种

    https://blog.csdn.net/datadev_sh/article/details/79241186
    https://blog.csdn.net/Yufail/article/details/88825123

    静态代码块，构造代码块，构造函数与普通代码块

    https://www.cnblogs.com/ysocean/p/8194428.html

JavaEE

    Session，Cookie和Token

    https://www.cnblogs.com/zlw-xf/p/8001383.html
    https://www.cnblogs.com/roxy/p/7805858.html
    https://www.cnblogs.com/moyand/p/9047978.html

    Servlet的生命周期
    拦截器和过滤器的区别

    https://blog.csdn.net/zxd1435513775/article/details/80556034
    https://www.cnblogs.com/panxuejun/p/7715917.html
    过滤器只在容器初始化时调用一次该怎么理解？
    https://blog.csdn.net/dingchenxixi/article/details/81391831

    防止XSS攻击

    https://www.cnblogs.com/hero123/p/9091625.html
    https://www.jianshu.com/p/cd49578bdd48

设计模式

    单例模式的好处，应用

    https://www.cnblogs.com/restartyang/articles/7770856.html

    工厂模式

    https://blog.csdn.net/weixin_41843053/article/details/80853758
    https://www.jianshu.com/p/ae2e22aa6147

    Java单例的饱汉与饿汉模式

    https://blog.csdn.net/sai739295732/article/details/62411016
    https://blog.csdn.net/qq_37768482/article/details/77539850

JVM

    JVM中的gc，Full GC

    https://baijiahao.baidu.com/s?id=1632743030610982339&wfr=spider&for=pc
    https://blog.csdn.net/hellozhxy/article/details/80649342
    https://blog.csdn.net/weixin_39788856/article/details/80388002
    https://www.cnblogs.com/jenkov/p/full_gc_old_gc_cms_gc.html
    https://www.cnblogs.com/williamjie/p/9516264.html

    垃圾回收及算法
    垃圾回收算法：

    标记-清除
    标记-复制
    标记-整理
    分代回收

垃圾收集器

年轻代
Serial：单线程
ParNew：多线程
Parallel Scavenge：使用复制算法，强调精确控制吞吐量

老年代
Serial Old：单线程，Serial 的老年代版本
Parallel Old：Parallel Scavenge 使用多线程和”标记-整理“算法 吞吐量优先
CMS：”标记-清除“算法，强调最短回收停顿时间
兼顾年轻代和老年代：
G1收集器：并行与并发，分代回收，”标记-整理”算法，可预测的停顿

    https://www.jianshu.com/p/35805f809a21

    假设有一个加法类从编译到最终使用的整个过程

    如何判断对象是否需要被回收？两个相互引用的对象如何被回收

    引用计数
    可达性分析

附：GCRoot的对象包括：

    虚拟机栈中引用的对象
    方法区中类静态属性引用的对象
    方法区中常量引用的对象
    本地方法栈中JNI引用的对象

    虚拟机栈异常类型以及复现代码
    堆内存异常类型以及复现
    直接内存怎么使用以及jvm对其管理

多线程

    https://www.jianshu.com/p/125ccf0046f3

    线程池的参数
    public ThreadPoolExecutor(
    int corePoolSize,
    int maximumPoolSize,
    long keepAliveTime,
    TimeUnit unit,
    ThreadFactory threadFactory,
    RejectedExecutionHandler handler
    );

    为什么要使用线程池

    https://blog.csdn.net/a497393102/article/details/8597819
    https://blog.csdn.net/Muz_victory/article/details/81216771

    如何合理的配置线程池
    CPU密集型 Ncpu+1
    IO密集型 2*Ncpu

混合型任务 进行任务拆分

    饱和策略/任务队列满了以后再来一个任务如何处理

    AbortPolicy
    CallerRunsPolicy
    DiscardOldestPolicy
    DiscardPolicy
    https://www.cnblogs.com/skywang12345/p/3512947.html

    JUC包里的东西，有哪些常用锁

    https://www.cnblogs.com/doit8791/p/9131148.html
    Lock，AQS，ReentrantLock，ReadWriteLock，LockSupport，Condition

    线程同步的几种方法？

    https://www.cnblogs.com/baizhanshi/p/7025974.html

    线程同步使用哪些锁？

    https://www.cnblogs.com/lixiangyang521/p/6861768.html

    死锁和死循环都会导致程序hold住，怎么判断是死锁还是死循环

    https://blog.csdn.net/wanglha/article/details/51133819

    并发容器种类
    https://www.cnblogs.com/ygj0930/p/6543877.html

    https://blog.csdn.net/cdefggg/article/details/86426917
    https://www.jianshu.com/p/7f50497b7f30

    concurrenthashmap数据结构

    线程状态(blocked waiting timed_waiting)

    https://www.cnblogs.com/cowboys/p/9315331.html

    等待和阻塞的区别

    https://blog.csdn.net/woshiyigeliangliang/article/details/81116872

    wait和sleep的区别

    https://blog.csdn.net/kangkanglou/article/details/82221301

    volatile变量i++

    https://www.cnblogs.com/zemliu/p/3298685.html
    https://blog.csdn.net/dm_vincent/article/details/79604716

    sychronized 和 RetreenLock的区别

    https://www.cnblogs.com/java-spring/p/10792097.html

    介绍一下线程池

    单线程池的应用场景

spring

    spring的主要特点？介绍一下AOP和IOC；AOP的实现方式；IOC的实现方式
    AOP和IOC；AOP是面向切面编程；IOC是控制反转；spring AOC的实现是 jdk动态代理和cglib代理；
    AOP的实现

    https://blog.csdn.net/wyl6019/article/details/80136000
    IOC的实现

    https://www.cnblogs.com/neon/p/10929759.html

    https://www.cnblogs.com/study-everyday/p/8566532.html

    https://www.jianshu.com/p/4b31dacf3a63

附：常见的四种代理方式

    https://blog.csdn.net/luanlouis/article/details/24589193
    cglib和jdk动态代理的比较
    https://blog.csdn.net/liangwenmail/article/details/78457106

    spring中如何配置事务管理级别

    https://www.cnblogs.com/cxyj/p/3906402.html

    springMVC的处理流程

    https://www.cnblogs.com/5ishare/p/8683971.html

    一个Controller中会涉及到哪些注解
    @Controller
    @Autowire
    @RequestMapping
    @RequestParam
    @RequestBody
    @ResponseBody
    @ModelAttribute

    Spring和Spring boot的区别

    https://www.jianshu.com/p/ffe5ebe17c3a
    https://blog.csdn.net/wang_666_/article/details/80527113
    https://www.codercto.com/a/27048.html

    @transaction

分布式

    分布式锁的实现

    https://blog.csdn.net/qq_32924343/article/details/79814133
    附：
    CAP原理
    http://www.ruanyifeng.com/blog/2018/07/cap.html

    了解微服务吗？

    RPC调用

    https://www.cnblogs.com/linlinismine/p/9205676.html
    https://www.cnblogs.com/FG123/p/10261676.html

操作系统 Linux

    Linux Cpu的轮询方式

    Linux中查询当前系统有多少个进程的指令

    Linux的五种io模式，javaNIO

    https://blog.csdn.net/datadev_sh/article/details/79241186
    https://blog.csdn.net/Yufail/article/details/88825123

    Linux 的swap分区

    https://www.cnblogs.com/saneri/p/10319412.html

    select,poll和epoll的区别

    https://www.cnblogs.com/Anker/p/3265058.html

绪论

    内核态与用户态，特权指令
    内核态：又称管态，是操作系统管理程序执行时机器所处的状态。它具有较高的特权，能够执行包括特权指令的一切指令，能够访问所有的寄存器和存储区
    用户态：又称目态，是用户程序执行时机器所处的状态。它具有较低的特权，只能执行规定的指令，只能访问指定的寄存器和存储区
    特权指令：只能由操作系统内核使用的，不允许用户程序使用的指令，如IO指令，设置中断屏蔽指令，清内存指令，存储保护指令和设置时钟指令

    中断与异常

    https://blog.csdn.net/u014134180/article/details/78418428
    什么是中断
    https://www.cnblogs.com/jacklong-yin/p/11263052.html

    系统调用
    操作系统提供给用户程序请求内核完成某种功能的一种过程调用

    https://blog.csdn.net/xiaomimi1993/article/details/81710623

进程管理
进程与线程

    进程的组成

    进程控制块（PCB）
    程序段
    数据段

    进程的状态与转换

    https://blog.csdn.net/qwe6112071/article/details/70473905

    内核级线程与用户级线程

    https://www.cnblogs.com/feng9exe/p/7890934.html

    进程通信方式
    a，管道；b，消息队列；c，共享内存
    几种通信方式的联系与区别

    https://blog.csdn.net/u014800094/article/details/53993275

处理器调度

    常见的调度算法
    a，先来先服务
    b，短作业优先
    c，优先级调度
    d，时间片轮转
    e，高相应比调度
    f，多级队列调度
    g，多级反馈队列调度

互斥与同步

    互斥的要求

    空闲让进
    忙则等待
    有限等待
    让权等待

    互斥的实现
    信号量机制；PV原子操作

    经典同步问题
    a，生产者消费问题
    b，读者-写者问题
    c，哲学家进餐问题
    d，理发师问题

    管程

    死锁产生的原因和必要条件
    原因：竞争资源；系统资源不足和进程推进顺序不当
    必要条件：

    互斥条件
    不剥夺条件
    请求与保持条件
    环路等待条件

    死锁的预防

    https://www.cnblogs.com/bopo/p/9228834.html

    死锁代码demo

    https://blog.csdn.net/wanglha/article/details/51133819

内存管理

    交换与覆盖

    存储管理方式
    连续管理方式
    非连续管理方式

    MMU和快表
    MMU

    https://www.cnblogs.com/alantu2018/p/9002309.html
    快表TLB
    https://blog.csdn.net/weixin_36725931/article/details/85344814
    TLB和MMU的区别
    https://www.cnblogs.com/linhaostudy/p/7771437.html

    虚拟内存

    https://www.cnblogs.com/kexinxin/p/9939085.html

    缺页中断与普通中断的区别
    a，在指令的执行期间产生和处理中断
    b，一条指令可以产生多个缺页中断

    页面置换算法
    a，OPT最佳置换算法
    b，FIFO先进先出
    c，LRU最近最少使用
    d，CLOCK时钟置换算法

    改进时钟算法

文件管理

    软链接和硬链接

    https://www.cnblogs.com/rswss/p/9466882.html
    https://www.cnblogs.com/sanjun/p/9971993.html

    i节点

    https://blog.csdn.net/cc_946079647/article/details/19088205

设备管理

    IO控制方式

    程序直接控制方式
    中断控制方式
    DMA控制方式
    通道控制方式

其他

    线程通信方式
    共享内存，管道，消息传递

    https://blog.csdn.net/pengzhisen123/article/details/79455742
    https://www.cnblogs.com/shilinnpu/p/8873390.html

