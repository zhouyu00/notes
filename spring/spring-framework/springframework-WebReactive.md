> 5.2.6.RELEASE

这部分文档包含了对于基于Reactive Stream API的能够运行于非阻塞服务器，例如，Netty，Undertow，以及Servlet3.1+ 容器的响应式web应用。有独立的章节设计 Spring WebFlux框架，响应式客户端，测试支持，以及响应式库。对于Servlet技术路线的应用，请查看Web on Servlet Stack。

# 1.SpringWebFlux

最初的Web 框架包括Spring Framework，Spring Web MVC，因为Servlet容器和Servlet API。响应式Web框架在5.0版本以后添加的。它是全无阻塞的支持响应式流背压，并且能够运行在Netty，Undertow和Servlet3.1容器。

两个web框架都反映了它们的源模块（spring-webmcv和spring-webflux）和共同合作的名称。每个模块都是可选的。应用可以使用一个或者其他或者都用，例如，使用响应式**webclient**的Spring MVC 控制器。

## 1.1 Ovewview

为什么创建Spring WebFlux?

部分原因是因为需要使用少量线程和最大利用少量的硬件资源来使用非阻塞web栈来处理并发。Servlet3.1提供了非阻塞io。然而，使用它们意味着放弃了其他的ServletAPI，比如同步协议的（Fileter，Servlert）或者阻塞的（getParameter，getPart）。建立新的通用API作为任何运行时非阻塞的基础是最初的出发点。对于基于异步非阻塞建立的服务器（例如Netty），这是很重要的。

另一个答案是函数式编程。Java5添加的注解（例如，REST 控制器和单元测试），Java8添加的lambda表达式提供了函数式编程的可能性。这些对于称述式组织异步逻辑的非阻塞应用和连续风格的API（例如，**Completable**和**ReactiveX**）非常有益。在编程模型层面上，Java8允许Spring

WebFlux 提供函数式Web端点通过注解控制器。

### 1.1.1 Define "Reactive"

我们了解了“非阻塞”和“函数式”，但是"响应式"是什么意思？

术语“响应式”，指的是能够响应变化的编程模型——网络组件响应IO事件，UI控制器响应鼠标事件等。能够看出来，非阻塞就是响应式，因为区别于阻塞，我们现在只在操作完成和数据可用的情况下响应通知。

Spring team 有一个重要于“响应式”相关的机制，那就是非阻塞背压。在同步情况下，重要的代码，阻塞调用作为天然的背压机制来强制调用者等待。在非阻塞代码里，控制事件频率以保证一个较快的生产者不会压垮它的目的地是非常重要的。

Reactive stream 一定程度上（适配java9）定义了异步组件之间带背压的交互。例如，一个数据仓库（作为发布者的角色）能够生产数据，然后一个HTTP Server（作为订阅者）能够将数据学到恢复力。这里Reactive Streams的主要目的是使用订阅者来控制发布者的生产数据的速度。

> 常见问题，如果一个发布者无法慢下来怎么办？
>
> Reactive Stream的目的是建立机制和边界。如果一个发布者无法慢下来，那么需要决定是否使用缓存，丢弃或者失败

### 1.1.2 Reactive API

Reactive Streams 在互操作性上扮演重要角色。作为库和基础设施的组件它很有趣，但是对于应用API它没有那么有用，因为它有点太底层了。应用需要更高层一点，函数式的API来组织异步逻辑——类似于Java8 流API但是不仅仅于此。这就是reactive库所需扮演的角色。

Reactor 是Spring webFlux 的响应式库的选择。它提供**Mono**和**Flux**API类来在处理0..1(Mono)和0..N（Flux）数据流通过ReactiveX提供的操作符。Reactor是一个响应式的流库，而且，它的所有操作都支持非阻塞的背压。响应器聚焦于服务端Java。它发展出了紧密的同Spring的合作。

WebFlux需要Reactor作为核心依赖，但是它需要通过Reactive Stream与其他响应式库来进行互操作。作为通用规则，WebFlux API 接受一个空白的**Publisher**作为输入，适配到内部Reactor类型，并返回一个**Flux**或者**Mono**作为输出。因此你可以输入任何**Publisher**并且可以在输出上应用任何操作，但是你在使用其他响应式库的时候需要进行适配。无论如何可行的是（例如，注解控制器），WebFlux透明地适配RxJava的用法或者其他响应式库。查看Reactive LIbraries 获取更多细节。

