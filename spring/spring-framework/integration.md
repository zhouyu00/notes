# 8. 缓存抽象

## 8.1 理解缓存抽象
...
缓存抽象提供了其他缓存相关的操作，比如能够更新缓存内容或者一处一个或者所有缓存。在缓存处理在应用过程中改变的数据这些都很有用。

正如其他Spring Framework中的其他服务，缓存服务是一个抽象的（不是缓存实现）并且需要实际的存储介质来存储缓存的数据，这意味这个抽象帮助你来写缓存逻辑，但是并不提供实际的数据存储，这个抽象。这个抽象通过**org.springframework.cache.Cache**和**org.springframework.cache.CacheManager**接口来实现。

Spring提供少量的抽象的实现：JDK**java.util.concurrent.CocurrentMap**基于缓存，Ehcache2.x,Gemfire cache,Caffeine,和JSR-107一致缓存（例如Ehcache3.x)。查看Plugging-in Different Back-end Caches 来获取更多信息关于插入其他的缓存和提供商。

> 缓存抽象没有针对多线程和多进程环境进行特别的护理，这样的特性可以在缓存实现中进行处理

如果你具有多进程环境（例如，一个应用更需要部署多个节点），你需要根据你的缓存提供商来进行缓存配置。取决于你使用的示例，相同数据的拷贝部署在几个节点足够。然而如果你在应用的过程中更改数据，你需要启用其他的传播机制。

缓存这个术语等同于典型的“获取如果没找到就执行并最终放置”的符合编程缓存的代码块。没有锁使用，并且多个线程会同时加载相同项目。这些场景类似于“驱逐”。如果多个线程需要并发地升级或者清理数据，你可能会使用到脏数据。确定的缓存提供商在这个领域提供先进的特征。查看你的缓存提供商的文档以获取更多细节。

为了使用缓存抽象，你需要注意两个方面：

*  缓存声明：确定需要缓存的方法及缓存策略
*  缓存配置：数据存储和读取的后台缓存

## 8.2  基于注解的申明式注解

对于缓存声明，Spring的缓存抽象提供各类一套Java注解：

* @Cacheable:触发缓存
* @CacheaEvict：触发缓存清理
* @CachePut:允许不经过查询进行缓存内容更新
* @Caching:重组应用到同一个方法的多个缓存操作
* @CacheConfig: 在类级别共享很多通用的缓存相关的设置

### 8.2.1 @Cacheable 注解
正如名称所说，你可以使用@Cacheable来装饰方法表示它们是可缓存的——即，该方法调用结果会被缓存，相同参数的调用的值会被直接返回不用再调用方法。在它的最简形式下，注解声明需要缓存相关的名称，如下所示：
```java
@Cacheable("books")
public Book findBook(ISBN isbn) {...}
```
在前面的代码段中，findBook方法关联到缓存中的books。每次方法被调用，缓存回去检查调用是否已经进行不用再次重复。在大多数的例子下，只有一个缓存被声明，注解使多个名称被指定以使用不止一个缓存。在这个例子中，方法被调用后，每个缓存被检查，如果击中了一个缓存，就返回相应的值。

> 所有其他的缓存不包含值的也会被更新，尽管缓存方法并没有调用

下面的方法使用了@Cacheable 在findBook方法上：
```java
@Cacheable({"books","isbns"})
public Book findBook(ISBN isbn){...}
```

#### Default Key Generation

既然缓存都是键值对存储方式，每个缓存方法的调用需要为缓存访问传入一个恰当的键。缓存抽象使用简单的KeyGenerator基于下面的算法：
* 如果没有给定任何参数，返回SimpleKey.EMPYT
* 如果给定一个参数，返回该实例
* 如果给定超过一个参数，返回包括所有参数的SimpleKey

这个方法对于大多数情况是适用的，尽管参数有着自然的键以及实现了有效的hashCode()和equals()方法。如果不是这种情况，你需要改变策略。

为了提供不同的默认的key生成器，你需要实现**org.springframework.cache.interceptor.Keygeneraotr**接口。

