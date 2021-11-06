

# java.lang
## java.lang.instrument
### 接口
#### ClassFileTransformer
提供一个转换类文件的代理，transformation 发生在JVM define Class（将类文件数据->JVM 类结构）之前

#### Instrumentation
这个类提供需要测量java程序语言的能力。Instrumentation 是为了使用工具向字节码中统一增加收集数据的方法。
因为这些代码是增加的，因此不会调整应用的状态或行为。
这些温和的工具包括监控，分析，覆盖率分析，和事件日志


# java.util

## java.uill.logging
### 接口
#### Filter
提供细粒度的控制关于什么需要被日志，在日志等级之上

#### LoggingMXBean
日志设施的管理接口
如果该实例为全局唯一的LoggingMXBean 能够被LoggerManager#getLogginMXBean获取，或者java.lang.management.ManagementFactory#getPlatformMBeanServer 获取

### 抽象类
#### Handler
从Logger获取信息并导出，例如导出到文件，网络日志服务，或者导出到系统日志等
可以通过设置level 为OFF来关闭

#### Formatter
提供日志记录的格式化，

### 类
#### Level 日志等级 

#### Logger 日志记录器

#### Logging 
提供一个LoggingMXBean 的实现

#### LoggingPermission
修改Logging的权限控制

#### LoggingProxyImpl
sun.util.logging.LoggingProxy 的实现

#### LogManager 
全局唯一用来提供和维护日志记录器和日志服务


#### LogRecord
用来在日志框架和单独的log Handler之间传递日志请求的对象

#### StreamHandler
基于流的处理器

#### SocketHandler
推送日志给网络流

#### FileHandler
用来输出记录到文件中。提供滚动文件输出，当文件到达限定大小后，会自动打开新文件并加上数字后缀
配置：
.level
.filter 
.formatter
.encoding
.limit 限制大小
.count 循环文件个数
.parttern 输出文件名称模式
.append 追加日志

#### ConsoleHandler
用来输出记录到System.err上，默认使用SimpleFormatter。
配置：LoggerManager使用全限定类名来加载配置，否则的话使用默认配置
默认配置如下:
.level =Level.INFO
.filter=null
.formatter=java.util.logging.SimpleFormatter
.encoding=null

#### MemoryHandler
基于buffer的内存处理

## java.util.prefs