> 另外的关于ReactiveAPI的，WebFlux 能够使用Kotlin提供的另外一种更重要的编程风格即Coroutines API。接下来的Kotlin样例中会提供协程API的写法。

### 1.1.3 Programming Models

**spring-web**模型包含了Spring WebFlux的响应式基础，包括HTTP抽象，Reactive Streams适配支持服务端，解码和核心**WebHandler**API兼容非阻塞式的ServletAPI。

在此基础上，Spring WebFlux提供两种编程模型选择：

* 注解控制器：与Spring MVC一致的，并且同样基于来自**spring-web**模块的注解。Spring MVC和WebFlux控制器同样支持响应式（Reactor和RxJava）返回类型，结果是，很难对它们进行区分。一个显著的分别是WebFlux也支持响应式**@RequestBody**参数。
* 函数式端点：基于Lambda，轻量，并且是函数式的编程模型。你可以将它看做一个小的库或者一套工具，能够用来路由和处理请求。它与注解控制器之间的最大区别是需要从开始到结束都进行处理，而注解控制器通过注解来声明目的，并被回调。

### 1.1.4 Applicability

Spring MVC 还是 WebFlux?

一个很自然的问题，但是基于不稳妥的二分法。实际上二者具有共同的部分并且具有各自的可选扩展。两者都有设计上的连续性和一致性，他们可以一起合作，并且从合作中获得好处。下面的图显示二者的联系，他们的共同点以及独特性：

![](E:\cyhome\notes\docs\spring\spring-framework\pic\mvcOrWebflux.JPG)

我建议你可以考虑下面的特点：

* 如果你使用的Spring MVC工作的很好，并且没有必要改变。重要的编程很好写，理解，以及排错。你最大的库函数选择余地，当然历史性的，很多都是阻塞式的
* 如果你已经考虑使用非阻塞web stack，Spring WebFlux 提供与其他同技术栈相同的模型优点，并且提供服务器的选择（Netty,Tomcat,Jetty,Undertow,以及Servlet3.1+容器），一个编程模型的选择（注解控制器和函数式web端点），以及一个响应式库（Reactor,RxJava,或者其他）。
* 如果你对轻量级，使用java8 Lamdba表达式或者Kotlin的函数式的web框架感兴趣，你可以使用Spring Web Flux函数式web端点。这对于小型应用及微服务，可以获益于它的更好的透明性和控制。
* 在微服务架构中，你可以拥有包括Spring MVC或者Spring WebFlux 控制器 或者Spring WebFlux的函数式端点的混合应用。在两种框架里支持相同的注解编程模型使得在为工作选择合适的工具重用知识更容易
* 一个简单的来评价应用的方法是检查它的依赖。如果你有阻塞式的持久化API（JPA，JDBC）等或者网络API，Spring MVC至少是最好的通用框架。技术上使用Reactor和RxJava在独立的线程上来进行阻塞调用是可行的，但是你无法用到大部分的非阻塞web栈
* 如果你一个需要调用远程服务的Spring MVC ，尝试一下响应式的**WebClient**。你可以直接从Spring MVC返回响应类型（Reactor,RxJava，或者其他）。每次调用的延迟越大或者调用之间具有相关性，则能获得更多的好处。Spring MVC控制器也能够调用其他响应式组件。
* 如果你有一个很大的团队，请记住切换到非阻塞函数声明式编程陡峭的学习曲线。除此之外，小范围开始并且权衡利弊。对于大范围的应用，这种切换是没有必要的，如果你不确定会带来什么好处，请学习非阻塞io的工作方式（例如，Nodejs单线程并发）以及它的影响。

### 1.1.5 Servers

Spring WebFlux 在 Tomcat，Jetty，Servlet3.1+容器，同时在运行时非Servlet容器如Netty和Undertow上被支持。所有的服务器适配到低层的，通用的API，以使得高层的编程模型能够在所有的服务器上被支持。

Spring WebFlux 没有内部支持开启或者关闭一个服务器。然而，它可以从Spring 配置和WebFlux基础设施通过几行代码快速的装配出一个应用。

Spring Boot 具有一个能够自动化这个过程的starter。默认地，这个Starter使用Netty，很容器能够切换到Tomcat，Jetty或Undertow通过更改你的Maven和Gradle依赖。Springboot默认使用Netty，因为他能够用于异步非阻塞的空间，并且能够使服务器和客户端共享资源。

Tomcat和Jetty能够同时使用Spring MVC和WebFlux。记住他们的用法是非常不同的。Spring MVC依赖于Servlet 阻塞IO和使应用直接使用ServletAPI，如果他们需要的话。Spring WebFlux 依赖于Serlvet3.1 非阻塞IO，基于底层适配器来使用ServletAPI。并不是没有封装的直接使用。