>默认的key生成策略，在Spring4.\0及更早的版本中使用的生成策略，对于多键策略，考虑参数的hashCode()而不是equals()。这可能给造成想不到的键冲突（查看 SPR-10237了解相关背景）。新的SimpleKeyGenerator 使用一个复合的键来应对这样的场景。
>如果你希望保持前面的键策略，你可以配置过期的**org.springframework.cache.intercepter.DefaultKeyGenerator**类或者创建一个定制的基于哈希的**KeyGenerator**实现。

#### 定制键生成声明
既然缓存是通用的，目标方法很可能具有不同签名，使得不能从缓存结构的头部获得映射。这在目标方法具有很多个参数，而只有其中一些适合缓存（其他通过方法逻辑）的时候显得尤其明显。考虑下面的例子：
```java
@Cacheable("books")
public Book findBook(ISBN isbn,boolean checkWarehouse,boolean includeUsed)
```
第一眼，当两个boolean参数影响book是否被找到，它们都不能使用缓存。另外的，如果如果两个中间一个很重要，但是另外的不是怎么办？

对于这样的例子，@Cacheable 注解使你指定键通过key属性如何生成。你可以使用SpEL来选择有用的参数（或者他们嵌套的属性），执行操作，甚至调用任意的方法而不是通过任何的代码或者实现各种借口。这是在使用默认的生成器的时候的推荐的方法，既然在代码增长时，各方法签名非常不同。当默认的策略可能对一些方法起作用时，但是他不一定对所有的方法都有效。

下面的例子使用了各种SpEL声明（如果你不熟悉SpEL，自己努力一下读一下Spring Expression Language)：
```java
@Cacheable(cacheNames="books", key="#isbn")
public Book findBook(ISBN isbn, boolean checkWarehouse, boolean includeUsed)

@Cacheable(cacheNames="books", key="#isbn.rawNumber")
public Book findBook(ISBN isbn, boolean checkWarehouse, boolean includeUsed)

@Cacheable(cacheNames="books", key="T(someType).hash(#isbn)")
public Book findBook(ISBN isbn, boolean checkWarehouse, boolean includeUsed)
```
前面的代码展示了选择一个特定的参数或者它的属性如何简餐，或者一个任意的（静态）方法。
如果一个算法负责生成键并且它需要被共享，你可定义一个keyGenerator。为了做到这个，指定KeyGenerator的将被使用的实现bean的名称，如下面所示：
```java
@Cacheable(cacheNames="books", keyGenerator="myKeyGenerator")
public Book findBook(ISBN isbn, boolean checkWarehouse, boolean includeUsed)
```
> key和keyGenerator 参数是手动互斥的，如果同时指定两个参数会抛错

#### 默认的缓存结果
缓存抽象使用一个简单的**CacheResolver**能够取到在操作等级通过使用CacheManager定义的缓存。
为了提供一个不同的默认缓存解析器，你需要实现**org.springframework.cache.intercepter.CacheResovler**接口。

#### 定制缓存解决方案
默认的缓存方案非常适合和一个单一的缓存管理器，并且没有复杂的缓存解决需求。
对于和多个缓存管理器工作的应用，你可以为每个操作哦设置对应的cacheManager,如下例子所示：
```java
@Cacheable(cacheNames="books", cacheManager="anotherCacheManager") 
public Book findBook(ISBN isbn) {...}
```
你可以完勉强全替代CacheResolver采用类似于取代key 生成器。如果方案对于每个缓存操作都需要，使得实现根据实时参数来处理缓存使用。下面的例子展示了如何来指定CacheResolver:
```java
@Cacheable(cacheResolver="runtimeCacheResolver")
public Book findBook(ISBN isbn){...}
```

> 自从Spring4.1版本后，缓存注解的value属性不再是强制的，因为限制信息可以通过CacheResolver提供而不是注解内容
> 类似于key和keyGenerator,cacheManager和cacheResolver参数是手动互斥的，同时的指定会抛错。CacheResolver会导致定制的CacheManager失效。这可能不是你想要的。