对于Undertow，Spring WebFlux 直接使用Undertow API而不使用Servlet API。

### 1.1.6 Performance性能

性能具有很多特征和意义。响应式和非阻塞并不总是使应用运行地更快。它们可以，（例如，如果使用**WebClient**并行地远程调用）。总的来说，非阻塞方式需要更多的工作，并且会轻微地增加需要的处理时间。

主要的预计的好处是，响应式和非阻塞能够充分利用少量的固定数目的线程和较少的内存。这使得应用加载时能够更具有弹性，因为他们以可预见的方式进行伸缩。为了观察这些优点，你需要具有一些延迟（包括混合的慢速和不可预测的io）。这通常是响应式栈展示它的力量的，之间的差距是很大的。

### 1.1.7 Concurrency Model并发模型

Spring MVC 和Spring WebFlux 支持注解控制器，但是在并发模型和默认的消耗阻塞线程之间有区别。

在Spring MVC（以及更广泛的servlet 应用），假设应用能够阻塞当前的线程，（例如，远程调用）。因为这个原因，Servlet 容器能够使用大量的线程池来吸收潜在的处理请求的阻塞。

Spring WebFlux（以及更广发的非阻塞服务器），假定应用不阻塞。因此，非阻塞服务器使用小规模的固定规模的线程池（时间循环工作器）来处理请求。

> "伸缩"和“小数目的线程”可能听起来矛盾，但是从不阻塞当前线程（依赖于回调），这意味着你不需要额外的线程，正如这里没有阻塞调用来吸收。

**Invoking a Blocking API**

如果你需要使用阻塞库怎么办？Reactor和RxJava同时提供**publishOn**操作来继续另外一个线程的处理。这意味着有一个简单逃生舱门。记住，阻塞API并不适合并发模型。

**Mutable State**

在Reactor和RxJava中，你通过运算符声明逻辑。在运行时，一个响应式的管道以不同的方式顺序地组织处理数据。一个关键的好处就是，它使得应用不需要保护可变状态。因为管道编码的应用从不并发地调用。

**Threading Model**

当一个服务器运行Spring WebFlux时，你希望看到什么线程？

* 在一个“普通的”Spring WebFlux 服务器（例如，没有数据接入也没有可选依赖），你可能期望看到一个服务器线程以及其他几个处理请求的线程（通常和CPU核心数一样）。Servlet 容器，许多启动时需要更多的线程（例如，在Tomcat上10个），在支持servlet（阻塞）IO和servlet3.1（非阻塞io）的情况下。
* 响应式**webClient**以事件循环风格来进行操作。因此你可以看到使用小规模的固定数目的处理线程（例如，**reactor-http-nio-**使用Reactor Netty connector）。然而，如果Reactor Netty用于客户端和服务器，两者默认共享事件循环资源
* Reactor和RxJava提供线程池的抽象，被称作调度器，来和切换处理到另外一个不同的线程池**publishOn**操作一起使用。调度器具有建议的并发策略的指定名称——例如，“并行”（对于限定数目的线程）或者“弹性”（对于大量线程由io约束的工作）。如果你查看这些线程，他意味着代码在使用指定的线程池**Scheduler**策略
* 数据访问库有自己其他第三方依赖能够自行创建和使用线程

**Configuring**

Spring Framework 不提供启动和关闭服务器的支持。为了配置服务器的线程模型，你需要使用服务端定制的配置API，或者你使用SpringBoot，检查每个服务器的SpringBoot配置选项。你可以直接配置**WebClient**，对于所有其他库，查看他们各自的文档。

## 1.2 Reactive Core 响应式核心

**spring-web**包含下面这些响应式web应用的功能支持：

* 对于服务器亲请求处理，有两个层次的支持：
  * HttpHandler：使用非阻塞io和Reactive Streams 背压的基本协议，提供了Reactor Netty，Undertow，Tomcat，Jetty 以及任何Servlet3.1+容器的兼容器。
  * **WebHandler** API：轻量的高层，泛用目的的用来处理请求的web API，基于具体的例如注解控制器和函数式端点编程模型之上建立

* 对于客户端，有一个基本的**ClientHttpConnector**协议来执行非阻塞和Reactive Stream 背压的HTTP请求，通过Reactor Netty和响应式Jetty HttpClient的适配器。应用中高层次的WebClient基于基本协议来建议。
* 对于客户端和服务器，解码器用于序列化和非序列化HTTP请求和回复内容。

### 1.2.1 HttpHandler

HttpHandler是一个具有一个方法来处理请求和回复的简单协议。它被有意地简化，它的主要和唯一目的就是作为不同HTTP服务器API上的最小抽象。

下面的表格描述了支持的服务器APIs：

| 服务器名称      | 使用的服务器API                                              | Reactive Streams 支持                               |
| --------------- | ------------------------------------------------------------ | --------------------------------------------------- |
| Netty           | Netty API                                                    | Reactor Netty                                       |
| Undertow        | Undertow API                                                 | spring-web:Undertow to Reative Stream 桥            |
| Tomcat          | Servlet3.1 非阻塞IO；Tomcat API用于读写ByteBuffers vs byte[] | spring-web:Servlet3.1 非阻塞IO到 Reactive Stream 桥 |
| Jetty           | Servlet3.1 非阻塞IO；Tomcat API用于读写ByteBuffers vs byte[] | spring-web:Servlet3.1 非阻塞IO到 Reactive Stream 桥 |
| Servlet 3.1容器 | Servlet3.1非阻塞IO                                           | spring-web:Servlet3.1 非阻塞IO到 Reactive Stream 桥 |

下面的表格描述了服务器依赖：

| 服务器名称    | Group id                | Artifact Name               |
| ------------- | ----------------------- | --------------------------- |
| Reactor Netty | io.projectreactor.netty | reactor-netty               |
| Undertow      | io.undertow             | undertow-core               |
| Tomcat        | org.apache.tomcat.embed | tomcat-embed-core           |
| Jetty         | org.eclipse.jetty       | jetty-server, jetty-servlet |

下面的小段代码展示了使用**HttpHandler**来适配每个服务器API：

**Reactor Netty**

```java
HttpHandler handler =...;
ReactorHttpHandlerAdapter adapter = new ReactorHttpHandlerAdapter(handler);
HttpServer.create().host(host).port(port).handler(adpater).bind().block();
```

**Undertow**

```java
HttpHandler handler=...;
UndertowHttpHandlerAdapter adapter = new UndertowHttpHandlerAdapter(handler);
Undertow server = Undertow.builder.addHttpListener(port,host).setHandler(adapter).build();
server.start();
```

**Tomcat**

```java
HttpHandler handler = ...;
Servlet servlet = new TomcatHttpHandlerAdapter(handler);

Tomcat server = new Tomcat();
File base = new File(System.getProperty("java.io.tmpdir"));
Context rootContext = server.addContext("",base.getAubsolutePath());
Tomcat.addServlet(rootContext,"main",servlet);
rootContext.addServletMappingDecoded("/","main");
server.setHost(host);
server.setPort(port);
server.start();
```

**Jetty**

```java
HttpHandler handler = ...;
Servlet servlet = new JettyHttpHandlerAdapter(handler);

Server server = new Server();
ServletContextHandler contextHandler = new ServletContextHandler(server,"");
contextHandler.addServlet(new ServletHolder(servlet),"/");
contextHandler.start();

ServerConnector connector = new ServerConnector(server);
connector.setHost(host);
connector.setPort(port);
server.addConnector(connector);
server.start();
```

**Servlet 3.1+ Container**

为了作为WAR部署到Servlet3.1+容器，你可以扩展和包含**AbstractReactiveWebInitializer**在WAR包中，这个类将HttpHandler包装为**ServletHttpHandlerAdapter**并且注册为**Servlet**。

### 1.2.2 WebHandler API

**org.springframework.web.server**包基于**HttpHandler**协议来提供给一个通用目的的通过一个链的多个**WebExceptionHandler**，多个**WebFilter**以及一个**WebHandler**组件的webAPI。这个链可以使用**WebHttpBuilder**将其组合起来，通过简单将其自动探测组件和注册组件builder的Spring **ApplicationContext**。

在**HttpHandler**有一个简单的目标来抽象不同的HTTP服务器的用法，**WebHandler** API目标是提供一套更广泛的常用在web应用中的特征：

* 带属性的User 会话
* 请求属性
* 解析请求的**Locale**和**Principal**
* 解析和缓存数据的方法
* multipart 数据的抽象
* 更多...



### 1.2.3 Filters

### 1.2.4 Exceptions

### 1.2.5 Codecs

### 1.2.6 Logging



# 2.WebClient



# 3.WebSockets

# 4.Testing

# 5.RSocket

# 6.Reactive Libraries