#### 同步缓存
在一个多线程环境中，特定的操作可能被并发地使用相同的参数（典型的启动）调用多次。默认的缓存抽象不锁任何内容，相同的值可能被计算多次，这与缓存的目的是冲突的。
对于这些特殊的情况，你需要使用sync属性来使得底层的cache提供商来锁定cache入口，当值正在被计算的时候。这样的结果，只有一个线程会计算值，而其他的线程被block直到缓存中的入口被更新。下面的例子展示了如何使用sync属性：
```java
@Cacheable(cacheNames="foos",sync=true)
public Foo executeExpensiveOperation(String id){...}
```

> 这是一个可选的特性，并且你喜欢的缓存库可能不支持。所有的有springframework核心库提供的CacheManager实现支持它。查看你的缓存提供商的文档来获取更多细节。

#### 条件缓存
有时候，一个方法可能不适合在所有的时候都进行缓存（例如，它可能取决于输入参数）。这个缓存注解通过使用SpEL表达式来判断true和false的condition参数来支持这样的用例。如果true，方法就被缓存。如果不是，它表现的像没有进行缓存（即，每次方法都会被调用，不管值是否已经被缓存或者使用了什么参数）。例如，下面的方法只有参数name使用短于32的长度才会被缓存：
```java
@Cacheable(cacheNames="book",condition="#name.length() < 32")
public Book findBook(String name)
```
作为contidiotin的附加参数，你可以使用unless来拒绝添加值到缓存。不同于condition，unless表达式在方法调用后被计算。为了扩展前面的例子，可能我们只想缓存平装版书籍，如下所示：
```java
@Cacheable(cacheNames="book", condition="#name.length() < 32", unless="#result.hardback") 
public Book findBook(String name)
```
缓存抽象支持java.util.Optional，只有它是有值的时候缓存它的内容。#result总是引用商业实体，而不是一个支持的包装器，因此前面的例子可以如下所示：
```java
@Cacheable(cacheNames="book", condition="#name.length() < 32", unless="#result?.hardback")
public Optional<Book> findBook(String name)
```

#### 可用的SpEL评价上下文
每个SpEL表达式依据于专用的context来评价。对于内置的参数，framework提供专用的缓存相关的元数据，例如参数名称。下面表格描述了上下文可用的项目，你可以用作key和条件计算。
| Name |Location|Description|Example|
|-----|-----|-----|-----|
|methodName|Root object|调用的方法名|#root.methodName|
|method|Root object|调用的方法|#root.method.name|
|target|Root object|调用的目标对象|#root.target|
|targetClass|Root object|调用的目标类|#root.targetClass|
|args|Root object|用于调用目标的参数（作为数组）|#root.args[0]|
|caches|Root object|当前方法调用的缓存集合|#root.caches[0].name|
|Argument name|Evaluation context|任意方法参数的名称，如果名称是不可用的（可能因为没有debug信息），参数名也可以在#a<#arg>下取得#arg代表参数索引|#iban或者#a0（你可以使用#p0或者#p<#arg>符号作为别名）|
|result|Evaluation context|方法调用的结果（缓存的值），只在unless表达式中，cache put表达式（计算key），或者cache evict 表达式（当 beforeInvocation是false）。对于支持的wrappers（例如Optional），#result引用实际的结果，而不是wrapper|#result|

### 8.2.2 @CachePut 注解
当缓存需要不在方法执行的介入下进行更新时，你可以使用@CachePut注解。这意味着方法总是被调用，它的结果总是被放入缓存（根据@CachePut选项）。它支持和@Cacheable相同的选项并且应当被用于缓存增长，而不是方法流优化。下面的例子使用了@CachePut annotation:
```java
@CachePut(cacheNames="book",key="#isbn")
public Book updateBook(ISBN isbn,BookDescriptor descriptor)
```
> 在相同的方法上使用@CachePut和@Cacheable注解强烈不推荐，因为它们具有不同的行为。当后者会导致方法调用跳过通过使用缓存，前者强制调用方法为了进行缓存更新。这会导致不受期待的行为，以及特殊边界情况的异常（例如，注解拥有互相排斥的条件），这样的声明应当被避免。需要强调的是，这样的条件不应当依赖于结果对象（即，#result变量），正如这些条件被验证有效提前到证实互斥

### 8.2.3 @CacheEvict注解
缓存抽象允许不仅是缓存存储的增长也包括清理。这个对于从缓存中移除脏的或者未使用的数据非常有用。与@Cacheable相反,@CacheEvict装饰的方法会执行缓存清理（即，方法的调用触发从缓存中移除数据）。类似于它的兄弟，@CacheEvict需要指定一个或者多个被该动作影响的的缓存，它可以使用传统的缓存和key方案或者指定条件，并且具有一个额外的参数(allEntries)意味将进行全缓存清理，而不只是（基于key）进行一个入口的清理。下面是例子:
```java
@CacheEvict(cacheNames="books", allEntries=true) 
public void loadBooks(InputStream batch)
```
这个选项在需要清理整个缓存区域的时候非常方便。不同于清理单个入口（将占用较长时间，因为它效率不高），所有的缓存将通过一个操作被清理，正如前面例子所展示的那样。这意味着，框架将忽视任何入口在这种场景下因为它不起作用（整个缓存被清理，而不是一个入口）。

你也可以通过使用beforeInvocation属性来配置清理是否在方法调用之后或者之前进行（默认在方法调用之后）。前者提供了与其他注解相同的语义，一旦方法成功完成，执行一个在缓存上的动作（在这里是清理）。如果一个方法没有被调用（可能被缓存），或者抛出异常，清理就不会发生。后者(beforeInvocation=true)导致清理总是发生在方法调用之前。这在某些场景下很有用，因为它并不依赖于方法是否成功调用。

### 8.2.4 @Caching
有时候，多个同类的注解需要进行配置（例如@CacheEvict或者@CachePut），例如，因为在不同的缓存上具有不同的condition和key表达式。@Cacheshide 使得多个嵌套的@Cacheable,@CachePut和@CacheEvict注解被用于同一个方法，下面展示了使用两个注解的情况:
```java
@Caching(evict = { @CacheEvict("primary"), @CacheEvict(cacheNames="secondary", key="#p0") })
public Book importBooks(String deposit, Date date)
```

### 8.2.5 @CacheConfig
到目前为止，我们已经看到了缓存操作提供了很多定制的选项，你可以为每个操作设置这些选项。然而，一些需要应用所有类的操作显得非常麻烦。例如，定义到每个操作的cache名称可以被定义到单个类级别的提到。这就是@CacheConfig的用处。下面的例子展示了使用@CacheConfig来设定缓存名：
```java
@CacheConfig("books") 
public class BookRepositoryImpl implements BookRepository {

    @Cacheable
    public Book findBook(ISBN isbn) {...}
}
```
@CacheConfig 是一个允许共享缓存名称，KeyGenerator,CacheManager,和CacheResolver的类级别的注解。放置这个注解在类上并不开启任何缓存操作。
一个操作级别的定制总是重载在@CacheConfig上的定制。因此这为每个缓存操作给定了三个级别的定制：
* 全局的，对CacheManager,KeyGenerator有效
* 类级别的使用@CacheConfig
* 一个操作级别的

### 8.2.6 启用缓存注解
一个很重要的事情就是声明缓存注解并不能自动开启它们的功能。和Spring中的其他很多操作一样，这个共需要被声明式启用（这意味着如果你觉得缓存具有负面作用，你可以禁用它通过移除一行配置而不是所有代码中的注解）。
为了启用缓存通过在你的一个@Configuration中添加@EnableCaching：
```java
@Configuration
@EnableCaching
public class AppConfig {
}
```
同样的，xml配置你可以通过使用cache:annotation-driven元素：
```xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:cache="http://www.springframework.org/schema/cache"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/cache https://www.springframework.org/schema/cache/spring-cache.xsd">

        <cache:annotation-driven/>
</beans>
```
上述两种方式都可以让你指定多个选项来影响通过AOP添加到系统中的缓存的行为。这种配置有意地被设置成了和@Transacitonal类似的方式。

> 处理缓存注解的默认通知模式是proxy，允许仅仅通过代理来拦截所有的调用。相同类的本地调用不能通过这种方法来进行拦截。至于更先进的拦截模式，考虑切换到aspectj模式来结合编译期和加载期的织入。

> 对于更多使用CachingConfigurer的有关先进配置（使用java配置），查看javadoc

|XML Attribute| Annotation Attribute| Default| Description|
|-------------|---------------------|--------|------------|
|cache-manager|N/A(请见CachingConfiurer javadoc)|cacheManager|使用的缓存管理器的名称。一个默认的CacheResolver 使用这个缓存管理器透明地初始化(或者如果没有设置的话使用cacheManager)。对于缓存方案更加细粒度的管理，考虑设置cacheresolver属性|
|cache-resolver|N/A(请见CachingConfiurer javadoc)|使用cacheManager的SimpleCacheResolver|CacheResolver的bean名称被用来删除底层的缓存。这个属性不是必须的，只是作为cache-manager属性的一个替代|
|key-generator|N/A(请见CachingConfiurer javadoc)|SimpleKeyGenerator|定制的键生成器的名称|
|error-handler|N/A(请见CachingConfiurer javadoc)|SimpleCacheErrorHandler|定制的缓存错误处理器的名称。默认的，任何缓存操作相关的抛出的错误在客户端抛出|
|mode|mode|proxy|默认的模式(proxy)通过SpringAOP框架处理注解来进行代理（遵从代理语义，正如前面所讨论的，将代理应用到方法进入代理的调用）。可替代的模式(aspectj)则织入受影响的类通过Spring AspectJ 缓存切面，调整目标类的字节码来应用到任何类的方法调用上。AspectJ 织入需要在加载期织入或者编译期织入启用并且Spring-aspects.jar在classpath下。（查看Spring configuration 获取细节关于如何设置加载期织入)|
|proxy-target-class|proxyTargetClass|false|只应用于proxy模式。控制为带有@Cacheable和@CacheEvict注解的类产生什么类型的缓存代理。如果proxy-target-class属性被设定为true，产生基于类的代理。如果proxy-target-class是false或者这个属性被忽略，标准的jdk基于接口的代理被创建。（查看Proxying Mechanisms 获取不同代理类型的细节考量）|
|order|order|Ordered.LOWEST_PRECEDENCE|注解到bean上的@Cacheable或者@CacheEvit的缓存通知顺序。（对于更多信息关于排序AOP通知，查看Advice Ordering）不指定排序意味着AOP子系统来决定通知顺序。|

> <cache:annotation-driven/>只查找与它定义在同一个application context下的bean中的@Cacheable/@CaChePut/@CacheEvict/@Caching。这意味着，如果你将<cache:annotation-driven/>放在WebApplicationContext中来配置DispatcherServlet，它只会检查你控制器中的bean，而不是你的服务。查看the MVC section 来获取更多信息

> ###  方法可见性与缓存注解
> 当你使用代理，你需要应用缓存注解到public可见性的方法上。如果你在protected，private或者包可见性的方法上使用了注解，不会报错，但是这些注解的方法也不会表现出注解配置的功能。考虑使用AspectJ（请看这部分余下内容）如果你需要注解非public方法，那么会改变它本身的字节码。

> Spring推荐你只用@Cache\*注解具体的类（和具体类的方法），相比于注解接口。你可以将@Cache\*放在接口上（或者接口方法上），但是它只有在你使用基于接口代理的时候起作用。这个Java注解不从接口继承的事实意味着，如果你使用基于类的代理(proxy-target-class="true")或者基于织入的切面（mode="aspectj"），这个缓存设置不会被代理或者织入机制检测到，这个对象不会被封装到一个缓存代理中。