
- [1 Spring Web MVC](#1-spring-web-mvc)
  - [1.1 DispatcherServlet](#11-dispatcherservlet)
    - [1.1.1 Context 层级结构](#111-context-层级结构)
    - [1.1.2 特殊Bean类](#112-特殊bean类)
    - [1.1.3 Web MVC Config](#113-web-mvc-config)
    - [1.1.4 Servlet Config](#114-servlet-config)
    - [1.1.5 Processing](#115-processing)
    - [1.1.6 Interception](#116-interception)
    - [1.1.7 Exceptions](#117-exceptions)
      - [解析链](#解析链)
      - [容器错误页](#容器错误页)
    - [1.1.8 View Resolution](#118-view-resolution)
      - [Handling](#handling)
      - [Redirecting](#redirecting)
      - [Forwarding](#forwarding)
      - [Content Negotiation](#content-negotiation)
    - [1.1.9 Locale](#119-locale)
      - [Time Zone](#time-zone)
      - [Header Resolver](#header-resolver)
      - [Cookie Resolver](#cookie-resolver)
      - [Session Resolver](#session-resolver)
      - [Locale Interceptor](#locale-interceptor)
    - [1.1.10 Themes](#1110-themes)
      - [定义主题](#定义主题)
      - [解析主题](#解析主题)
    - [1.1.11 Multipart Resolver](#1111-multipart-resolver)
      - [Apache Commons Fileupload](#apache-commons-fileupload)
    - [1.1.12 Logging](#1112-logging)
      - [Sensitive Data](#sensitive-data)
  - [1.2 Filters](#12-filters)
    - [1.2.1 Form Data](#121-form-data)
    - [1.2.2 Forwarded Headers](#122-forwarded-headers)
    - [1.2.3 Shallow ETag](#123-shallow-etag)
    - [1.2.4 CORS](#124-cors)
  - [1.3 Annotated Controllers](#13-annotated-controllers)
    - [1.3.1 Declaration](#131-declaration)
      - [AOP Proxies](#aop-proxies)
    - [1.3.2Reuqest Mapping](#132reuqest-mapping)
      - [URL patterns](#url-patterns)
    - [1.3.5 DataBinder](#135-databinder)
  - [1.4 Functional Endpoints](#14-functional-endpoints)
  - [1.5 URI Links](#15-uri-links)
  - [1.6 Asynchronous Requests](#16-asynchronous-requests)
  - [1.7 CORS](#17-cors)
  - [1.8 HTTP Caching](#18-http-caching)
  - [1.10 View Technologies](#110-view-technologies)
  - [1.11 MVC Config](#111-mvc-config)
    - [1.11.1 Enable MVC Config](#1111-enable-mvc-config)
    - [1.11.2 MVC Config API](#1112-mvc-config-api)
    - [1.11.3 Type Conversion](#1113-type-conversion)
    - [1.11.4 Validation](#1114-validation)
    - [1.11.5 Interceptors](#1115-interceptors)
    - [1.11.6 Content Types](#1116-content-types)
    - [1.11.7 Message Converters](#1117-message-converters)
  - [1.12 HTTP/2](#112-http2)
- [2.REST Clients](#2rest-clients)
  - [2.1 RestTemplate](#21-resttemplate)
  - [2.2 WebClient](#22-webclient)
- [3. Testing](#3-testing)
- [4. WebSockets](#4-websockets)
  - [4.1 WebScoket 介绍](#41-webscoket-介绍)
    - [4.1.1 HTTP Versus WebSocket](#411-http-versus-websocket)
    - [4.1.2  When to Use WebSocket](#412-when-to-use-websocket)
  - [4.2 WebSocket API](#42-websocket-api)
    - [4.2.1 WebSocket Handler](#421-websocket-handler)
    - [4.2.2 WebSocket 握手](#422-websocket-握手)
    - [4.2.3 部署Deployment](#423-部署deployment)
    - [4.2.4 Server Configuration](#424-server-configuration)
    - [4.2.5 Allowed Origins](#425-allowed-origins)
  - [4.3 SockJS Fallback](#43-sockjs-fallback)
    - [4.3.1 Overview](#431-overview)
    - [4.3.2 Enbaling SockJS](#432-enbaling-sockjs)
    - [4.3.3 IE8 和9](#433-ie8-和9)
    - [4.3.4 心跳](#434-心跳)
    - [4.3.5 客户端切断连接](#435-客户端切断连接)
    - [4.3.6 SockJS和CORS](#436-sockjs和cors)
    - [4.3.7 SockJsClient](#437-sockjsclient)
    - [4.4 STOMP](#44-stomp)
    - [4.4.1 Overview](#441-overview)
    - [4.4.2 优点](#442-优点)
    - [4.4.3 Enable STOMP](#443-enable-stomp)
    - [4.4.4 WebSocket Server](#444-websocket-server)
    - [4.4.5 Flow of Messages 信息流](#445-flow-of-messages-信息流)
    - [4.4.6 Annotated Controllers](#446-annotated-controllers)
      - [@MessageMapping](#messagemapping)
          - [支持的方法参数](#支持的方法参数)
        - [Return Values](#return-values)
      - [@SubscribeMapping](#subscribemapping)
      - [@MessageExceptionHandler](#messageexceptionhandler)
    - [4.4.7 发送信息Sending Messages](#447-发送信息sending-messages)
    - [4.4.8 Simple Broker](#448-simple-broker)
    - [4.4.9 External Broker 外部broker](#449-external-broker-外部broker)
    - [4.4.10 连接到Broker](#4410-连接到broker)
    - [4.4.11 Dots as Sperator使用点作为分隔符](#4411-dots-as-sperator使用点作为分隔符)
    - [4.4.12认证Authentication](#4412认证authentication)
    - [4.4.13 Token 认证](#4413-token-认证)
    - [4.4.14 User Destination 用户目的地](#4414-user-destination-用户目的地)
    - [4.4.15 信息顺序Order of Message](#4415-信息顺序order-of-message)
    - [4.4.16 Events 事件](#4416-events-事件)
    - [4.4.17 Interception 拦截](#4417-interception-拦截)
    - [4.4.18 STOMP 客户端](#4418-stomp-客户端)
    - [4.4.19 WebSocket Scope](#4419-websocket-scope)
    - [4.4.20 性能](#4420-性能)
    - [4.4.21 Monitoring 监控](#4421-monitoring-监控)
      - [Client WebSocket Sessions](#client-websocket-sessions)
    - [4.4.22 Testing](#4422-testing)
- [5 Other Web Frameworks](#5-other-web-frameworks)

version5.2.6

这部分文档覆盖了基于ServletAPI构建的以及部署到Servlet容器的servlet-stack网页应用。独立章节包括SpringMVC，View Technologies，CORS Support，和 WebSocke支持。reactive-stack应用，请看Web on Reactive Stack

# 1 Spring Web MVC

Spring Web MVC 是基于ServletAPI的原生web框架，并且从一开始就被纳入Spring Framework之内。正式名称来自于它的源模块（spring-webmvc）,但是更被人熟知的名称是“Spring MVC”。

与Spring Web MVC并列的，Spring Framework 5.0 引入了 reactive-stack web框架，名叫“Spring WebFlux”，基于其源模块spring-webflux。这部分包含了Spring Web MVC。下一部分包含Spring WebFlux。

对于Servlet容器及JavaEE 版本的基本的信息和兼容性，请看Spring Framework wiki。

## 1.1 DispatcherServlet

Spring MVC ,正如大多数其他Web框架一样，是围绕一个中心的Serlvet前端控制器，**DispatcherSerlet**设计的，提供了共享的算法来处理请求过程，并可以通过可配置的代表模块来控制其实际工作。这个模型非常灵活并可以支持多种工作流。

**DispatcherServlet**，同任何Serlvet一样可以被声明并且根据Serlvet的Java配置或者**web.xml**文件进行映射。同样的，**DispatcherServlet**使用Spring的配置来发现需要请求映射、视图解析、异常处理及其他功能的代表模块。

接下来的例子展示了Java配置方式注册和初始化**DispatcherServlet**，Serlvet容器会自动探测到该过程（在Serlvet Config查看）。

```java
public class MyWebApplicationInitializer implements WebApplicationInitializer{
	@Override
	public void onStartup(ServletContext servletCxt){
		//Load Spring web application configuration
		AnnotationConfigWebApplicationContext ac = new AnnotationConfigWebApplicationContext();
		ac.register(AppConfig.class);
		ac.refresh();
		
		//Create and register the DispatcherSerlet
		DispatcherServlet servlet = new DispatcherServlet(ac);
		ServletRegistration.Dynamic registration = servletCxt.addServlet("app",servlet);
		registration.setLoadOnStartup(1);
		registration.addMapping("/app/*");
	}
}
```

>除了直接使用ServletContextAPI之外，你也可以扩展 AbstractAnnotationConfigDispatcherSerlvetinitializer并且覆盖特定的方法，查看下面的上下文集成

下面是**web.xml**配置方式注册和初始化DispatcherServlet:

```xml
<web-app>
	<listener>
		<listener-class>org.framework.web.context.ContextLoaderListener</listener-class>
	</listener>
	
	<context-param>
		<param-name>contextConfigLocation</param-name>
		<param-value>/WEB-INF/app-context.xml</param-value>
	</context-param>
	
	<servlet>
		<servlet>app</servlet>
		<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet>
		<init-param>
			<param-name>contextConfigLocation</param-name>	
            <param-value></param-value>
		</init-param>
		<load-on-startup>1</load-on-startup>
	</servlet>
	
	<serlvet-mapping>
		<servlet-name>app</servlet-name>
		<url-pattern>/app/*</url-pattern>
	</serlvet-mapping>
</web-app>
```

>SpringBoot 具有不同的初始化序列。不同于挂载到Servlet容器的声明周期上，SpringBoot 使用Spring配置来启动他自己和嵌入的Servlet容器。**Filter**和**Servlet**被在Spring配置中探测到并注册到Servlet容器中。更多细节请见SpringBoot文档。

### 1.1.1 Context 层级结构

**DispatcherServlet**等待**WebApplicationContext**（一个普通ApplicationContext的扩展）来进行自我配置。**WebApplicationContext**持有ServletContext和相关的Servlet的引用。它绑定到ServletContext如果他们需要使用的话以使用RequestContextUtils的静态方法来查找WebApplicationContext。

对于很多应用，有单个**WebApplication**很简单并且足够。但是使用context层级结构实现多个**DispatcherServlet**（或者其他的Servlet）实例每个都具有自己的**WebApplicationContext**配置并且共享同一个根**WebApplication**是可能的。查看Additional Capablities of the Applicaiton 获得更多ApplicationAontext 的层级结构特征。

根**WebApplicationContext**包括基础设施bean，例如数据仓库，商业服务以及其他需要被多个Servlet共享的而服务。这些beans可以被有效集成并且可以被**WebApplicationContext**Servlet特定的含有本地beans子类重写。接下来的图像展示了这个关系：

![层级关系](.\pic\层级关系.JPG)

接下来的例子配置了一个**WebApplicationContext** 层级关系：

```java
public class MyWebAppInitializer extends AbstractAnnotationConfigDispatcherServletInitializer{
	@Override
    protected Class<?>[] getRootConfigClasses(){
        return new Class<?>[]{RootConfig.class};
    }
    @Override
    protected Class<?>[] getServletConfigClasses(){
        return new Class<?>[]{App1Config.class};
    }
    @Override
    protected String[] getServletMapping(){
        return new String[]{"/app1/*"};
    }
}
```

>如果应用上下文层级结构没有提供，应用可以通过**getRootConfigClasses**返回所有配置**getServletConfigClasses()**返回**null**

下面的例子展示了**web.xml**的等价表示

```xml
<web-app>

    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>

    <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>/WEB-INF/root-context.xml</param-value>
    </context-param>

    <servlet>
        <servlet-name>app1</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>/WEB-INF/app1-context.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>

    <servlet-mapping>
        <servlet-name>app1</servlet-name>
        <url-pattern>/app1/*</url-pattern>
    </servlet-mapping>

</web-app>
```



>如果一个应用的层级结构没有提供，应用会配置一个“根”应用上下文并且保留**configConfigLocation**参数为空

### 1.1.2 特殊Bean类

**DispatcherServlet**代表特殊的能够处理请求和渲染合适回复的bean。“特殊bean”这里指实现了框架协议并且被Spring管理的对象。它们通常遵循内置的协议，但是你可以定制它们的属性和扩展来替代它们。

接下来的表格列出了能够被**DispatcherSerlvet**检测到的特殊bean：

| Bean type                | Explanation                                                  |
| :----------------------- | ------------------------------------------------------------ |
| HanderMapping            | 映射请求到handler通过一列表的intercpetors进行pre和post处理。映射基于一定的原则，细节取决于**HandlerMapping**实现</br>两个主要的**HandlerMapping**实现为**RequestMappingHandlerMapping**（支持**@RequestMapping**注解方法）和**SimpleUrlHandlerMapping**（维护清楚的URI路径模式注册到handlers） |
| HandlerAdapter           | 帮助handler映射到请求而不管handler是如何调用的。例如调用一个注解的控制器需要解析注解，**HandlerAdapter**主要目的从**DispatcherServlet**屏蔽这些细节 |
| HandlerExceptionResolver | 异常解析策略，可能映射到它们到handlers，HTML错误页，或者其他的目标。查看Exceptions |
| ViewResolver             | 解析从handler返回的view 基于String的逻辑名称到一个实际的**View**并渲染到Response。查看ViewResolution和View Technonlogies |
| LocaleResolver           | 解析客户端使用的现场以及它们的时区，为了提供国际化的视图。查看Locale |
| ThemeResolver            | 解析你的web应用可以使用的指数提，例如提供个性化的布局。查看Themes |
| MultipartResolver        | 在multipart 解析库的帮助下解析multipart请求解析（例如，浏览器上传文件）。查看Multipart Resolver |
| L                        | 存储和取回”input"和“output”，**FlashMap**可以用于从一个请求传递属性到另外一个请求，通常用于重定向。查看Flash Attributes |



### 1.1.3 Web MVC Config

应用可以声明列在处理请求的特殊bean类型基础设施bean。**DispatcherServlet**在**WebApplicationContext**检测特殊bean。如果没有匹配的bean类，它会使用默认的列在**DispatcherServlet.properties**类型。

在大多数例子里，MVC Config是最好的起点。它用Java或者XM声明需要的beans，并提供了高等级的callbackAPI配置来定制MVC Config。

>Spirng Boot 依赖MVC的java配置来配置SpringMVC，并提供一些其他的额外方便选项



### 1.1.4 Servlet Config

在Servlet3.0的环境中，你可以选择通过编码方式或者web.xml方式来配置Servlet 容器。接下来的例子注册了一个DispatcherServlet：

```java
import org.springframework.web.WebApplicationInitializer;
public class MyWebApplicationInitializer implements WebApplicationInitializer{
	@Override
	public void onStartup(ServletCongtext container){
        XmlWebApplicationContext appContext = new XmlWebApplicationContext();
        appContext.setConfigLocation("/WEB-INF/spring/dispatcher-config.xml");
        
        ServletRegistration.Dynamic registration= container.addServlet("dispatcher",new DispatcherServlet(appContext));
        registration.setLoadOnStartup(1);
        registration.addMapping("/");
    }
}
```

**WebApplicationInitializer**是一个SpringMVC提供的接口保证你的实现被检测到来初始化Servlet3容器。一个**AbstractDispatcherServletInitializer**抽象基础类**WebApplicationInitializer**来使它注册到**DispatcherServlet**通过覆盖servlet方法来映射和**DispatcherServlet**位置配置更加简单。

```java
public class MyWebAppInitializer extends AbstractAnnotationConfigDispatcherServletIntializer{
	@Override
	protected Class<?>[] getRootConfigClasses{
		return null;
	}
	@Override
	protected Class<?>[] getServletConfigClasses{
		return new Class<?> {MyWebConfig.class;}
	}
	@Override
	protected String[] getServletMapping(){
		return new String[]{"/"};
	}
}
```

如果你使用基于XML的配置，你需要直接从**AbstractDispatcherServletInitializer**扩展，正如下面例子所展示的：

```java
public class MyWebInitializer extends AbstractDispatcherServletInitializer{
    @Override
    protected WebApplicationContext createRootApplicationContext(){
        return null;
    }
    @Override
    protected WebApplicationContext createServletApplicationContext(){
        XmlWebApplicationContext cxt = new XmlWebApplicationContext();
        cxt.setConfigLocation("/WEB-INF/spring/dispatcher-config.xml");
        return cxt;
    }
    @Override
    protected String[] getServletMappings(){
        return new String[]{"/"};
    }
}
```



**AbstractDispatcherServletInitializer**可以提供一个便利的添加**Filter**的方式，并且自动将他们映射到**DispatcherServlet**，正如下面例子展示的：

```java
public class MyWebAppInitializer extends AbstractDispatcherServletInitializer{
    //...
    @Override
    protected Fileter[] getServletFilters(){
        return new  Filter[]{
            new HiddenHttpMethodFilter(),new CharacterEncodingFilter();
        }
    }
}
```

每个filter被按照基于具体类型的默认名称，并且自动映射到**DispatcherServlet**。

**AbstractDispatcherServletInitializer**的**isAysncSupported** protected方法提供了**DispatcherServlet**的单个异步支持，并且所有的filter都会映射到这个方法。默认情况下，这个标记位设定为true。

如果你需要进一步定制**DispatcherServlet**，你可以重写**createDispatcherServlet**方法。



### 1.1.5 Processing

**DispatcherServlet**处理请求如下：

* 搜索**WebApplicationContext**并且作为控制器和其他原件可以使用的属性绑定到request中。默认绑定在**DispatcherServlet.WEB_APPLICATION_CONTEXT_ATTRIBUTE**键
* 本地解析器绑定到request中，使得其他原件在处理request时（渲染视图，准备数据，及其他）能够进行地区化解析。如果你不需要地区化解析，你不需要本地化解析
* 主题解析器绑定到request中，使得视图能够决定使用什么主题。如果你不使用主题，你可以忽略它
* 如果你定义了一个multipart file解析器，会检查请求是否请求multipart。如果找到了mulitipart，请求被包装在**MultipartHttpServletRequest**以等待其他元件进行进一步处理。查看Multipart Resover 获取更多信息及multipart 处理
* 查找合适的handler。如果找到了以后handler，与该handler有关的异常链（preprocessors，postprocessors和控制器）会被执行来准备一个模型和渲染。另外，对于注解控制器来说，response可以被渲染（在 **HandlerAdapter**内部）而不是返回一个视图
* 如果返回了model，view被渲染。如果没有返回model（可能因为preprocessor或者postprocessor因为安全原因中断了请求过程），view不会被渲染，因为request已经被处理



在**WebApplicationContext**中声明的**HanderExceptionResolver** 被用于解析在处理请求过程中抛出的异常。这些异常解析器允许定制逻辑来处理异常。查看Exception来获取更多细节。

Spring**DispatcherServlet**也支持ServletAPI提供的返回**last-modification-data**。一个特殊的request决定last modification date的过程非常简单：**DispatcherServlet**查看一个合适的handler映射，并且测试handler是否被发现实现了**LastModified**接口。如果实现了该接口，**LastModified**接口的**long getLastModified(request)**方法的返回值会被返回给客户端。

让你可以定制独立的**DispatcherServlet**实例通过添加Servlet初始化参数（**init-param**元素）到**web.xml**的Servlet声明中。下面的表格支持一下参数：

| Parameter                       | Explanation                                                  |
| ------------------------------- | ------------------------------------------------------------ |
| contextClass                    | 实现**ConfigurableWebApplicationContext**的类，被Servlet实例化和贝蒂配置。默认使用**XmlWebApplicationContext**。 |
| contextConfigLocation           | 传递String给context实例（通过**contextClass**）来指定那里可以找到相关的contexts。这个String潜在的可以是多String（由分号充当分隔符）来指定多上下文。以防多context位置指定的bean重复，最近的位置会被优先使用 |
| namespace                       | **WebApplicationContext**的名称空间。默认为**[servlet-name]-servlet** |
| throwExceptionIfNotHandlerFound | 当没有找到处理request的handler时决定是否抛出**NoHandlerToundException**。这类异常能够被**HandlerExceptionResolver**捕获到（例如，通过使用一个**@ExceptionHandler**控制器方法）和其他异常一样。<br>默认的这个会被设置成**False**，即这种情况下**DispatcherServlet**设置response status为404（NOT_FOUND)而不抛出异常<br>这表示如果默认的servlet handling也被设置，那么没有解析的requests总会被转发给默认的servlet，404错误总不会被抛出 |

### 1.1.6 Interception

当你想要应用所有的功能到特定的requests的时候，所有的**HandlerMapping**实现支持的拦截器非常好用，例如检查一个principal。拦截器必须实现**org.springframework.web.servlet**包**Handlerinterceptor**的三个方法并必须提供所有pre处理和post处理的灵活性：

* preHandle(..):在handler执行前
* postHandle(..):在handler执行后
* afterCompletion(..):在请求完成后

**preHandle(..)**返回一个boolean值。你可以用这个方法跳出或者继续执行链的处理过程。当这个方法返回**true**，执行链继续进行。当返回false，**DispatcherServlet**认为拦截器自己处理了请求（例如，渲染了一个合适的视图）并且不再继续执行其他的拦截器及实际的执行链中的handler。

这意味着**postHandle**对于reponse已经写入并且先于postHandler通过HandlerAdapter提交的**@ResponseBody**和**ResponseEntity**方法没有那么有用。这意味着这是改变response已经太晚了，例如添加一个额外的头。对于这样的场景，你可以实现**ResponseBodyAdvice**和声明一个**Controller Advice** bean或者直接通过**RequestMappingHandlerAdapter**进行配置。



### 1.1.7 Exceptions

如果在请求映射期间发生了一个异常或者从请求handler（例如从**@Controller**)抛出，**DispatcherServlet**代表了一个**HandlerExceptionResolver** beans链来解析异常并提供可选的处理，通常是一个异常Response。

| HandlerExceptionResolver          | Description                                                  |
| --------------------------------- | ------------------------------------------------------------ |
| SimpleMappingExceptionResolver    | 在异常类名和错误视图事件的映射。对于渲染浏览器应用的错误页面非常有用。 |
| DefaultHandlerExceptionResolver   | 解析由SpirngMVC抛出的异常，并且将它们映射到HTTP状态码。查看可以用作替代的**ResponseEntityExceptionHandler**及Rest API 异常 |
| ResponseStatucExceptionResolver   | 解析**@ResponseStatus**的异常并将他们应黑色到状态码基于注解值 |
| ExceptionHandlerExceptionResolver | 解析调用**@Controller**或者**@ControllerAdvice**中的**@ExceptionHandler**方法抛出的异常 |



#### 解析链

你可以构造一个解析链通过在你的Spring配置中声明多个**HandlerExceptionResolver** beans 并设定他们的**order**。order属性越高，异常解析器越靠后调用。

**HandlerExceptionResolver**的协议使它能够返回：

* 一个指向错误视图的**ModelAndView**
* 一个空的**ModelAndView**，如果它的异常已经被解析器处理了
* **null**如果异常仍然没有被解析，提供给后来的解析处理。如果异常直到最后也没有被处理，它允许冒泡到Servlet容器中。

MVC Config自动声明内置解析器为了处理默认的Spring MVC异常。**@ResponseStatus**异常以及支持**@ExceptionHandler**方法。你可以定制这个列表或者替换它。



#### 容器错误页

如果一个异常经过了任何**HandlerExceptionResolver**仍然没有被解析，就会留给传播，或者reponse 状态码被设置成错误状态（4xx,5xx)，Servlet容器能够被渲染成默认的错误页。为了定制容器的错误页面，你可以在**web.xml**声明一个页面映射。例子如下：

```xml
<error-page>
	<location>/error</location>
</error-page>
```

根据前面的例子，当一个异常冒泡或者Response带有状态码，Servlet容器会将其进行ERROR分发到配置的URL上（例如，**/error**）。这种接下来会被**DispatcherServlet**，可能被映射到一个实现了error的视图或者一个JSON response的**@Controller**，正如下面所示：

```java
public class ErrorController{
    @RequestMapping(path="/error")
    public Map<String,Object> handle(HttpServletRequest request){
        Map<String,Object> map = new HashMap<String,Object>();
        map.put("status",request.getAttribute("javax.servlet.error.status_code"));
        map.pus("reason",request.getAttribute("javax.servlet.error.message"));
        return map;
    }
}
```

>servlet API 没有提供Java创建创建页面映射的方式。如果你可以，同时使用**WebApplicationInitializer**与最小化的**web.xml**

### 1.1.8 View Resolution

Spring MVC 定义**ViewResolver**和**View**接口，使你不需要借助特定的视图技术就可以渲染模型到路由器。**ViewResolver**提供一个从视图名到实际视图的映射。**View**负责在移交给特定的视图技术之前定位数据。

下面的表格提供了**ViewResolver**层级结构的更多细节：

| ViewResolver                   | Description                                                  |
| ------------------------------ | ------------------------------------------------------------ |
| AbstractCachingViewResolver    | **AbstarctCachingViewResolver**的子类实例缓存它们解析的视图实例。缓存改善了一定的视图技术的表现。你可以关闭缓存通过设定**cache**为**false**。更重要的是，你需要在运行时刷行一定视图（例如，当一个FreeMarker模板被调整了），你需要使用**removeFromCache(String viewName,Locale loc)**方法。 |
| XmlViewResolver                | **ViewResolver**的实现接受同Spring XML bean factory具有相同DTD的XML配置文件。默认的配置文件是**/WEB-INF/views.xml** |
| ResourceBunleViewResolver      | **ViewResolver**的实现使用**ResourceBundle**中被bundle基本名称指定的的bean定义。对于每一个它支持解析的视图，它使用属性**[viewname].(class)**作为视图类，使用**[viewname].url**作为视图URL。你可以在View Technologies中找到实例。 |
| UrlBaseViewResolver            | **ViewResolver**接口的简单实现直接解析逻辑视图名到URL通过一个清晰的映射定义。如果你的逻辑名以一个直接的方式匹配到视图资源名，不采用随机的映射，这个是很合适的。 |
| InternalResourceViewResolver   | 支持**InternalResourceView**（实际上，Servlets和JSPs）及子类例如**JstlView**和**TilesView**的**UrlBasedViewResolver**的好用的子类。你可以指定视图类通过这个解析器的**setViewClass(..)**的方法。查看**UrlBasedViewResolver**的 Javadoc 来查看细节 |
| FreeMarkerViewResolver         | **UrlBasedViewResolver**支持**FreeMarkerView**的好用子类及他们的定制类。 |
| ContentNegotiatingViewResolver | **ViewResolver**接口的实现，用来解析一个基于request文件的名称或者**Accept**头。查看Content Negotiation |



#### Handling

你可以通过定义多于一个解析器来实现一个解析链，如果必要，可以通过设定**order**来配置顺序。order值越大，解析器在解析链的位置越靠后。

**ViewResolver**协议指定了它可以返回null来表示没有找到对应的视图。然而，在JSPs和**InternalResourceViewResolver**的情况下，唯一找到JSP的方式就是通过**RequestDispatcher**进行一个分发。这样你必须配置**InternalResourceViewResolver**为所有视图解析器的最后一个。

配置视图解析和添加**ViewResolver** beans到你的Spring配置一样简单。MVC Config为View Resolvers和添加无控制逻辑HTML模板渲染的View Controllers提供一个专用的配置API。



#### Redirecting

特别的**redirect:**前缀定义了一个视图名来执行一个重定向。**UrlBasedViewResolver**（及其子类）会将这个识别为一个重定向指令。视图的其余部分就是重定向的URL。

实际效果控制器返回一个**RedirectView**，但是控制现在可以通过逻辑视图名称来操作。一个逻辑视图名（例如，**redirect:/myapp/some/resourece**）重定向相对于当前的Servlet context，当一个名称例如**redirect:https://myhost.com/some/arbitrary/path**重定向到一个绝对URL。

如果一个控制器方法被**@ResponseStatus**所注解，那么注解值会优先于RedirectView设置的Response 状态。



#### Forwarding

你可以使用特殊的**forward:**前缀在视图名称中，它最终会被**UrlBasedViewResolver**（及其子类）所解析。他会创建一个**InternalResourceView**，并调用一个**RequestDispatcher.forward()**。然而，**InternalResourceViewResolver**及**InternalResourceView**(对于JSPs)前缀并不起作用给，但是如果你使用跟其他类型的视图技术并仍然希望被Servlet/JSP引擎强制执行重定向资源，它很有用。这意味着，你可能需要链接多个视图解析器。



#### Content Negotiation

**ContentNegotiatingViewResolver**本身不解析视图，但是代表其他视图解析器并且选择客户端选择的视图。这个表现可以通过**Accept**头或者从查询参数（例如，“/path?format=pdf”）来决定。

**ContentNegotiatingViewResolver**选择一个合适的视图来处理请求通过比较请求的媒体类型（如Content-Type）于支持视图的每个一**ViewResolver**.列表中兼容**Content-Type**的第一个**View**返回客户端表示。如果一个兼容的视图不被**ViewResolver**链支持，指定视图列表的**DefaultView**属性会被查询。后一种选项适合单视图渲染当前资源的合适表示而不是逻辑视图名称。**Accept**头能够包含通配符（例如，**text/***），在这种情况下，View的**Content-Type**是**text/xml**是一个兼容的匹配。

查看MVC Config下的View Resolver获取更多的配置详情。



### 1.1.9 Locale

Spring的大多数体系结构都支持国际化，正如Spring web MVC框架一样。**DispatcherServlet**使你自动通过使用客户端的现场来解析信息。这个通过**LocaleResolver**对象来实现。

当一个请求来时，**DispatcherServlet**查找一个本地化解析器，如果它找到了，它会使用解析器来处理。通过使用**RequestContext.getLocale()**方法，你可以总是获取本地化通过使用本地化解析器。

为了自动本地化解析，你可以将拦截器加到handler 映射（查看Interception获取更多handler映射拦截器的信息）来在特定的环境下改变本地化信息（例如，基于request里的参数）。

本地解析器和拦截器被定义在**org.srpingframework.web.servlet.i18n**包，并且被配置在你的应用context里。下面是spring 所包含的本地化解析器。

* Time Zone
* Header Resolver
* Cookie Resolver
* Session Resolver
* Locale Interceptor

#### Time Zone

为了获得客户端的本地化，很有用的是获取客户端的时区。**LocaleContextResolver**接口获取一个**LocaleResolver**扩展来使解析器提供一个更丰富的能够包含时区信息的**LocaleContext**。

当可用时，用户的**TimeZone**可以通过使用**RequestContext.getTimeZone()**方法来获取。时区信息能够被任何Date/Time**Converter**和**Formatter**对象使用并且被Spring**ConverterService**注册。

#### Header Resolver

本地解析器检查客户端（例如，网页浏览器）发送的请求中的**accept-language**头。通常请求头中包括客户端操作系统的现场信息。这意味着解析器不支持时区信息。

#### Cookie Resolver

本地解析器检查**Cooke**来检查是否存在是否由定义**Locale**或者**TimeZone**。如果这样它会使用指定的信息。通过使用这个本地解析器，你可以定义cookie名及最大有效时间。下面的例子定义了一个**CookieLocaleResolver**:

```xml
<bean id="localeResolver" class="org.springframework.web.servlet.i18n.CookieLocaleResolver">
	<property name="cookieName" value="clientlanguage"/>
    <!--in seconds，如果被设定为-1，cookie不进行持久化（当浏览器关闭时就删除）-->
    <property name="cookieMaxAge" value="100000"/>
</bean>
```

下面的表格描述了属性**CookieLocaleResolver**:

| Property     | Default          | Description                                                  |
| ------------ | ---------------- | ------------------------------------------------------------ |
| cookieName   | classname+LOCALE | cookie名字                                                   |
| cookieMaxAge | Servlet 容器默认 | cookie在客户端的最大存活时间。如果被设置为-1，则cookie不进行持久化，当客户端关闭浏览器时，cookie不再可用。 |
| cookiePath   | /                | 限制cookie在你网站的使用范围。当**cookiePath**被定义时，cookie只在设定的path及path下面的路径有效 |

#### Session Resolver

**SessionLocaleResolver**是你从用户请求相关的Session中获取**Locale**和**TimeZone**。相比**CookieLocaleResolver**，这种方式本地选择Servlet容器的HttpSession中的本地化选择。结果是这些设置只在每个Session内有效，当session结束时，就失去效果。

这意味着这和外部的session管理机制例如Spring Session Project没有直接的关系。**SessionLocaleResolver**聘雇斌且调整对应的**HttpSession**属性根据当前的**HttpServletRequest**。

#### Locale Interceptor

你可以通过添加**LocaleChangeInterceptor**到**HandlerMapping**的定义之一中来改变本地化。它能够通过调用Dispatcher应用上下文的**LocaleResolver**中的**setLocale**方法来检测request中的参数。接下来的例子展示了调用所有的***.view**资源包含一个**siteLanguage**现在能够改变locale参数。例如，一个请求URL，**https:www.sf.net/home.view?siteLanguage=nl**，改变网站语言为荷兰语。下面的例子展示如何拦截这个本地化：

```xml
<bean id="localeChangeInterceptor" class="org.springframework.web.servlet.i18n.LocaleChangeInterceptor">
	<property name="paramName" value="siteLanguage"/>
</bean>

<bean id="localeResolver" class="org.springframework.web.servlet.i18n.CookieLocaleResolver"/>

<bean id="urlMapping" class="org.springframework.web.servlet.handler.SimpleUrlHandlerMapping">
	<property name="interceptors">
    	<list>
        	<ref bean="localeChangeInterceptor"/>
        </list>
    </property>
   	<property name="mappings">
    	<value>/**/*.view=someController</value>
    </property>
</bean>
```

### 1.1.10 Themes

你可以应用Spring Web MVC 框架的主题来设置你应用的所有界面外观，以此加强用户体验。主题是一些列静态资源的集合，典型样式表及图片等影响应用视觉风格的东西。

#### 定义主题

为了在你的应用中使用主题，你必须实现**org.springframework.ui.context.ThemeSource**接口。**WebApplicationContext**扩展**ThemeSource**接口但是代表它的功能的一个专门实现。默认的，代表接口为**org.springframework.ui.context.support.ResourceBundleThemeSource**实现，从根目录的classpath添加属性文件。为了使用一个定制的**ThemeSource**实现，并且配置**ResourceBundleThemeSource**的基本名称前缀，你可以在应用上下文中注册一个带保留名称**themeSource**的bean。web应用会自动检测到这个bean并且使用它。

如果你使用**ResourceBundleThemeSource**，一个主题是被定义在一个简单的属性文件中。属性文件列出了构成主题的资源，如下所示：

```properties
styleSheet=/themes/cool/style.css
background=/themes/cool/img/coolBg.jpg
```

属性的见是从视图中的主题元素的引用名称。对于一个JSP，你可以直接使用**spring:theme**定制标签，类似**spring:message**标签。下面的JSP fragment使用了定义在前面的主题属性来定制界面外观：

```JSP
<%@ taglib prefix="spring" uri="http://www.springframework.org/tags"%>
<html>
    <head>
        <link rel="stylesheet" href="<spring:theme code='styleSheet'/>" type="text/css"/>
    </head>
    <body style="background=<spring:theme code='background'/>">
        ...
    </body>
</html>
```

默认的，**ResourceBundleThemeSource**被用作空的基本名称前缀。结果是，属性文件从classpath的根目录进行加载。因此，你可以将**cool.properties**主题定义文件放在classpath的根目录下（例如，**/WEB-INF/classes**)。**ResourceBundleThemeSource**使用标准的Java资源bundle加载机制，允许主题的完全国际化。例如我们可以有一个**/WEB-INF/classes/cool_nl.properties**，引用荷兰语文本的背景图片。

#### 解析主题

定义主题之后，正如前面部分所描述的，你需要决定使用哪个主题。**DispatcherServlet**查找在一个名叫**themeResolver**来决定使用哪个**ThemeResolver**实现。一个主题解析器工作在和本地化解析器类似的情况下。它根据请求检测使用主题，并且可以改变请求主题。接下来的表格描述了Spring提供的主题解析器：

| Class                | Description                                                  |
| -------------------- | ------------------------------------------------------------ |
| FixedThemeResolver   | 选择一个固定的主题，通过使用**defaultThemeName**属性         |
| SessionThemeResolver | 这个主题在用户的HTTP session中维护。它在每次会话中都需要被设置，并且在两次会话之间不会被持久化 |
| CookieThemeResolver  | 选择的主题会被写入到客户端的cookie                           |

Spring也提供了一个**ThemeChangeInterceptor**允许主题可以根据每个请求的简单参数请求进行改变



### 1.1.11 Multipart Resolver

**org.springframework.web.multipart**包的**MultipartResolver**是解析包含文件上传的multipart request的策略。这里有一个基于Commons FileUpload的实现和另一个基于Servlet3.0的multipart请求解析的实现。

为了使用multipart 处理，你需要在你的**DispatcherServlet** Spring 配置一个名为**multipartResolver**的**MultipartResolver** bean。**DispatcherServlet**检测到它并将它应用到输入请求中。当一个具有content-type为**multipart/form-data**的POST请求被接受时，解析器会解析内容，并且将当前的**HttpServletRequest**包装为**MultipartHttpServletRequest**提供访问方式给可解析部分进行解析并将它们暴露为请求参数。

#### Apache Commons Fileupload

为了使用Apache Commons Fileupload，你需要配置一个名为**multipartResolver**的**CommonsMultipartResolver**。你也需要将**commons-fileupload**作为依赖添加到你的classpath。

Servlet 3.0

Servlet3.0 multipart 解析需要通过Servlet容器设置来启用。因此，你需要：

* Java方式，在Servlet 注册中设置一个**MultipartConfigElement**
* **web.xml**方式，添加一个**<multipart-config>**部分到servlet声明中

下面的例子展示了如何设置一个**MultipartConfigElement**到Servlet registration:

```java
public class AppInitializer extends AbstractAnnotationConfigDispatcherServletInitializer{
    //...
    @Override
    protected void customizeRegistration(ServletRegistration.Dynamic registration){
        //也可选择设置maxFileSize,maxRequestSize,fileDSizeThreshold
        registration.setMultipartConfig(new MultipartConfigElement("/temp"));
    }
}
```

一旦Servlet3.0 配置后，你可以添加一个名为**multipartResolver**的**StandardServletMultipartResolver**类bean。



### 1.1.12 Logging

Spring MVC 中DEBUG-级的日志，被设计为紧凑，最小的并且人类友好的。它集中于那些再三重复的高价值有用信息，而不是那些在仅仅为特定任务排错时候的信息。

TRACE-级日志大多数和DEBUG级遵循同样的原则（例如，不应当成为fire hose）但是能够被用于任何任务的排错。另外的，一些TRACE级别的日志信息能够展示不同于DEBUG级别的细节。

好的日志来自于使用日志的经验。如果你碰见了不能反馈状态信息的，请让我们知道。

#### Sensitive Data

DEBUG和TRACE 日志可能记录敏感的信息。这也是为什么请求参数和请求头默认被遮挡，以及它们的日志必须全部清晰地通过**DispatcherServlet**的**enableLoggingRequestDetails**属性来进行启用。

```java
public class MyInitializer extends AbstractAnnotationConfigDispatcherInitializer{
    @Override
    protected Class<?>[] getRootConfigClasses(){
        return ...;
    }
    
   	@Override
    protected Class<?>[] getServletConfigClasses(){
        return ...;
    }
    
    @Override
    protected String[] getServletMappings(){
        return ...;
    }
    
    @Override
    protected void customizeRegistration(ServletRegistration.Dynamic regitration){
        registration.setInitParameter("enableLoginRequestDetails","true");
    }
}
```



## 1.2 Filters

**spring-web**提供下main这些有用的过滤器：

* Form Data
* Forwarded Headers
* Shallow ETag
* CORS

### 1.2.1 Form Data

浏览器仅仅能够通过HTTP GET或者HTTP POST提交表单数据，但是非浏览器客户端可以使用HTTP PUT.PATCH 以及DELETE。Servlet API 需要**ServletRequest.getParameter*()**方法来提供仅仅对HTTP POST的表单域支持。

**spring-web**模块提供了**FormContentFilter**来拦截携带**application/x-www-form-urlencoded** content type的HTTP PUT，PATCH，和 DELETE请求，从请求体中读取表单数据，并且将**ServletRequest**打包以使得能够从**ServletRequest.getParameter*()**方法族能够获取表单数据。

### 1.2.2 Forwarded Headers

当一个请求遍历各种代理时（比如负载均衡器）host，port以及 scheme 都可能变化，这使得从客户端角度看链接当前点到正确的host，post以及scheme成为一件具有挑战性的事情。

RFC 7239定义了**Forwarded** HTTP 请求头中代理需要提供的关于原有请求的信息。这也有一些其他的非标准清球头，包括**X-Forwarded-Host**，**X-Forwarded-Port**，**X-Forwarded-Proto**，**X-Forwarded-Ssl**和**X-Forwarded-Prefix**。

**ForwardedHeaderFilter**是一个能调整请求的Servlet filter为了 a）基于**Forwarded** 头改变 host，port，和scheme，b）移除这些头为了消除之后的影响。该过滤器依赖包装请求，并且必须它必须排在其他过滤器之前，例如**RequstContextFilter**这种需要处理调整后的而非原始请求的过滤器。

当应用无法得知请求头是否被一个恶意的客户端有计划的添加的，还有一些其他的关于重定向头的安全考虑。这也是为什么一个代理需要配置信任边界，并且移除外来的不受信任的**Forwarded**头 。你也可以配置**ForwardedHeaderFilter**为**removeOnly=true**，这样它只会移除头但是不使用头。

为了支持异步请求和错误分发，这个过滤器必须被映射**DispatcherType.ASYNC**和**DispatcherType.ERROR**。如果使用Spring框架的**AbstractAnnotationConfigDispatcherServletInitializer**（查看 Servlet Config）所有的过滤器自动注册所有的分发类型。然而如果通过**web.xml**或者在Spring Boot中通过**FilterRegistrationBean**中注册，那么需要确保添加**DispatcherType.ASYNC**和**DispatcherType.ERROR**到**DispatcherType.REQUEST**。

### 1.2.3 Shallow ETag

**ShallowETagHeaderFilter**过滤器创建一个”shallow"标签通过缓存到response中的内容并且计算一个MD5码。下一次客户端请求时，它采取相同的处理，但是它也将计算值同请求头中的**If-None-Match**值进行比较，如果相等，返回一个304（NOT_MODIFIED)。

这种策略节约了网络带宽而不是CPU，相比于每个请求都进行完全处理的情况。其他的控制器级别的策略，前面讲过的可以避免计算。查看HTTP Caching。

该过滤器有一个**writeWeakETag**参数配置过滤器鞋weak ETags 如下：**W/"02a2d595e6ed9a0b24f027f2b63b134d6"**（正如[RFC 7232 Section2.3](https://tools.ietf.org/html/rfc7232#section-2.3)中定义的）。

为了支持异步请求，该过滤器必须被映射到**DispatcherType.ASYNC**一边过滤器能够延迟，并且成功地在最后的异步分发中生成ETag。如果使用Spring 框架的**AbstractAnnotationConfigDispatcherServletInitializer**（见Servlet Config)所有的过滤器能够自动注册所有的分发类型。如果通过**web.xml**注册过滤器或者通过Spring Boot的**FilterRegistrationBean**包括**DispatcherType.ASYNC**。

### 1.2.4 CORS

Spring MVC 通过控制器上的注解来提供对CORS细粒度的支持。然而，当使用Spring Security时，我们建议使用内置的**CorsFilter**，并且它需要排在Spring Security过滤器链之前。

## 1.3 Annotated Controllers

Spring MVC提供了基于注解的编程模型，其中**@Controller**和**@RestController**组件使用注解来表达请求映射，请求输入，异常处理及其他。注解控制器具有 灵活的方法签名并且不需要通过扩展基础类或者实现特定的接口。接下来的例子展示了一个通过注解来定义的控制器。

```java
@Controller
public class HelloController{
    @GetMapping("/hello")
    public String handle(Model model){
        model.addAttribute("message","Hello world!");
        return "index";
    }
}
```

在前面的例子里，方法接受了一个**model**并且返回了一个String类型的视图名，但是其他选择也存在，并且会在接下来的章节介绍。

> spring.io的guides和tutorials使用了这部分介绍的基于注解的编程模型

### 1.3.1 Declaration

你可以通过使用在Servlet的**WebApplicationContext**的标准Spring bean来定义控制器。**@Controller**原型使用Spring 对检测classpath路径中的**@Component**类通用支持自动检测并且自动注册将其为bean定义。它表现为一个注解类原型也具有web组件的角色。

为了启动**@Controller** beans的自动检测，你可以添加组件扫描在你的Java配置中，正如下面的例子展现的：

```java
@Configuration
@ComponentScan("org.example.web")
public class WebConfig{
    //...
}
```

下面的例子展现了与前面等效的XML配置：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:p="http://www.springframework.org/schema/p"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">

    <context:component-scan base-package="org.example.web"/>

    <!-- ... -->

</beans>
```

**@RestController**是一个由元注解**@Controller**和**ResponseBody**组成的组合注解，它表示一个控制器其中的每个方法都继承**@ResponseBody**注解类型，因此直接将返回值写入到回复体，而不是进行视图解析和渲染HTML模板。

#### AOP Proxies

在一些情况下，你需要在运行时对你的控制器通过AOP代理进行装饰。一个例子就是你选择直接在控制器上使用**@Transactional**。如果在这种情况下，对于特定的控制器，我们推荐使用基于类的代理。这是控制器的典型默认选择。然而如果一个控制器需要实现一个不属于Spring context callback（例如，**IntializingBean**，***Aware**，及其他）的接口，你需要清晰的配置基于类的代理。例如，对于**\<tx:annotation-driven/>**你需要改成**<tx:annotation-driven proxy-target-class="true"/>**，**@EnableTrasactionManagement**需要改成**@EnableTransactionManagement(proxyTargetClass=true)**。

### 1.3.2Reuqest Mapping
你可以使用**@RequestMapping*8注解来映射请求到控制器方法。它具有多种属性来通过URL，HTTP方法，请求参数，请求头和媒体类型来映射。你可以使用它在类级别来表达共享的映射或者在方法级别来收窄范围到特定的映射点。
如下是根据HTTP方法特定的**@RequestMapping**的快捷方式:
* @GetMapping
* @PostMapping
* @PutMapping
* @DeleteMapping
* @PatchMapping

提供这些快捷方法的原因是，理论上，大多数控制器方法会被映射到一个特定的HTTP方法而不是使用 **@RequestMapping**，默认地，被映射到所有的HTTP方法。于此同时，**@RequestMapping**
还被用于类级别来表达共享的映射。

下面的例子具有类型和方法级别的映射：
```java
@RestController
@RequestMapping("/persons")
class PersonController {

    @GetMapping("/{id}")
    public Person getPerson(@PathVariable Long id) {
        // ...
    }

    @PostMapping
    @ResponseStatus(HttpStatus.CREATED)
    public void add(@RequestBody Person person) {
        // ...
    }
}
```
#### URL patterns
你可以使用使用glob patterns和通配符来映射：
|Pattern|Description|Example|
|-------|-----------|-------|
|?|匹配一个字符|"/pages/t?st.html\n 匹配"/pages/test.html"和"/pages/t3st.html"|
|*|匹配0个或者多个而字符在一个路径段内|"\/resources/\*png"匹配"\/resources/file.png"\n"/projects/\*/versions"匹配"/projects/spring/boot/versions"|

### 1.3.5 DataBinder
@Controller 或者@ControllerAdvice 类能使用@InitBinder来初始化WebDataBinder,他们依次可以：
* 绑定请求参数（如，表单或者请求参数）到模型对象上
* 转换基于String的请求值（例如请求参数，路径变量，请求头，cookies，以及其他参数）到控制器方法参数的目标类型
* 在渲染HTML格式时，格式化模型对象的值为字符串值

@InitBinder方法能够注册控制器特定的java.bean.PropertyEditor或者Spring Converter 和 Formatter 组件。另外，你可以使用MVC
config来注册Converter 和Formatter类型为全局共享的FormmattingConversionService。

@InitBinder 方法支持许多与@RequestMapping相同的参数，除了@ModelAttribute(命令对象)参数。典型地，他们都被声明为一个带有WebDataBinder参数（为了注册）和一个void 返回值。下面列出了一个例子。

```java
@Controller
public class FormController {

    @InitBinder 
    public void initBinder(WebDataBinder binder) {
        SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd");
        dateFormat.setLenient(false);
        binder.registerCustomEditor(Date.class, new CustomDateEditor(dateFormat, false));
    }
    // ...
}

```
可选的，当你需要使用一个基于Formatter setup 通过一个共享的FormatingConversionService，你可以重用相同的方法以及注册控制器特定的Formatter实现，如下例子所示：
```java
@Controller
public class FormController {

    @InitBinder 
    protected void initBinder(WebDataBinder binder) {
        binder.addCustomFormatter(new DateFormatter("yyyy-MM-dd"));
    }

    // ...
}
```
## 1.4 Functional Endpoints



## 1.5 URI Links



## 1.6 Asynchronous Requests





## 1.7 CORS



## 1.8 HTTP Caching



## 1.10 View Technologies



## 1.11 MVC Config

MVC Java配置和MVC XML配置为大多数应用提供默认配置，并且提供配置API来进行定制。

对于更多进一步地配置，并不能从配置API中进行，请查看Advanced Java Config 和 Advanced XML Config。

你没有必要理解MVC 创建的底层bean和MVC 名称空间。如果你需要了解更多，查看Special BeanTypes和 Web MVC Config。

### 1.11.1 Enable MVC Config

在Java配置中，你可以使用**@EnableWebMvc**注解来开启MVC配置，如下所示：

```java
@Configuration
@EnableMvc
public class WebConfig{
    
}
```

在XML配置中，你可以使用**<mvc:annotation-driven>**元素来启用MVC配置，如下所示：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:mvc="http://www.springframework.org/schema/mvc"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/mvc
        https://www.springframework.org/schema/mvc/spring-mvc.xsd">

    <mvc:annotation-driven/>

</beans>
```

前面的的例子注册了大量的Spring MVC 基础设施bean，并且定义依赖在classpath上可用（例如，JSON，XML和其他的有效载荷转换器）

### 1.11.2 MVC Config API

在Java 配置中，你可以实现**WebMvcConfigurer**接口，如下所示：

```java
@Configuration
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer{
    //实现配置方法。。
}
```

在XML配置中，你可以检查属性和**<mvc:annotation-driven/>**的子元素。你可以查看Spring MVC XML schema，或者使用你IDE的补全特性来查看需要使用哪些属性和子元素。

### 1.11.3 Type Conversion

默认的，各种不同数字和日期类型的格式器被安装，为了支持范围内的**@NumberFormat**和**@DateTimeFormat**定制。

为了在Java 配置中注册定制的formatters 和 converters ，示例如下：

```java
@Configuration
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer{
	@Override
	public void addFormatters(FomatterRegistry registry){
		//...
	}
}
```

同样的在XML配置中，

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:mvc="http://www.springframework.org/schema/mvc"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/mvc
        https://www.springframework.org/schema/mvc/spring-mvc.xsd">

    <mvc:annotation-driven conversion-service="conversionService"/>

    <bean id="conversionService"
            class="org.springframework.format.support.FormattingConversionServiceFactoryBean">
        <property name="converters">
            <set>
                <bean class="org.example.MyConverter"/>
            </set>
        </property>
        <property name="formatters">
            <set>
                <bean class="org.example.MyFormatter"/>
                <bean class="org.example.MyAnnotationFormatterFactory"/>
            </set>
        </property>
        <property name="formatterRegistrars">
            <set>
                <bean class="org.example.MyFormatterRegistrar"/>
            </set>
        </property>
    </bean>

</beans>
```

默认的Spring MVC 在解析和格式化Date值的时候考虑request。这些会在“input”表单中使用时表示为String。对于“date”和“time”表单域，浏览器使用一个固定的HTML规格定义的格式。对于这样的例子中的date和time，格式能够被如下定制：

```Java
@Configuration
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer{
    @Override
    public void addFormatters(FormatterRegistry registry){
        DateTimeFormatterRegistrar registrar = new DateTimeFormatterRegistrar();
        registrar.setUserIsoFormat(true);
        registrar.registerFormatters(registry);
    }
}
```

>查看 **FormatterRegistrar** SPI 及**FormattingConversionServiceFactoryBean**以获取更多信息，当你使用FormatterRegistrar 实现时



### 1.11.4 Validation

默认的，如果Bean Validation出现在classpath（例如，Hibernate Validator)，**LocalValidatorFactoryBean**注册为全局Validator为了在控制器方法参数里使用**@Valid**和**Validated**。

Java方式的配置，你可以定义全局Validator实例如下：

```java
@Configuration
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer {

    @Override
    public Validator getValidator() {
        // ...
    }
}
```

下面的例子展示了如何在XML中实现相同的配置

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:mvc="http://www.springframework.org/schema/mvc"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/mvc
        https://www.springframework.org/schema/mvc/spring-mvc.xsd">

    <mvc:annotation-driven validator="globalValidator"/>

</beans>
```

这意味着你也可以本地注册Validator，如下所示：

```java
@Controller
public class MyController {

    @InitBinder
    protected void initBinder(WebDataBinder binder) {
        binder.addValidators(new FooValidator());
    }
}
```

> 如果你注入了**LocalValidatorFactoryBean**在其他地方，创建一个bean并将它标记为@Primary来避免与在MVC配置中声明的bean冲突

### 1.11.5 Interceptors

在Java配置中，你可以注册拦截器来应用到输入请求，如下：

```java
@Configuration
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer {

    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(new LocaleChangeInterceptor());
        registry.addInterceptor(new ThemeChangeInterceptor()).addPathPatterns("/**").excludePathPatterns("/admin/**");
        registry.addInterceptor(new SecurityInterceptor()).addPathPatterns("/secure/*");
    }
}
```

下面的例子展示了如何在XML配置相同的配置：

```xml
<mvc:interceptors>
    <bean class="org.springframework.web.servlet.i18n.LocaleChangeInterceptor"/>
    <mvc:interceptor>
        <mvc:mapping path="/**"/>
        <mvc:exclude-mapping path="/admin/**"/>
        <bean class="org.springframework.web.servlet.theme.ThemeChangeInterceptor"/>
    </mvc:interceptor>
    <mvc:interceptor>
        <mvc:mapping path="/secure/*"/>
        <bean class="org.example.SecurityInterceptor"/>
    </mvc:interceptor>
</mvc:interceptors>
```

### 1.11.6 Content Types

你可以配置Spring MVC 如何决定请求的媒体类型（例如，**Accept**头，URL 路径扩展，查询参数，等等）。

默认的，URL路径扩展是最先检查的,**json**，**xml**，**rss**和**atom**注册为已知的扩展（依赖于 classpath的依赖）。其次检查**Accept**头。

考虑到仅仅对**Accept**头的默认改变，如果你必须使用基于URL的content type解析，考虑使用基于路径扩展的查询参数策略。查看Suffix Match 和 Suffix Match and RFD 获取更多细节。

在Java配置中，你可以定制content type解析如下：

```Java
@Configuration
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer {

    @Override
    public void configureContentNegotiation(ContentNegotiationConfigurer configurer) {
        configurer.mediaType("json", MediaType.APPLICATION_JSON);
        configurer.mediaType("xml", MediaType.APPLICATION_XML);
    }
}
```

XML:

```xml
<mvc:annotation-driven content-negotiation-manager="contentNegotiationManager"/>

<bean id="contentNegotiationManager" class="org.springframework.web.accept.ContentNegotiationManagerFactoryBean">
    <property name="mediaTypes">
        <value>
            json=application/json
            xml=application/xml
        </value>
    </property>
</bean>
```

### 1.11.7 Message Converters

你可以通过覆盖**configureMessageConverters()**来在Java中配置**HttpMessageConverter**（来替代Spring MVC默认创建的converters）或者通过覆盖**extendMessageConverters()**（来定制默认的convertes或者添加额外的converters到默认的）。

下面的例子添加了XML和JSON converters通过一个定制的ObjectMapper，而不是默认的：

```java
@Configuration
@EnableWebMvc
public class WebConfiguration implements WebMvcConfigurer{
    @Override
    public void configurMessageConverters(List<HttpMessageConverter<?>> converters){
        Jackson2ObjectMapperBuilder builder = new Jackson2ObjectMapperBuilder()
            .indentOutput(true)
            .dateFormat(new SimpleDataFormat("yyyy-MM-ddd"))
            .modulesToInstall(new ParameterNamesModule());
        converters.add(new MappingJackson2HttpMessageConverter(builder.build()));
        converters.add(new MappingJackson2XmlHttpMessageConverter(builder.build()));
    }
}
```

在前面的例子里



## 1.12 HTTP/2

Servlet4 容器被要求支持HTTP/2,Spring Framework 5兼容Servlet API4。从编程模型的解读来看，应用并没有什么特别要做的。然而这里有一些其他的与服务器配置有关的需要考虑。想要获取更多的细节，请查看HTTP/2 wiki 页面。

Servlet API暴露了一个与HTTP/2相关的API。你可以使用**javax.servlet.http.PushBuilder**主动地向客户端推送资源，并且它在**@RequestMapping**中被作为方法参数支持。



# 2.REST Clients

这部分描述作为连接REST端点来连接的客户端。

## 2.1 RestTemplate

**RestTemplate**是一个执行HTTP请求的同步客户端。它是由Spring提供的在底层HTTP client库上暴露简单模板方法的API。

> 5.0版本的**RestTemplate**正在维护中，目前没有变化和更新的要求。如果有需求，请考虑使用能够提供更现代的API并且支持同步异步和流式场景的WebClient 。

查看 REST Endpoint 获取更多细节。



## 2.2 WebClient

**WebClient**是一个非阻塞式的，响应式的执行HTTP请求的客户端。它在5.0被引入用来作为RestTemplate的更现代的替代选择，能够提供同步、异步和流式场景的有效支持。

相比于**RestTemplate**,**WebClient**支持下面的功能：

* 非阻塞IO
* 响应式流式背压
* 少量资源下的高并发
* 充分利用Java8的函数式，流畅的API
* 同步和异步
* 服务器的流式上游和下游处理

请查看WebClient 获取更多细节



# 3. Testing

这部分总结了**spring-test**在Spring MVC应用中可以配置的部分。

* Servlet API Mocks:为了对控制器、过滤器和其他web组件进行单元测试的Servlet API 的Mock实现。查看Servlet API mock 对象获取更多细节。
* TestContext Framework:在JUnit和TestNG tests中加载Spring 配置的支持,包括有效的缓存加载所有测试方法的配置和支持通过一个**MockServletContext**来加载一个**WebApplicationContext**。查看TestContext Framework 获取更多细节。
* Spring MVC Test:一个通过**DispatcherServlet**(支持注解)完全使用Spring MVC基础设施而不使用HTTP服务器,用来测试注解控制器的框架，名为**MockMVc**。查看Spring MVC Test 获取更多细节
* Client-side REST: **spring-test**提供一个你可以用作mock服务器来测试客户端代码，实际上内部使用**RestTemplate**的**MockRestServiceServer**。查看Client REST Tests来获取更多细节。
* **WebTestClient**:用来测试WebFlux应用，也可以用来进行端到端完整性测试，测试任何服务器，在一个HTTP连接之上。它是一个非阻塞的响应式的客户端，非常适合测试异步和流式场景。



# 4. WebSockets

这部分参考文档覆盖支持了 Servlet stack，包括原始WebScoket交互的Websocket 信息 ，通过SockJS仿真的Websocket 仿真，以及通过WebSocket之上的子协议STOMP进行的订阅发布信息.

## 4.1 WebScoket 介绍

WebSocket协议，RFC6455，提供一个标准的在客户端和服务器的单个TCP连接上建立全双工的双向的交流频道的方式。它不同于TCP协议和HTTP协议，但是它工作在HTTP协议之上，使用80和443端口，并且允许重用已经存在的防火墙规则。

一个WebSocket 交互以使用HTTP 的**Upgrade**等字段的HTTP请求头来升级，以这种方式来切换到WebSocket协议，下面的例子展示了一个报文：

```yaml
GET /spring-websocket-portfolio/portfolio HTTP/1.1
Host: localhost:8080
Upgrade: websocket 
Connection: Upgrade 
Sec-WebSocket-Key: Uc9l9TMkWGbHFD2qnFHltg==
Sec-WebSocket-Protocol: v10.stomp, v11.stomp
Sec-WebSocket-Version: 13
Origin: http://localhost:8080
```

不同于使用通常的200状态码，一个支持WebSocket的服务器将会返回类似于下面的报文：

```yaml
HTTP/1.1 101 Switching Protocols 
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Accept: 1qVdfYHU9hPOl4JYYNXF623Gzn0=
Sec-WebSocket-Protocol: v10.stomp
```

经过成功的握手后，HTTP协议底层的TCP协议升级请求保持开放来帮助客户端和服务器继续发送和接受消息。

一个完全的WebScokets介绍超出了本文档的范围。查看RFC6455,HTML5的WebSocket章节获取这其他更多的介绍。

如果一个WebSocket服务器运行于一个网页服务器之后，你需要配置它来传递WebSocket升级请求给WebSocket服务器。同样的，如果一个应用运行于云环境，查看相关的云服务商提供的WebSocket支持的章节。

### 4.1.1 HTTP Versus WebSocket

尽管WebSocket设计用来HTTP完善和以HTTP请求开始，弄懂二者的不同架构和应用编程模型非常重要。

在HTTP和REST中，一个应用以许多的URLs模型来描述。为了和这个应用交互，客户端访问者许多URLs，请求回复风格。服务器基于HTTP URL 方法和请求头，路由请求到合适的处理器。

相反的，在WebSockets里，通常只有一个URL来用于初始的连接。最终，所有的应用消息通过一个相同的TCP连接。这点是一个完全不同的异步，事件驱动的消息模型。

WebSocket是一个低等级的传输协议，不同于HTTP，没有规定任何相关的消息相关的语义。这些以为没有方法来路由或者完成一个协议直到客户端和服务器就消息语义达成共识。

WebSocket 客户端和服务器能够协商使用高等级的消息协议（例如，STOMP）,通过基于HTTP握手协议的的Sec-WebScoket-Protocol协议。如果没有这个消息协议，需要提出他们自己的协议。



### 4.1.2  When to Use WebSocket

WebSockets 能够使一个网页动态和可交互。然而在许多例子里，一个Ajax和HTTP流或者长轮询能够提供简单和有效的解决方式。

例如，新闻，邮件，以及社交需求需要动态更新，但是每几分钟就进行更新并不合适。合作，游戏以及金融应用，另一方面则需要更加接近于实时更新。

时钟延迟单独不是决定因素。如果消息的容量相对低（例如，监控网络失败）HTTP 流或者轮询能够提供有效的解决方法。结合低时延，高频率以及高容量等则最适用Websocket。

请记住在因特网，脱离你控制的限制代理可能会阻碍WebSocket 交互，可能是因为他们没有配置来传递**Upgrade**头，或者他们关闭长连接出现了闲置。这意味着内部应用WebSocket的使用最好在防火墙之内，是个更加直接的来作为公共门面应用的决定。



## 4.2 WebSocket API

Spring 框架提供一个 WebSocket API你能够使用客户端和服务端应用来处理WebSocket 消息。

### 4.2.1 WebSocket Handler

创建WebSocket 服务器像实现**WebSocketHandler**一样简单，或者更多的，通过扩展**TextWebSocketHandler**或者**BinaryWebSocketHandler**。下面的例子使用了**TextWebSocketHandler**。

```java
import org.springframework.web.socket.WebSocketHandler;
import org.springframework.web.socket.WebSocketSession;
import org.springframework.web.socket.TextMessage;

public class MyHandler extends TextWebSocketHandler{
    @Override
    public void handleTextMessage(WebSocketSession sesson,TextMessage message){
        //...
    }
}
```

这需要WebSocket java配置或者XML配置支持来讲之前的WebSocket Handler映射到一个特定的URL，如下例所示：

```java
import org.springframework.web.socket.config.annotation.EnableWebSocket;
import org.springframework.web.socket.config.annotation.WebSocketConfigurer;
import org.springframework.web.socket.config.annotation.WebSocketHandlerRegistry;

@Configuration
@EnableWebSocket
public class WebSocketConfig implements WebSocketConfigurer {

    @Override
    public void registerWebSocketHandlers(WebSocketHandlerRegistry registry) {
        registry.addHandler(myHandler(), "/myHandler");
    }

    @Bean
    public WebSocketHandler myHandler() {
        return new MyHandler();
    }

}
```

下面的例子使用了XML配置相同的内容：

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:websocket="http://www.springframework.org/schema/websocket"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/websocket
        https://www.springframework.org/schema/websocket/spring-websocket.xsd">

    <websocket:handlers>
        <websocket:mapping path="/myHandler" handler="myHandler"/>
    </websocket:handlers>

    <bean id="myHandler" class="org.springframework.samples.MyHandler"/>

</beans>
```

上面的例子是在Spring MVC应用中使用，并且需要包含在**Dispatcher**配置中。然而Spring的Websocket不仅仅支持Spring MVC。相对其他HTTP服务环境需要在**WebSocketHttpRequestHandler**的帮助下需要简单的完善一个**WebSocketHandlker。**

当时比较直接和不直接使用**WebSocketHandler**API时，例如通过STOMP消息，应用需要同步发送信息因为底层的WebSocket会话（JSR-356)不支持并发发送。一个选择是使用**ConcurrentWebSocketSessionDecorator**来包装**WebSocketSession**。



### 4.2.2 WebSocket 握手

最简单来定制初始化HTTP Websocket握手请求的是通过**HandshakeInterceptor**，它通过暴露“before”和“after”握手。你可以使用一个interceptor来阻碍握手，来使**WebSocketSession**能够访问许多属性。接下来的例子使用了一个内置的拦截器来传递HTTP session属性到 WebSocket会话：

```java
@Configuration
@EnableWebSocket
public class WebSocketConfig implements WebSocketConfigurer{
    @Override
    public void registerWebSocketHandler(WebSocketHandlerRegistry registry){
        registry.addHandler(new MyHandler(),"/myHandler")
            .addInterceptors(new HttpSessionHandshakeInterceptor());
    }
}
```

下面的XML配置实现了相同的效果：

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:websocket="http://www.springframework.org/schema/websocket"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/websocket
        https://www.springframework.org/schema/websocket/spring-websocket.xsd">

    <websocket:handlers>
        <websocket:mapping path="/myHandler" handler="myHandler"/>
        <websocket:handshake-interceptors>
            <bean class="org.springframework.web.socket.server.support.HttpSessionHandshakeInterceptor"/>
        </websocket:handshake-interceptors>
    </websocket:handlers>

    <bean id="myHandler" class="org.springframework.samples.MyHandler"/>

</beans>
```

一个更加先进的选项是扩展能够执行WebSocket 握手包括验证客户端来源，协商子协议以及其他细节的**DefaultHandshakeHandler**。如果它需要配置一个定制的**RequestUpgradeStrategy**为了适应WebSocket服务引擎和目前没有支持的版本（查看更多相关主题的部署），一个应用需要使用这个选项。java配置和xml名称配置都能够配置定制的**HandshakeHandler**。

> Spring 提供一个你能够用来用额外的行为装饰**WebSocketHandler**的**WebSocketHandlerDecorator**基类。记录日志和异常处理也默认提供和添加，当你使用Websocket java配置和XML名称空间。**ExceptionWebSocketHandlerDecorator**缓存所有的**WebSocketHandler**方法发起的未捕获异常以及关闭WebSocket会话的**1011**状态码意味着的服务器错误。



### 4.2.3 部署Deployment

Spring WebSocket API很容易整合到Spring MVC应用中，**DispatcherServlet**能够服务HTTP WebSocket 握手和其他HTTP 请求。通过调用**WebSocketHttpRequestHandler**能够将其整合到其他的HTTP过程场景。这很方便而且容易理解。然而在JSR-356运行时，需要考虑一些特殊的情况。

Java WebSocket API（JSR-356）提供两个部署机制。第一个涉及启动时Servlet 容器classpath扫描（Servlet 3 特性）。第二个是在Servlet 容器初始化时，需要注册API。两个机制都不能使用单一的“前端控制器”对于所有HTTP过程，包括WebSocket 握手以及其他所有的HTTP请求，例如Spring MVC的**DispatcherServlet**。

这是一个JSR-356中重要的限制那就是Spring Websocket 需要指明服务器特别的**RequestUpgradeStrtegy**实现，尽管JSR-356运行时。这样的策略现在存在于Tomcat，Jetty，GlassFish，WebLogic，WebSphere和 Undertow(还有 WildFly)。

> 一个用来克服前面提到的Java WebSocket API限制的请求已经被创建，并且能够按照eclipse-ee4/websocket-api#211。Tomcat，Undertow，以及WebSphere提供他们自己的API替代选择能够处理这个，包括Jetty。我们希望更多的服务器会实现。

第二个考虑就是支持JSR-356的Servlet容器能能够运行一个**ServletContainerInitializer**（SCI）扫描可能在某些场景下显著的降低应用的启动速度。如果观察到Servlet容器升级支持JSR-356支持版本后出现了显著的影响，那么可以选择禁用web 片段（以及SCI 扫描）通过在web.xml使用**<absolute-ordering/>**元素，如下所示：

```xml
<web-app xmlns="http://java.sun.com/xml/ns/javaee"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="
        http://java.sun.com/xml/ns/javaee
        https://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"
    version="3.0">

    <absolute-ordering/>

</web-app>
```

### 4.2.4 Server Configuration

每个底层的WebSocket引擎都会暴露一些配置属性来控制运行时特征，如消息缓冲的尺寸，空闲时间，以及其他。

对于Tomcat，和GlassFish，你可以添加一个**ServletServerContainerFactoryBean**到你的WebSocket Java配置，如下所示：

```java
@Configuration
@EnableWebSocket
public class WebSocketConfig implements WebSocketConfigurer {

    @Bean
    public ServletServerContainerFactoryBean createWebSocketContainer() {
        ServletServerContainerFactoryBean container = new ServletServerContainerFactoryBean();
        container.setMaxTextMessageBufferSize(8192);
        container.setMaxBinaryMessageBufferSize(8192);
        return container;
    }

}
```

XML的对应设置：

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:websocket="http://www.springframework.org/schema/websocket"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/websocket
        https://www.springframework.org/schema/websocket/spring-websocket.xsd">

    <bean class="org.springframework...ServletServerContainerFactoryBean">
        <property name="maxTextMessageBufferSize" value="8192"/>
        <property name="maxBinaryMessageBufferSize" value="8192"/>
    </bean>

</beans>
```

> 对于客户端 WebSocket 配置，你需要使用**WebSocketContainerFactoryBean**（XML）或者Containerprovider.getWebScoketContainer()(Java Configuration)

对于Jetty，你需要提供一个预先配置的Jetty**WebSocketServerFactory**并将它插入到Spring的**DefaultHandshakeHandler**通过你的WebSocket Java 配置。下面的例子展示了怎么来配置：

```java
@Configuration
@EnableWebSocket
public class WebSocketConfig implements WebSocketConfigurer {

    @Override
    public void registerWebSocketHandlers(WebSocketHandlerRegistry registry) {
        registry.addHandler(echoWebSocketHandler(),
            "/echo").setHandshakeHandler(handshakeHandler());
    }

    @Bean
    public DefaultHandshakeHandler handshakeHandler() {

        WebSocketPolicy policy = new WebSocketPolicy(WebSocketBehavior.SERVER);
        policy.setInputBufferSize(8192);
        policy.setIdleTimeout(600000);

        return new DefaultHandshakeHandler(
                new JettyRequestUpgradeStrategy(new WebSocketServerFactory(policy)));
    }

}	
```

下面的例子是怎么使用xml配置来实现;

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:websocket="http://www.springframework.org/schema/websocket"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/websocket
        https://www.springframework.org/schema/websocket/spring-websocket.xsd">

    <websocket:handlers>
        <websocket:mapping path="/echo" handler="echoHandler"/>
        <websocket:handshake-handler ref="handshakeHandler"/>
    </websocket:handlers>

    <bean id="handshakeHandler" class="org.springframework...DefaultHandshakeHandler">
        <constructor-arg ref="upgradeStrategy"/>
    </bean>

    <bean id="upgradeStrategy" class="org.springframework...JettyRequestUpgradeStrategy">
        <constructor-arg ref="serverFactory"/>
    </bean>

    <bean id="serverFactory" class="org.eclipse.jetty...WebSocketServerFactory">
        <constructor-arg>
            <bean class="org.eclipse.jetty...WebSocketPolicy">
                <constructor-arg value="SERVER"/>
                <property name="inputBufferSize" value="8092"/>
                <property name="idleTimeout" value="600000"/>
            </bean>
        </constructor-arg>
    </bean>

</beans>
```

### 4.2.5 Allowed Origins

正如Spring Framework4.1.5所说，默认的Websocket和SockJs行为能够接受同样origin请求。它能够允许所有或者一个特别的请求源表。这个确认是为了浏览器客户端设计。任何类型的客户端都可以调整origin头部值（查看RFC6454:web源值概念获取更多细节）。

三个可能的行为是：

* 允许唯一的同源请求（默认）：在这种模式下，当SockJS可用时，HTTP框架的回复头中的**X-Frame-Options**被设定为**SAMEORIGIN**，并且JSONP传送被禁用，因为不允许检查请求的来源。结果是，IE6和IE7不支持这种模式
* 允许特定名单的源：每个允许的源必须以**http://**或者**https://**开头。在这种模式下，当SockJS可用时，IFrame transport 不可用。结果是，IE6到9都不支持这种模式
* 允许所有的源：为了使用这种模式，你需要提供*****作为允许的源值，所有的传输都可用。

可以配置WebSocket 和SockJs允许的源，如下所示：

```java
import org.springframework.web.socket.config.annotation.EnableWebSocket;
import org.springframework.web.socket.config.annotation.WebSocketConfigurer;
import org.springframework.web.socket.config.annotation.WebSocketHandlerRegistry;

@Configuration
@EnableWebSocket
public class WebSocketConfig implements WebSocketConfigurer {

    @Override
    public void registerWebSocketHandlers(WebSocketHandlerRegistry registry) {
        registry.addHandler(myHandler(), "/myHandler").setAllowedOrigins("https://mydomain.com");
    }

    @Bean
    public WebSocketHandler myHandler() {
        return new MyHandler();
    }

}
```

对应的XML配置：

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:websocket="http://www.springframework.org/schema/websocket"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/websocket
        https://www.springframework.org/schema/websocket/spring-websocket.xsd">

    <websocket:handlers allowed-origins="https://mydomain.com">
        <websocket:mapping path="/myHandler" handler="myHandler" />
    </websocket:handlers>

    <bean id="myHandler" class="org.springframework.samples.MyHandler"/>

</beans>
```



## 4.3 SockJS Fallback

在公用的因特网上，具有限制的不在你控制范围内的代理可能会阻碍WebSocket交互，不仅因为他们没有配置为传送**Upgrade**头或者因为他们关闭长连接导致其出现空闲。

解决这个问题的方法为Websocket仿真，即，在最初使用WebSocket，然后降级为基于HTTP的技术来模拟WebSocket交互，并且暴露相同的应用API。

在Servlet堆栈中，Spring Framework提供服务（和客户端）支持SockJS协议。

### 4.3.1 Overview

使用SockJS的目的是使应用使用WebsocketAPI但是能够在运行时降级为非Websocket的替代选择，而不需要更改任何代码。

SockJS 组成成分为：

* 以可执行测试形式定义的SockJS协议
* SockJS Javascript 客户端——一个在浏览器使用的客户端
* SockJS服务器实现，包括Spring Framework的**spring-websocket**模块
* SockJS 在**spring-websocket**模块中的Java客户端

SockJS被设计用在浏览器中。它使用多种技术来支持较大范围的浏览器版本。为了查看SockJS支持的类型和浏览器，查看SockJS客户端页面。传输使用了三种类型：Websocket，HTTP 流和HTTP 长轮询。为了对三个库有个大概了解，请查看 blog post。

SockJS以**GET /info**作为开头向服务器发送以获取基本信息。之后，它必须决定使用哪种传输协议。如果可以的话，使用WebSocket，如果不是，在大多数浏览器中最终会使用流式传输。如果还不行，则选择HTTP轮询。

所有的传输请求具有下列这样的URL结构;

```
https://host:port/myApp/myEndpoint/{server-id}/{session-id}/{transport}
```

这里：

* **{server-id}**用于在集群中路由请求，其他场景没有用
* **{session-id}**联系请求属于的SockJS Session
* **{transport}**指明请求的传输类型（例如，**websocket**，**xhr-streaming**，或者其他的）

WebSocket传输只需要一个HTTP请求来做WebSocket 握手。所有信息之后通过socket交换。

HTTP 传输需要更过的请求。Ajax/XHR 流，例如依靠单一的长诗请求来传送服务端到客户端的信息，以及额外的HTTP POST 请求来做客户端到服务端的信息。长轮询比较类似，除了它关闭当前请求，在每一次完成服务端到客户端的传送之后。

SockJS添加最少的信息框架。例如，服务器发送信件**o**（”open“框架）。初始，信息以**a["message1","message2"]**（JSON-编码的数组）来发送，信件**h**（”heartbeat“框架）如果25秒没有信息流发送（默认），信件**c**（”close“框架）来关闭会话。

为了学习更多，在浏览器运行一个例子，并且查看HTTP请求。SockJS客户端允许确定传输表，因此每次查看每次传输的内容是可行的。SockJS也提供debug 标志，在浏览器控制台中打印有用的信息。在服务器端，你可以为**org.springframework.web.socket**启用**TRACE**日志。查看跟多细节，请查看SockJS协议narrated test。

### 4.3.2 Enbaling SockJS

你可以启动SockJS通过如下的Java配置：

```java
@Configuration
@EnableWebSocket
public class WebSocketConfig implements WebSocketConfigurer{
    
    @Override
    public void registerWebSocketHandlers(WebSocketHandlerRegistry registry){
        registry.addHandler(myHandler(),"/myHandler").withSockJS();
    }
    
    @Bean
    public WebSocketHandler myHandler(){
        return new MyHandler();
    }
}
```

下面是相等的xml配置：

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:websocket="http://www.springframework.org/schema/websocket"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/websocket
        https://www.springframework.org/schema/websocket/spring-websocket.xsd">

    <websocket:handlers>
        <websocket:mapping path="/myHandler" handler="myHandler"/>
        <websocket:sockjs/>
    </websocket:handlers>

    <bean id="myHandler" class="org.springframework.samples.MyHandler"/>

</beans>
```

 前面Spring MVC的例子需要被包含在**DispatcherServlet**配置当中。然而，Spring WebSocket和SockJS支持都不依赖于Spring MVC。它需要在**SockJsHttpRequestHandler**的帮助下被相对简单的整合到HTTP服务器环境。

在浏览器端，环境可以使用**sockjs-client**(version1.0.x)。它模仿W3C WebSocket API并与服务器交互已获得最佳的传输选择，来决定最终在浏览器中使用哪个传输协议。查看sockjs-clien以及浏览器支持的传输列表。客户端也提供一些配置，例如配置包含哪些传输协议。

### 4.3.3 IE8 和9

IE8、9浏览器仍在使用中。它们是使用SockJS的主要原因。这部分包括了使用这些浏览器的重要考虑。

SockJS客户端支持了在IE8和9中的Ajax/XHR 流通过使用微软的**XDomainRequest**。这些跨域的工作不支持发送cookies。Cookes通常对Java应用很重要。然而，不管SockJS客户端可以被多种服务器类型使用（不只是java服务器），它需要知道cookes是否重要。如果这样SockJS更适合流式的Ajax/XHR。否则它依赖基于框架的技术。

第一个**/info**的来自SockJS客户端的请求的信息会影响客户端对于传输协议的选择。其中一个细节就是，服务器应用是否依赖于cookies（例如，为了认证或者集群的粘滞会话）。Spring的SockJS支持包括一个属性被叫做**sessionCookieNeeded**。它默认是开启的，因为大多数Java应用需要依赖于**JSESSIONID**的cookie。如果你的应用更不需要它，你可以关闭这个选项，那么SockJS客户端可以选择在IE8和9上使用**xdr-streaming**。

如果你使用基于框架的的传输，请记住浏览器能够被指示禁用框架通过设置HTTP响应头中的**X-Frame-Options**为**DENY**，**SAMEORIGION**或者**ALLOW-FROM<origin>**。这是为了防止点击劫持。

> Spring Security3.2+提供了在每个回复中设置**X-Frame-Options**的能力。默认的，Spring Security Java配置被设定为DENY。在3.2中Spring Security XML名称空间不能默认设置头但是可以手动配置。在后来的版本中，它设定为默认配置。
>
> 查看Spring Securiy文档的默认Security Headers来获取更多配置**X-Frame-Options**的方法，你也可以查看SEC-2501来获取额外背景信息

如果你的应用添加**X-Frame-Options**回复头（如果必要的话）以及依赖于基于框架的传输，你需要设置请求头值为**SAMEORIGIN**或者**ALLOW-FROM<origin>**。Spring SockJS支持需要知道SockJS客户端的位置，因为它从框架进行加载。默认的，框架被设置为下载SockJS客户端从CDN 位置。将应用源配置为同一个URL是一个好主意。

下面是java配置：

```java
@Configuration
@EnableWebSocketMessageBroker
public class WebSocketConfig implements WebSocketMessageBrokerConfigurer {

    @Override
    public void registerStompEndpoints(StompEndpointRegistry registry) {
        registry.addEndpoint("/portfolio").withSockJS()
                .setClientLibraryUrl("http://localhost:8080/myapp/js/sockjs-client.js");
    }

    // ...

}
```

xml名称空间通过**<websocket:sockjs>**元素来进行类似的配置。

> 在初始化开发的过程中，启用Sockjs客户端的**devel**模式能够阻止浏览器缓存SockJS请求（就像在框架中一样），其他情况下则会被缓存。查看SockJS客户端以获取更多细节。

### 4.3.4 心跳

SockJS协议需要服务器发送心跳信息来防止代理认为连接挂掉了。Spring SockJS配置有一个**heartbeatTime**属性，你可以来调整频率。默认的，一个心跳连接每25秒发送一次，当没有其他信息通过该连接发送的时候。25秒的值是根据IETF 文档制定的公共网络应用的标准。

> 当时基于用WebSocket和SockJS的STOMP是，如果STOMP客户端和服务器协商交换的心跳时，SockJS的心跳是禁用的。

Spring SockJS支持你配置**TaskScheduler**来规划心跳任务。任务安排通过默认的基于可用的处理器的默认配置的线程池实现。你可以通过你的设置来思考定制的设置。

### 4.3.5 客户端切断连接

HTTP流和HTTP长轮询SockJS传输需要一个连接比通常的保证开启的更长时间。为了对这部分有个概览，请查看blog post。

在Servlet 容器中，这是通过Servlet3的异步支持来实现从Servlet容器线程退出，从另外的线程处理请求并继续写入回复。

一个特殊的事情是ServletAPI不支持提供退离线的客户端的通知。查看eclipse-ee4j/servlet-api#44。然而，Servlet容器触发一个异常并最终写入到回复中。因为Spring SockJS服务支持服务端发送的心跳连接（默认每25秒），这意味着一个客户端切断连接会在这段时间内被检测到（或者更早，如果信息发送的更加频繁）。

> 结果是，网络IO失败通常因为客户端切断连接，这可能会导致没必要的stack traces充满日志。Spring 进了最大努力来识别这样的代表着客户端切断连接（对于每个服务器来说）的网络失败，并且通过使用专门的日志类**DISCONNECTED_CLIENT__LOG_CATEGORY**（定义在**AbstractedSockJsSession**中）来记录最小的信息。如果你需要查看stack traces，你可以查看**TRACE**类别

### 4.3.6 SockJS和CORS

如果你允许跨域请求（查看Allowed Origins)，SockJS 协议使用CORS来支持XHR流和轮询传输中的跨域。因此CORS头是自动添加的，除非回复中的CORS的存在被检测到。因此，如果一个应用已经配置了提供CORS支持（例如，通过Servlet过滤器），Spring **SockJsService**会跳过这部分。

可以通过设置Spring SockJsService中的e**suppressCors**来关闭额外添加的CORS头。

SockJ需要下面的 这些头和值：

* **Access-Control-Allow-Origin**：从**Origin**请求头的值的初始化
* **Access-Control-Allow-Credentials**：总是被设置为**true**
* **Access-Control-Request-Headers**：从相同的请求头的值初始化
* **Access-Control-Methods**：HTTP支持方法（查看**TransportType**枚举类）
* **Access-Control-Max-Age**：设置为31536000（1年）

对于具体的实现，查看**AbstractSockJsService**中的**addCorsHeaders**以及源码中的**TransportType**枚举类。

可选地，如果CORS配置允许的话，考虑排除SockJS的端点前缀，使用Spring的**SockJSService**来处理。



### 4.3.7 SockJsClient

Spring 提供了一个SockJS java客户端在不使用浏览器的情况下来连接远程SockJS端点。这在两个服务器在公共网络（即网络代理可能会阻碍WebSocket协议）需要进行远端双向交流的需求时非常有用。一个SockJS Java客户端在进行测试时也很有用（例如，来模拟大量的并发用户）。

SockJS Java客户端支持**websocket**，**xhr-streaming**和**xhr-polling**协议。上面的也适用于浏览器的使用。

你可以配置**WebSocketeTransport**通过：

* JSR-356运行时的**StandardWebSocketClient**
* **JettyWebSocketClient**通过使用Jetty 9+ 原生Websocket API
* 任何Spring的**WebSocketClient**实现

一个**XhrTransport**，根据定义，支持**xhr-streaming**和**xhr-polling**，因此，从一个客户端的角度来看，在使用url连接到服务器上外没有任何区别。现在这里有两种实现方式：

* **RestTemplateXhrTransport**使用Spring的**RestTemplate**来做HTTP请求
* **JettyXhrTransport**使用Jetty的**HttpClient**来做HTTP请求

下面的例子展示怎样创建一个SockJS客户端并且连接到一个SockJS端点：

```java
List<Transport> transports = new ArrrayList<>(2);
transports.add(new WebsocketTranport(new StandardWebSocketClient()));
transports.add(new RestTemplateXhrTransport());

SockJsClient sockJsClient = new SockJsClient(transports);
sockJsClient.doHandshake(new MyWebSocketHandler(),"ws://example.com:8080/sockjs");
```

> SockJS使用JSON格式化的数组用作信息。默认的，jackson2被使用，并且需要在classpath中。可选地你需要配置**SockJsMessageCodec**的实现，并且在**SockJsClient**中进行配置

使用**SockJsClient**来模拟大量的并发用户，你需要配置底层的HTTP客户端（用作XHR传输）来允许充足的连接和线程。下面的例子展示怎么使用Jetty：

```java
HttpClient jettyHttpClient = new HttpClient();
jettyHttpClient.setMaxConnectionPerDestination(1000);
jettyHttpClient.setExecutor(new QueuedThreadPool(1000));
```

下面的例子展示了服务端相关的属性（查看javasoc细节）你需要考虑进行调整的。

```java
@Configuration
public class WebSocketConfig extends WebSocketMessageBrokerConfigurationSupport{
    @Override
    public void registerStompEndpoints(StompEndpointRegistry registry){
        registry.addEndpoint("/sockjs").withSockJS()
            .setStreamByteLimit(512*1024)
            .setHttpMessageCacheSize(1000)
            .setDisconnectDelay(30*1000);
    }
}
```

1. 设置**streamBytesLimit**为512KB（默认为128KB）
2. 设置**httpMessageCache**为1000（默认为100）
3. 设置**disconnectDelay**为30秒（默认为5秒）

### 4.4 STOMP

WebSocket定义了两类信息（文本和二进制），但是它们的内容是未定义的。协议定义了一个机制供客户端和服务端协商子协议（即，更高级的信息协议）来在WebSocket之上定义能够发送什么信息，格式，以及其他。子协议的使用是可选的，但是，客户端和服务端必须就此达成协议来决定信息内容。

### 4.4.1 Overview

STOMP（简单文本传输协议）最初是为脚本语言创立来连接商业信息broker。它设计为常用信息模式的最小子集。STOMP能够在双工网络协议如TCP，WebSocket之上使用。尽管STOMP是一个面向文本的协议，信息负载可以是文本或者二进制内容。

STOMP是一个在HTTP之上建立的基于框架的协议。下面展示了STOMP框架的结构：

```
COMMAND
header1:value1
header2:value2

Body^@
```

客户端可使用**SEND**或者**SUBSCRIBE**命令来发送或者订阅信息，并且通过**destination**头来描述信息以及信息的接收者。这就是简单的发布订阅机制你可以用来通过broker发布信息到其他连接的客户端或者发送信息到服务端来请求执行某些操作。

当你使用Spring的STOMP支持，Spring WebSocket应用对于客户端来说即STOMP的broker。信息被路由到**@Controller**信息处理方法或者一个简单的保存多个订阅即发布信息到订阅用户端的内存broker。你可以配置Spring与一个专门的STOMP broker共同工作（例如，RabbitMQ，ActiveMQ， 或者其他）来进行实际的发布或者接受信息。在这种情况下，Spring维护到broker的TCP链接，转送信息到STOMP，并且将信息从他传送给连接的Websocket客户端。即，Springweb应用，能能够依赖统一的基于HTTP安全的，通用的验证，以及熟悉的编程模型来处理信息。

下面的信息展示了客户端订阅接受股票报价，服务器会每个一段时间发送（例如，使用定时任务通过**SimpleMessageTemplate**来发送信息到broker）：

```
SUBSCRIBE
id:sub-1
destination:/topic/price.stock.*

^@
```

下面的例子展示了客户端发送交易请求，服务器能够通过**@MessageMapping**来进行处理：

```
SEND
desination:/queue/trade
content-type:application/json
content-length:44
{"action":"BUY","ticker":"MM","shares",44}^@
```

通过执行，服务器能够发布交易确认信息和细节给客户端。

destination的意义有意的保留为不清晰的在STOMP规格中。它可以是任何字符串，可以完全由STMOP服务器来定义它们所支持的语义和格式。常用的，destination可以被设置成类似路径的字符串如**/topic/..**代表发布订阅模式，和**/queue/**代表着点对点模式信息交换。

STOMP服务器能够使用**MESSAGE**命令来发布命令到所有的订阅者。下面的例子展示了一个服务器发送股票价格信息到一个订阅客户端“

```
MESSAGE
message-id:nxahklf6-1
subscription:sub-1
destination:/topic/price.stock.MMM

{"ticker":"MMM","price":129.45}^@
```

服务器不能够自动推送消息。所有来自服务器的消息都是响应特殊的客户端订阅，并且**subscirption-id**必须对应客户端订阅的**id**头。

前面的概略意在展示STOMP协议的基本概念。我们推荐重新整体阅读一遍STOMP协议描述。

### 4.4.2 优点

使用STOMP作为子协议使得Spring Framework和Spring Security提供更丰富的编程模型，相比原始的WebSockets。这与HTTP和原始TCP之间比较具有相似性，并且使得Spring MVC和其他网络框架具有更丰富的功能。下面是框架的优点：

* 不需要创造一个定制的消息协议和消息格式
* 提供可用的STOMP客户端，包括Spring Framework的Java客户端。
* 你可以（有选择的）使用message broker（比如RabbitMQ，ActiveMQ，及其他）来管理订阅和发布消息
* 应用逻辑可以通过任意数目的**@Controller**实例组织，并且信息对于一个连接可以基于STOMP的destination 头路由到控制器而不是通过单一的**WebSocketHandler**来处理原始的WebSocket信息。
* 你可以使用Spring Security基于STOMP destinations 和 信息类型来加密信息



### 4.4.3 Enable STOMP

WebSocket 之上运行的STOMP在**spring-messaging**和**spring-websocket**模块中提供。一旦你使用了这些依赖，你可以暴露一个STOMP端点，在WebSock和SockJS的回调之上，如下所示：

```java
import org.springframework.web.socket.config.annotation.EnableWebSocketMessageBroker;
import org.springframework.web.socket.config.annotation.StompEndpointRegistry;

@Configure
@EnableWebSocketMessageBroker
public class WebSocketConfig implements WebSocketMessageBrokerConfigurer{
    
    @Override
    public void registerStompEndpoints(StompEndpointRegistry registry){
        registry.addEndpoint("/portfolio").withSockJS();
    }
    
    @Override
    public void configureMessageBroker(MessageBrokerRegistry config){
        config.setApplicationDestinationPrefixes("/app");
        config.enableSimpleBroker("/topic","/queue");
    }
}
```

1. **/portfolio**一个HTTP URL 由端点供给WebSocket(或者SockJS)客户端来做WebSocket握手连接的
2. 带有**/app**的destination头的STOMP信息被路由到**@Controller**的**@MessageMapping**方法中
3. 使用内置的用于订阅和发布的Message broker和路由带有**/topic**或者**/queue**的destination头的信息到当前的broker

下面是同样的XML配置：

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:websocket="http://www.springframework.org/schema/websocket"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/websocket
        https://www.springframework.org/schema/websocket/spring-websocket.xsd">

    <websocket:message-broker application-destination-prefix="/app">
        <websocket:stomp-endpoint path="/portfolio">
            <websocket:sockjs/>
        </websocket:stomp-endpoint>
        <websocket:simple-broker prefix="/topic, /queue"/>
    </websocket:message-broker>

</beans>
```

> 对于内置的简单broker，**/topic**和**/queue**前缀没有什么特殊的意义。他们仅仅是一个协议用来区分订阅/发布 和点对点信息（即，许多订阅者与一个消费者）。当你使用外置的broker，检查STOMP页的broker来查看属于什么类型的STOMP destination，以及它支持什么样的前缀

为了从浏览器连接，对于SockJS，你可以使用**sockjs-client**。对于STOMP，许多应用已经使用了**jmesnil/stomp-websocket**库（即stomp.js)，这个库功能性完好并且已经多年被用作生产，但是并没有继续维护。当前**JSteunou/websocket-client**是维护最积极并且发展较好的库。下面的样例代码基于这个库：

```js
var socket = new SockJS("/spring-websocket-portfolio/portfolio");
var stompClient = webstomp.over(socket);

stompClient.connect({},function(frame){
    
})
```

可选的 ，如果你通过WebSocket(不使用 SockJS)连接，你可以使用以下的代码：

```js
var socket = new WebSocket("/spring-websocket-portfolio/portfolio");
var stompClient = Stomp.over(socket);

stompClient.connect({}, function(frame) {
}
```

这意味着前面的例子中的**stompClient**不需要设置**login**和**passCode**头。就算设置了，他们也会在服务端被忽略（或者，被覆盖）。在认证中查看连接一个broker和认证获取更多信息。

为了更多的示例代码，请查看：

* Using Webscoket to build an interactive web application - 一个开始向导
* Stock Portfolio - 一个简单的应用



### 4.4.4 WebSocket Server

为了配置底层的WebSocket 服务器，可以使用服务器配置而引用。对于Jetty，你需要通过设置在**StompEndpointRegistry**时设置**HandshakeHandler**和**WebSocketPolicy**。

```java
@Configuration
@EnableWebSocketMessageBroker
public class WebSocketConfig implements WebSocketMessageBrokerConfigurer {

    @Override
    public void registerStompEndpoints(StompEndpointRegistry registry) {
        registry.addEndpoint("/portfolio").setHandshakeHandler(handshakeHandler());
    }

    @Bean
    public DefaultHandshakeHandler handshakeHandler() {

        WebSocketPolicy policy = new WebSocketPolicy(WebSocketBehavior.SERVER);
        policy.setInputBufferSize(8192);
        policy.setIdleTimeout(600000);

        return new DefaultHandshakeHandler(
                new JettyRequestUpgradeStrategy(new WebSocketServerFactory(policy)));
    }
}
```

### 4.4.5 Flow of Messages 信息流

一旦STMOP端点暴露出来，Spring 应用对于连接的客户端就成为一个STOMP broker。这部分描述了服务端的的信息流。

spring-message 模块的很多基础支持，源于Spring Integration，后来被分离出来并入Spring Framework为了更广泛的许多Spring项目的使用和应用场景。下面的列表简单的描述了一些信息抽象：

* Message：简单的信息代表，包括信息头和信息负载
* MessageHandler：处理信息的协议
* MessageChannel：发送信息的并解耦生产者和消费者协议
* SubscribableChanel：带有**MessageHandler**订阅者的**MessageChannel**
* ExecutorSubscribabelChannel：用**Excutor**分发信息的**SubscribableChannel**

![](./pic/信息流.jpg)

前面的的图片展示了三种 message channel:

* **clientInboundChannel**：从WebSockets客户端接收的信息
* **clientOutboundChannel**：发送服务器信息到WebSocket客户端
* **brokerChannel**：在服务端内部通过发送信息到message broker

![](./pic/信息流2.jpg)

前面两幅图的主要区别为"broker relay"的使用，它将信息通过TCP发送给外部的STOMP broker，然后通过它将信息发送给它的订阅客户端。

当从WebSocket 连接收到信息后，他们被编码成为STOMP格式，转为Spring **Message**表示，并发给**clientInboundChannel**进行进一步的处理。例如以**/app**作为destination header的STOMP信息被路由到**@MessageMapping**注解的方法，当**/topic**和**/queue**信息被直接路由到message broker。

一个注解**@Controller**处理一个来自客户端的STOMP信息可能通过**brokerChannel**发送信息到message broker，然后broker通过**clientOutChannel**将信息广播到匹配的订阅者。同一个控制器可以对HTTP请求做同样的处理，因此一个客户端可以执行一个HTTP POST，即一个**@PostMapping**方法可以发送信息到messagebroker来广播到订阅客户端。

我们可以将下面作为简单的样例。下面的例子建立了一个服务器：

```java
@Configuration
@EnableWebSocketMessageBroker
public class WebSocketConfig implements WebSocketMessageBrokerConfigurer{
    
    @Override
    public void registerStompEndpoints(StompEndpointRegistry registry){
        registry.addEndpoint("/portfolio");
    }
    
    @Override
    public void configureMessageBroker(MessageBrokerRegistry registry){
        registry.setApplicationDestinationPrefixes("/app");
        registry.enableSimpleBroker("/topic");
    }
	
}

@Controller
public class GreetingController{
    @MessageMapping("/greeting")
    public String handle(String greeting){
        return "["+getTimestampZ()+":"+greeting;
    }
}
```

前面的例子支持了以下的流程：

1. 客户端连接到**http://localhost:8080/portfolio**，一旦一个WebSocket连接建立，STOMP信息就开始在之上运行
2. 客户端发送一个SUBSCRIBE报文到**/topic/greeting**的destination header，一旦接收和解码 ，信息就被发送到**clientInboundChannel**并且之后被路由到存储的客户订阅信息的message broker。
3. 客户端发送一个SEND的报文到**/app/greeing**。**/app**前缀能够帮助路由到注解控制器。在**/app**除去后，接下来的destination**/greeting**部分用作将其映射到**GreetingController**中的**@MessageMapping**方法
4. 从**GreetingController**返回的值被转为在携带内容的Spring **Message**和一个默认的**/topic/greeting**的destination header(通过用"/topic"取代输入中的destination中的”/app")。结果的信息发送到**brokerChannel**并且被message broker 处理。
5. Message broker查找所有匹配的订阅者，并且通过**clientOutboundChannel**将MESSAGE报文发给每个订阅者，信息被变为STOMP格式，并且基于WebSocket connection。

下一节提供更多的关于注解方法的细节，包括参数种类和支持的返回类型。

### 4.4.6 Annotated Controllers

应用可以使用注解**@Controller**类来处理来自客户端的信息。这种类能够声明**@MessageMapping**，**SubscribeMapping**，和**@ExceptionHandler**方法，如下：

* @MessageMapping
* @SubscribeMapping
* @MessageExceptionHandler

#### @MessageMapping

你可以使用@MessageMapping 来注解方法以基于它们的destination来路由信息。这个注解提供在方法级别和类型级别的支持。在类型级别，@MessageMapping被用来表达控制器的所有方法的共有映射。

默认的，映射值遵循Ant风格的路径模式（例如/thing*,/thing\*\*)，包括支持模板变量（例如，/thing/{id}）。这个值可以通过**@DestinationVariable**方法参数来引用。应用也可以切换到点分割的映射，正如在Dot as Separators中解释的。

###### 支持的方法参数

下面的表格描述了方法参数：

| 方法参数                                                     | 描述                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Message                                                      | 为了访问完全的Message信息                                    |
| MessageHeaders                                               | 访问信息内部的头部值                                         |
| MessageHeaderAccessor,<br> SimpMessageHeaderAccessor,<br>StompHeaderAccessor | 访通过类型访问其访问头部                                     |
| @Payload                                                     | 访问信息的Payload部分通过一个配置的**MessageConverter**来转换（例如，从JSON)<br><br>假设没有其他的参数匹配，这个注解的出现不是必须的<br><br>如果你可以用@javax.validation.Valid或者Spring的@Validated注解Payload参数，来使用payload参数有效验证 |
| @Header                                                      | 如果必要的话，通过类型转换使用一个org.springframework.core.convert.converter.Converter，来访问特定的值 |
| @Headers                                                     | 访问信息的所有头参数，参数被描述成**java.util.Map**          |
| @DestinationVariable                                         | 访问信息destination中的模板变量。必要的话，变量被转化为声明的方法参数类型 |
| java.security.Principal                                      | 反映在Websocket 进行HTTP握手时的用户登录                     |



##### Return Values

默认的，@MessageMapping方法的返回值被对应的**MessageConverter**序列化到有效载荷，并且作为Message发送到**brokerChannel**，随后被转发到订阅者。出站信息的destination和入站信息一致但是具有**/topic**前缀。

你可以使用**@SendTo**和**@SendToUser**注解来定制输出信息的destination。**@SendTo**是用来定制目标destination或者指定多个destination。**@SendToUser**是用来将输出信息发送给输入信息的相关用户的，查看User Destination。

你可以在同一个方法上同时使用**@SendTo**和**@SendToUser**，他们也同时支持在类级别上使用，这种情况下，他们对类中的方法就是默认有效的。然而，任何方法级别的**@SendTo**或者**@SendToUser**会覆盖类级别的这样的注解。

信息可以使用异步方式处理，即一个**@MessageMapping**方法可以返回**ListenableFuture**,**CompleteFuture**或者**CompletionStage**。

这意味着**@SendTo**和**@SendToUser**仅仅是等同于使用**SimpMessageTemplate**发送信息的便利用法。如果必要，对于更高级的场景，**@MessageMapping**方法应该直接使用**SimpMessagingTemplate**。这个可以通过返回一个值来替代。查看Sending Messages。



#### @SubscribeMapping

**@SubscribeMapping**类似于**@MessagingMapping**但是仅仅用于订阅信息映射。它支持和**@MessageMapping**相同个的方法参数。然而对于返回值，它会将信息直接（通过clientOutboundChannel，响应订阅）传送给客户端而不是（通过brokerChannel,作为匹配订阅的广播）发送给broker。添加@SendTo和@SendToUser会覆盖这个行为进而发送给broker。

哪个更有用？假设broker映射到**/topic**和**/queue**，同时应用Controller映射到**/app**。在这种设定中，broker存储所有的需要重复广播的**/topic**和**/queue**的订阅，就不需要应用自己来处理。客户端也可以订阅**/app** destination，控制器可以返回给订阅返回一个值响应订阅而不涉及broker存储和使用订阅（有效的一次性的响应请求模式）。这种方式的一个使用场景就是启动时向UI中填入初始数据。

什么时候没有用？不要试图映射broker和控制器到相同的destination，除非你因为某些原因想二者独立的处理信息和订阅。进站message 并行的进行处理。无法保证broker或者controller先处理某个信息。如果目标是存储一个订阅并且准备广播完成后进行通知，客户端需要询问一个收据，如果服务器支持它（简单 broker不支持）。下面的例子，展示了向Java STOMP 客户端添加收据。

```java
@Autowired
private TaskScheduler messageBrokerTaskScheduler;

//初始化
stompClient.setTaskScheduler(this.messageBrokerTaskScheduler);

//订阅
StompHeaders headers = new StompHeaders();
headers.setDestination("/topic/...");
headers.setReceipt("r1");
FrameHandler handler = ...;
stompSession.subscribe(headers,handler).addReceiptTask(()->{
   	//订阅准备 
});
```

服务端的配置就是注册一个**ExecutorChannelInterceptor**到**brokerChannel**，并且实现**afterMessageHandled**方法在信息之后调用，包括订阅，都被处理。



#### @MessageExceptionHandler

应用可以使用**@MessageExceptionHandler**来处理**@MessageMapping**方法抛出的异常。你可以在注解声明异常或者通过方法参数声明你处理的已换成那个。下面的例子展示了通过方法参数来声明处理的异常。

```java
@Controller
public class MyController{
    //...
    
    @MessageExceptionHandler
    public ApplicationError handleEXception(MyException exception){
        //...
        return appError;
    }
}
```

**@MessageExceptionHandler**方法支持灵活的方法签名，并且支持相同个方法参数类型，返回作为**@MessageMapping**的方法值。

典型的，**@MessageExceptionHandler**方法应用在**@Controller**类内部（或者类）。如果你希望这样的方法在更广泛的范围内起作用，你可以在标记**@ControllerAdvice**中声明它们。这点使用上和SpringMVC具有类似的用法。

### 4.4.7 发送信息Sending Messages

如果你希望从应用的任意部分发送信息到连接的客户端？任意应用组件能够发送信息到**brokerChannel**。最简单的方法就是注入**SimpMessagingTemplate**并且用它来发送信息。典型的，你可能根据类型来注入它， 如下例所示：

```java
@Controller
public class GreetingController{
    @Autowired
    public GreetingController(SimpMessagingTemplate template){
    	this.template= template;
    }
    
    @RequestMapping(path="/greetings",method=POST)
    public void greet(String greeting){
        String test = "["+getTimestamp()+"]:"+greeting;
        this.template.convertAndSend("/topic/greetings",text);
    }
}
```

你也可以使用它的名称注入（brokerMessagingTemplate)，如果存在另外的同类bean。

### 4.4.8 Simple Broker

内置的简单信息broker处理来自客户端的订阅，将他们存储在内存，并且发布信息到匹配destination的连接的客户端上。broker支持路径类的destination，包括Ant风格的destination模式订阅。

> 应用也可以使用dot分割的destination。查看Dots as Separators。

如果配置了定时任务，简单broker可以支持STOMP 心跳连接。为了使用这个，你需要声明自己的定时任务，并且使用它。下面的例子展示了如何使用你自己的定时任务：

```java
@Configuration
@EnableWebSocketMessageBroker
public class WebSocketConfig implements WebSocketMessageBrokerConfigurer{
    
    private TaskScheduler messageBrokerTaskScheduler;
    
    @Autowired
    public void setMessageBrokerTaskScheduler(TaskScheduler taskScheduler){
        this.messageBrokerTaskScheduler = taskScheduler;
    }
    
    @Override
    public void configureMessageBroker(MessageBrokerRegistry registry){
        registry.enbaleSimpleBroker("/queue/","/topic/")
            	.setHeartbeatValue(new long[]{10000,20000})
            	.setTaskScheduler(this.messageBrokerTaskScheduler);
    }
}
```

### 4.4.9 External Broker 外部broker

简单broker最开始用起来很好，但是仅仅支持STOMP命令的子集（不支持acks，receipts,和其他特性），依赖于简单信息发送循环，对于集群化不适用。作为替代，你能够升级你的应用为全特征信息broker。

查看STOMP文档来进行你信息Broker的选择（例如，Rabbit MQ，Active MQ，等等）安装broker，并启用STOMP支持。遇事你可以启动STOMP broker转发（而不是简单 broker）在Spring配置中。

下面的例子展示了使用全特性broker的样例配置：

```java
@Configuration
@EnableWebSocketMessageBroker
public class WebSocketConfig implements WebSocketMessageBrokerConfigurer{
    
    @Override
    public void registerStompEndpoints(StompEndpointRegistry registry){
        registry.addEndpoint("/portfolio").withSockJS();
    }
    
    @Override
    public void  configureMessageBroker(MessageBrokerRegistry registry){
        registry.enableStompBrokerRelay("/topic","/queue");
        registry.setApplicationDestinationPrefixes("/app");
    }
}
```

下面的例子展示了相同的xml配置：

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:websocket="http://www.springframework.org/schema/websocket"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/websocket
        https://www.springframework.org/schema/websocket/spring-websocket.xsd">

    <websocket:message-broker application-destination-prefix="/app">
        <websocket:stomp-endpoint path="/portfolio" />
            <websocket:sockjs/>
        </websocket:stomp-endpoint>
        <websocket:stomp-broker-relay prefix="/topic,/queue" />
    </websocket:message-broker>

</beans>
```

STOMP之前的配置是使用Spring**MessageHandler**转发信息给外部的message broker。因此需要建立到broker的TCP连接，发送信息给它，并且接受broker发送的信息给客户端通过他们的WebSocket Session。本质上，它也是一个双向的中继器。

> 添加**io.projectreactor.netty:reactor-netty**和**io.netty:netty-all**依赖到你的项目用于连接管理

### 4.4.10 连接到Broker

一个STOMP broker 终极护卫单一的“系统”TCP 连接到broker。这种用于信息的链接通常由服务端应用发起，而不是接受信息。你可以为连接配置STOMP证书（及，STOMP 报文中的**login**和**passcode**头值）。他们被暴露在XML名称空间和java配置中作为**systemLogin**和**systemPasscode**属性具有默认的**guest**值和**guest**。

STOMP broker也创建到每个连接的WebSocket 客户端的独立的连接你可以配置用于所有TCP连接代表客户端的STOMP证书。这个暴露在XML名称空间和Java配置中作为**clientLogin**和**clientPasscode**属性具有默认的**guest**值和**guest**。

>STOMP broker中继总会在发往代表客户端的broker的每一个**CONNECT**报文中设置**login**和**passcode**。然而WebSocket 客户端不需要设置这些头值。它们会被忽略。正如认证部分解释的，WebSocket 客户端应当使用HTTP认证来保护WebSocket 端点同时建立客户端认证。

STOMP broker 中继同时发送和接受来自broker的心跳维持基于“系统”的TCP连接。你可以配置发送和接受的间隔（默认为10秒）。如果到broker的连接丢失了，broker 中继每五秒重新尝试连接直到成功。

任何Spring bean能够通过实现**ApplicationListener<BrokerAvailablityEvent>**来接受“系统”到broker的连接丢失和建立时的通知。例如，一个广播股票价格的股票价格服务会停止发送信息当没有活动的“系统”连接时。

默认的，STOMP broker 中继总是连接或者在丢失连接后重连接相同的host和端口。如果你希望提供不同的地址在每次连接尝试中，你可以配置一组连接地址的supplier，而不是固定的主机和端口。下面的例子展示了：

```java
@Configuration
@EnableWebSocketMessageBroker
public class WebSocketConfig extends AbstractWebSocketMessageBrokerConfigurer {

    // ...

    @Override
    public void configureMessageBroker(MessageBrokerRegistry registry) {
        registry.enableStompBrokerRelay("/queue/", "/topic/").setTcpClient(createTcpClient());
        registry.setApplicationDestinationPrefixes("/app");
    }

    private ReactorNettyTcpClient<byte[]> createTcpClient() {
        return new ReactorNettyTcpClient<>(
                client -> client.addressSupplier(() -> ... ),
                new StompReactorNettyCodec());
    }
}
```

你可以通过**virtualHost**属性配置STOMP broker 中继。这个值被设置为每个CONNECT报文的**host**头而且非常有用（例如，在云环境中实际host建立TCP连接不同于提供基于云的STOMP 服务的host）。

### 4.4.11 Dots as Sperator使用点作为分隔符

当信息被路由到**@MessageMapping**方法是，他们通过**AntPathMatcher**来进行匹配。默认的，模式会使用斜杠作为分隔符。这里有一个类似于HTTP URLs和 Web 应用的好协议。如果你更习惯信息协议，你可以使用点作为分隔符。

下面的例子展示了如何在Java配置中进行配置：

```java
@Configuration
@EnableWebSocketMessageBroker
public class WebScoketConfig implements WebSocketMesssageBrokerConfigurer{
    //...
    @Override
    public void configureMessageBroker(MessageBrokerRegistry registry){
        registry.setPathMatcher(new AntPathMatcher("."));
        registry.enableStompBrokerRelay("/queue","/topic");
        registry.setApplicationDestinationPrefiexes("/app");
    }
}
```

在XML配置中的同等配置：

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xmlns:websocket="http://www.springframework.org/schema/websocket"
        xsi:schemaLocation="
                http://www.springframework.org/schema/beans
                https://www.springframework.org/schema/beans/spring-beans.xsd
                http://www.springframework.org/schema/websocket
                https://www.springframework.org/schema/websocket/spring-websocket.xsd">

    <websocket:message-broker application-destination-prefix="/app" path-matcher="pathMatcher">
        <websocket:stomp-endpoint path="/stomp"/>
        <websocket:stomp-broker-relay prefix="/topic,/queue" />
    </websocket:message-broker>

    <bean id="pathMatcher" class="org.springframework.util.AntPathMatcher">
        <constructor-arg index="0" value="."/>
    </bean>

</beans>
```

之后，一个控制器能够使用点作为**@MessageMappping**方法中的分隔符，如下所示：

```java
@Controller
@MessageMapping("red")
public class RedController{
    
    @MessageMapping("blue.{green}")
    public void handleGreen(@DestinationVariabel String green){
        //...
    }
}
```

这个客户端能够发送信息到**/app/red.blue.green123**。

在前面的例子里，我们没有改变“broker 中继“的前缀，因为这些完全取决于外部的信息 borker。查看对应的broker的STOMP文档页面来确定它支持的destination头。

### 4.4.12认证Authentication

每个STOMP和WebSocket 信息会话通过HTTP请求开始。需要通过请求来升级到WebSockets(即，WebSocket握手)，或者，防止SockJS退化，一系列SockJS HTTP传输请求。

许多应用已经拥有了认证和授权来保证HTTP请求的安全。典型的，用户通过Spring Security通过使用一些机制例如登录页面，HTTP basic认证，或者其他途径。认证用户的安全上下文存储在HTTP会话里，并且联系它的子请求也在同样的基于cookie的会话里。

因此，对于Websocket握手或者SockJS HTTP 传输请求，典型的，通过**HttpServletRequest#getUserPrincipal()**已经有一个认证用户可用的。Spring自动通过联系具有WebSocket或者SockJS会话的用户，并为之创建会话，接着，所有的STOMP信息通过那个会话基于用户头进行传递。

简单的说，一个典型的web应用在安全方面除了它已经完成的，不需要再做额外的工作。用户在HTTP请求级别进行认证，并通过基于cookie的HTTP会话（之后联系到为用户创建的WebSocket 或者SockJS会话）进行维护的一个安全上下文，最终通过应用的每一个**Message**流会携带一个用户头。

STOMP 协议明确要求在**CONNECT**报文中携带**login**和**passcode**头。这些都是在原始设计中就被要求的并且现在还需要的，例如，基于TCP的STOMP。然而对于基于WebSocket的STOMP协议，默认的，Spring在STOMP协议层次忽略了认证头，假定用户已经在HTTP传输层进行了认证，并预计WebSocket或者SockJS会话包含了认证的用户。

> Spring Security提供了使用**ChannelInterceptor**的WebSocket子协议认证来基于用户头来认证信息。同时Spring Session也提供了 WebSocket integration 来保证 用户HTTP 会话在WebSocket 活动时不会超时。

### 4.4.13 Token 认证

 Spring Security OAuth 提供基于token的安全，包括JSON Web Token(JWT)。你可以使用这个作为web应用的认证机制包括 基于WebSocket 交互的STOMP ，正如前面的部分做描述的一样（通过基于cookie的会话维护身份）。

同时，基于cookie的会话并不总是最合适的（例如，应用不维护服务端会话，或者在移动端，它通常要求使用头来进行认证）。

WebSocket 协议 RFC6455 并不指定任何特定的方法在WebSocket 握手期间，服务器能够用来认证用户。实际上，浏览器客户端只能够使用标准的认证头（即basic HTTP 认证），或者cookies，不能提供定制的头。同样的，SockJS JavaScirpt 客户端没有提供一个发送携带者SockJS传输请求的HTTP头的方法。查看sockjs-client issue196。可替代的，它允许发送查询参数，你可以用他们来携带token，但是它具有自己的缺陷（例如，token可能无意间和URL一起被记录在服务器日志中）。

> 前面的对于基于浏览器的客户端不适用于Spring 基于java的STOMP 客户端，后者同时支持发送WebSocket和SockJS请求。

因此，想要避免使用cookies的应用可能在HTTP协议层次上没有任何好的认证替代方案。除了使用cookies，他们可能更喜欢按照下面两步在STOMP信息协议来使用头部认证：

1. 连接时使用STOMP客户端来传送认证头
2. 使用一个**ChannelInterceptor**来处理认证头

下面的例子使用了服务端配置来注册定制的认证拦截器。这意味着一个拦截器只需要认证和在CONNECT** Message**设置用户头。Spring标记和存储认证用户，并且将它联系到之后相同会话的STOMP信息中。下面的例子展示了如何注册一个定制的认证拦截器：

```java
@Configuration
@EnableWebSocketMessageBroker
public class MyConfig implements WebSocketMessageBrokerConfigurer{
    
    @Override
    public void configureClientInboundChannel(ChannelRegistration registrartion){
        registration.interceptors(new ChannelInterceptor(){
           @Override
            public Message<?> preSend(Message<?> message,MessageChannel channel){
                StompHeaderAccessor accessor = MessageHeaderAccessor.getAccessor(message,StompHeaderAccessor.class);
                if(StompCommand.CONNECT.equals(accessor.getCommand())){
                    Authentication user = ...;//access authentication header(s)
                    accessor.setUser(user);
                }
                return message;
            }
        });
    }
}
```

这意味着，当你使用Spring Security来认证信息时，现在，你需要确定认证的**ChannelInterceptor**配置排在Spring security之前。这最好通过声明定制的拦截器在它自己的标记为**@Order(Ordered.HIGHEST_PRECEDENCE+99)**的**WebSocketMessageBrokerConfigurer**实现中来完成。

### 4.4.14 User Destination 用户目的地

应用可以发送信息到指定的用户，Spring STOMP通过识别**/user/**前缀目的地来支持这个目的。例如，一个客户端可以订阅到**/user/queue/position-updates** destination。这个目的地被**UserDestinationMessageHandler**处理，并转化到到唯一指定的用户会话中（例如**/queue/position-updates-user123**）。这在提供了订阅到一通用名称的同时，保证了订阅到相同destination的用户之间没有冲突并 收到独立唯一的位置更新。

在发送端，信息可以被发送到**/user/{username}/queue/position-updates**，也是通过**UserDestinationMessageHandler**转换到一个或者多个目的地，对应每个用户相关的会话。这使得应用组件发送信息到特定用户只需要知道通用地址和用户名即可。这个也支持注解和信息模板。

一个处理信息的方法能够将信息发送给相关的用户通过**@SendToUser**注解（也支持类级别共享的destination），如下例所示：

```java
@Controller
public class PortfolioController{
    
    @MessageMapping("/trade")
    @SendToUser("/queue/position-updates")
    public TradeResult executeTrade(Trade trade,Principal principal){
        //...
        return tradeResult;
    }
}
```

> 当用户destination含有一个认证用户的，它不被特别需要。WebSocket 会话没有关联到一个验证用户的能够订阅到用户destination。在这种情况下，**@SendToUser**注解表现的行为与**broadcast=false**相同（即，目标只发送给信息被处理的）。

你可以发送信息给user destination 从任何应用组件，通过注入Java配置的或者XML名称空间创建的**SimpMessageTemplate**。（bean 名称是**brokerMessagingTempalte**，如果需要通过**@Qualifier**限定的）下面的例子展示了如何来做：

```java
@Service
public class TradeServiceImpl implements TradeService{
    private final SimpMessageTemplate messagingTemplate;
    
    @Autowired
    public TradeServiceImpl(SimpMessageTemplate messageTemplate){
        this.messateTemplate = messagingTemplate;
    }
    
    //...
    
    public void afterTradeExecuted(Trade trade){
        this.messagingTemplate.convertAndSendToUser(trade.getUserName(),
                                                   "/queue/position-updates",
                                                   trade.getResult());
    }
}
```

> 当你用外部信息 broker来使用user destination时，你需要检查broker文档关于怎样管理不活动的队列，因为当用户会话结束时，所有的唯一的用户队列被移除。例如，RabbitMQ 创建自动删除的队列，当你使用destination如**/exchange/amq.direct/position-updates**。因此在这种情况下，客户端可以订阅到**/user/exchange/amq.direct/position-updates。类似的，ActiveMQ有清楚不活动队列的配置选项。

在一个多应用服务器场景，一个user destination可能没有被解析，因为用户连接到了不同的服务器。在这种场景下，你可以配置一个destination来广播未解析信息使得其他服务器有机会进行解析。这可以通过java配置的**userDestinationBroadcast**属性 **MessageBorkerRegistry**和XML中的**message-broker**和**user-destination-broadcast**属性来完成。

### 4.4.15 信息顺序Order of Message

从broker来的信息被发布到**clientOutboundChannel**，从这里他们被写入WebSocket会话。channel基于**ThreadPoolExecutor**，信息在不同线程被处理，被客户端接受的结果序列不一定匹配准确的发布顺序。

如果发布顺序很重要，可以启用**setPreservePublishOrder**标记，正如下面的例子展示的：

```java
@Configuration
@EnableWebSocketMessageBroker
public class MyConfig implements WebSocketMessageBrokerConfigurer{
    
    @Override
    protected void configureMessageBroker(MessageBrokerRegistry registry){
        //...
        registry.setPreservePublishOrder(true);
    }
}
```

下面的例子展示同等的XML配置：

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:websocket="http://www.springframework.org/schema/websocket"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/websocket
        https://www.springframework.org/schema/websocket/spring-websocket.xsd">

    <websocket:message-broker preserve-publish-order="true">
        <!-- ... -->
    </websocket:message-broker>

</beans>
```

当设置标志位后，具有相同客户端会话的信息同每次一个地被发布到**clientOutboundChannel**，因此发布顺序能够保证。这会带来一个较小的性能开销增加，因此只有在必要的时候才启用。

### 4.4.16 Events 事件

一些**ApplicationContext**事件被发布并且能够被实现了Spring的**ApplicationListener**接口的接收：

* **BrokerAvailabilityEvent**：传达broker是否可用。当启动时简单broker变得立即可用，或者当应用运行时，STOMP broker中继可能失去它到全特征的连接（例如，broker重启）。当borker重启后，broker中继能够拥有重连逻辑和重建系统到broker的连接。结果是，当从连接变为不连接或者从不连接变为连接的状态改变就会应发事件变化。使用**SimpMessagingTemplate**能够订阅事件并且能够在borker不可用时避免发送信息。在任何情况下，它们在发送信息时需要处理**MessageDeliveryException**。
* **SessionConnectEvent**：当收到一个新的STOMP CONNECT报文来传达一个新的客户端会话开始时触发。这个事件包含代表连接的信息，包括session ID，用户信息（如果有），以及任何定制的客户端发送的头。这个对于追踪客户端会话很有用。订阅了此事件的组件可以使用**SimpMessageHeaderAccessor**或者**StompMessageHeaderAccessor**来封装包含的信息。
* **SessionConnectedEvent**：当broker 已经发送了一个STOMP CONNECTED 报文以响应CONNECT报文在一个**SessionConnectEvent**事件之后短暂发布。此时，STOMP 会话被视为完全建立。
* **SessionSubscribeEvent**：当一个新的STOMP SUBSCRIBE 报文接收时发布
* **SessionUnsubscribeEvent**：当一个新的STOMP UNSUBSCRIBE报文接收时发布
* **SessionDisconnectEvent**：当一个STOMP 会话结束时发布。当WebSocket 会话结束时，DISCONNECT可能已经被从客户端发送或者自动生成。在一些情况，这个事件每次会话被处罚不止一次。组件对多次断连接事件的响应是幂等性的。

> 当你使用全特征broker的时候，STOMP broker中继自动重连系统连接如果broker变得暂时不可用。客户端连接通常是不会自动重连的。假设启用了心跳连接，客户端能够察觉broker十秒没有发送回复。客户端需要实现他们自己的重连逻辑。

### 4.4.17 Interception 拦截

事件提供了STOMP连接生命周期中的通知，但是并不是为所有的客户端信息。应用可以注册一个**ChannelInterceptor**来在处理链的任意阶段拦截任何信息。下面的例子展示了如何拦截来自客户端的入站信息：

```java
@Configuration
@EnableWebSocketMessageBroker
public class WebSocketConfig implements WebSocketMessageBrokerConfigurer{
    @Override
    public void configureClientInboundChannel(ChannelRegistration registration){
        registration.interceptors(new MyChannelInterceptor());
    }
}
```

一个定制的**ChannelInterceptor**能够使用**StompHeaderAccessor**或者**SimpMessageHeaderAccessor**来获取关于message的信息，如下所示：

```java
public class MyChannelInterceptor implements ChannelInterceptor{
    @Override
    public Message<?> preSend(Message<?> message,MessageChannel channel){
        StompHeaderAccessor accessor = StompHeaderAccessor.wrap(message);
        StompCommand command = accessor.getStompCommand();
        //...
        return message;
    }
}
```

应用也可以实现**ExecutorChannelIntercepor**，作为携带处理信息在线程中的回调的**ChannelInterceptor**。当每一个发送给频道的每一个信息**ChannelInterceptor**被调用一次，**ExecutorChannelInterceptor**在线程中提供钩子每个订阅到该频道的信息**MessageHandler**。

这意味着，正如前面描述的**SessionDisconnectEvent**，当WebSocket 会话关闭时，一个DISCONNECT信息会从客户端发送或者被自动生成。在一些场景下，一个拦截器可能在每次会话中不止一次拦截信息。组件对于多次断连接事件是幂等性的。

### 4.4.18 STOMP 客户端

Spring提供基于WebSocket客户端的STOMP和基于TCP客户端的STOMP。

为了开始，你可以创建和配置**WebSocketStompClient**，正如下面展示的：

```java
WebSocketClient webSocketClient = new StandardWebSocketClient();
WebSocketStompClient stompClient = new WebSocketStompClient(webSocketClient);
stompClient.setMessageConverter(new StringMessageConverter());
stompClient.setTaskScheduler(taskScheduler); // for heartbeats
```

在前面的李自力，你可以使用**SockJsClient**来替代**StandardWebSocketClient**，因为也是**WebSocketClient**的实现。**SockJsClient**能够使用WebSocket或者基于HTTP的传输层作为回调。查看更多细节，请访问SockJsClient。

接下来，你可以建立连接，并且提供一个STOMP会话的处理器，如下例所示：

```java
String url = "ws://127.0.0.1:8080/endpoint";
StompSessionHandler sessionHandler = new MyStompSessionHandler();
stompClient.connect(url,sessionHandler);
```

当会话可用是，处理器被通知，如下所示：

```java
public class MyStompSessionHandler extends StompSessionHandlerAdapter{
    @Override
    public void afterConnected(StompSession session,StompHeaders connectedHeaders){
        //...
    }
}
```

一旦会话建立，任何有效载荷被发送并使用配置的**MessageConverter**进行序列化，如下所示：

```java
session.send("/topic/something","payload");
```

你也可以订阅到destinations。**subscribe**方法需要一个处理订阅信息的处理器，并返回一个**Subscription**你可以用于取消订阅。对于每个接受的信息，这个handler能够指定需要逆序列化的目标**Object**类型，如下所示：

```java
session.subscribe("/topic/something",new StompFrameHandler(){
   	@Override
    public Type getPayloadType(StompHeaders headers){
        return String.class;
    }
    @Override
    public void handleFrame(StompHeaders headers,Object payload){
        //...
   }
});
```

为了启用STOMP 心跳连接，你需要通过**TaskScheduler**来配置**WebSocketStompClient**，并且可选地配置心跳间隔（10秒写不活动，会导致发送心跳包，10秒读不活动，关闭连接）。

> 当你使用**WebSocketStompClient**做性能测试来模拟从同一个记起来的上千个客户端，考虑关闭心跳连接，哪位每个连接需要按时安排它自己的心跳任务，并且对于大量的运行于相同机器上的客户端没有优化

STOMP 协议也支持receipts，客户端使用RECEIPT报文回复服务器在发送或者订阅过程处理时必须添加**receipt**头。为了支持这种处理，**StompSession**提供**setAutoReceipt(boolean)**方法能够保证后续的每一个发送和订阅事件被添加一个**receipt**头。可选的，你可以手动添加receipt头到**StompHeaders**，发送和订阅都返回**Receiptable**实例，你可以使用它来注册receipt成功或者失败的回调。对于这个特征你需要使用**TaskScheduler**和receipt超时时间（默认15秒）配置client。

**StompSessionHandler**它本身即**StompFrameHandler**，使它处理ERROR报文以及处理处理信息时回调异常**handleException**，以及处理传输级错误包括**ConnectionLostException**的**handelTranportError**。

### 4.4.19 WebSocket Scope 

每个WebSocket会话包含属性映射表。Map被作为入站客户端信息的头被添加，并且可以从控制器方法中访问，如下所示：

```java
@Controller
public class MyController {

    @MessageMapping("/action")
    public void handle(SimpMessageHeaderAccessor headerAccessor) {
        Map<String, Object> attrs = headerAccessor.getSessionAttributes();
        // ...
    }
}
```

你可以声明一个在**websocket**作用域中Spring管理的bean。你可注入WebSocket作用域的bean到控制器，任何channel拦截器注册到**clientInboundChannel**。它们都是典型的单例，并且比任何独立的WebSocket 会话存活时间长。因此，你需要为WebSocket作用域的bean来使用作用域代理模式，如下面所示：

```java
@Component
@Scope(scopeName="webSocket",proxyMode=ScopedProxyMode.TARGET_CLASS)
public class MyBean{
    @PostConstruct
    public void init(){
        //依赖注入后调用
    }
    //...
    @PreDestroy
    public void destroy(){
        //当WebSocket会话结束后调用
    }
}

@Controller
public class MyController{
    private final MyBean myBean;
    
    @Autowired
    public MyController(MyBean myBean){
        this.myBean = myBean;
    }
    
    @MessageMapping("/action")
    public void handle(){
        //从当前WebSocket 会话中使用 this.myBean
    }
}
```

当进入任何定制作用域时，当它第一次被从作用域中访问时，Spring 初始化一个第一次新的**MyBean**实例，并且将实例存储到WebSocket会话属性中。当会话结束后会返回相同的实例。WebSocket作用域的bean会调用所有Spring生命周期的方法，如前面所示。

### 4.4.20 性能

当涉及性能时，没有什么单一特别有效的因素。它受许多因素影响，包含信息规模和容量，应用方法调用是否需要阻塞，以及其他因素（例如网络速度，和其他）。这部分的目标是提供能够提升性能的所有可用配置的概览。

在消息应用中，信息通过频道基于线程池的异步调用传送。配置这样的应用需要掌握channels和下面的信息。推荐回顾Flow of Messages。

比较明显的开始调整的地方就是配置**clientInboundChannel**和**clientOutboundChannel**基于的线程池。默认的，两者都被配置为可用处理器的两倍。

如果注解方法处理信息主要使用CPU，**clientInboundChannel**线程数需要配置接近处理器的数。如果更多是IO操作，并且需要阻塞和等待其他外部系统，线程数目则需要增加。

> **ThreadPoolExecutor**具有三个重要的属性：核心线程数，最大线程数，以及没有可用线程时队列的容量。
>
> 一个通常的争议点是配置核心线程数（例如，10）和最大线程（例如，20）最终使得线程池在10到20线程。实际上如果队列容量使用了默认的Integer.MAX_VALUE，线程池在填满核心线程之后不会再增加，因为所有添加的任务都被放入了队列里。
>
> 查看ThreadPoolExecutor的javadoc来学习这些属性如何启动，并理解各种队列策略

在**clientOutboundChannel**端，所有工作都是发送信息给WebSocket客户端。如果客户端具有比较快的网速，线程数应当设置为接近可用处理器数。如果比较慢或者带宽低，它们需要使用更多的时间来处理信息并且把压力交给了线程池这端。因此，增加线程池的数目是很有必要的。

当**clientInboundChannel**的工作量可能预测时，毕竟，它是基于应用的工作内容进行预测，预测**clientOutboundChannel**的工作量很困难，它基于应用控制之外的因素进行估计。因为这个原因，另外两个关于发送信息的附加属性：**sendTimeLimit**和**sendBufferSizeLimit**。你可以使用这些方法来配置允许多久一次发送以及发送信息到客户端时可以缓存多少数据。

通常的想法是，任意给定时间内，只能使用一个线程来发送给客户端。所有附加的信息被缓存，意味着你可以使用这些来决定发送一条信息的时间和缓存的数据量。查看javadoc和XML模式文档来查看重要的更多的细节。

下面展示了一个可能的配置：

```java
@Configuration
@EnableWebSocketMessageBroker
public class WebSocketConfig implements WebSocketMessageBrokerConfigurer{
    @Override
    public void configureWebSocketTransport(WebSocketTransportRegistration registration){
        registration.setSendTimeLimit(15*1000).setSendBufferSizeLimit(512*1024);
        //...
    }
}
```

下面是XML的同等配置：

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:websocket="http://www.springframework.org/schema/websocket"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/websocket
        https://www.springframework.org/schema/websocket/spring-websocket.xsd">

    <websocket:message-broker>
        <websocket:transport send-timeout="15000" send-buffer-size="524288" />
        <!-- ... -->
    </websocket:message-broker>

</beans>
```

你可以使用Websocket 传输配置之前展示的来配置最大允许输入STOMP信息的规模。理论上，一个WebSocket 信息在规模上不做限制。实际上，WebSocket服务器使用限制，例如Tomcat限制为8K，Jetty为64K。因此STOMP客户端（例如Javascript webstomp-client和其他）将更大的STOMP信息划分为16K的包，并使用多个WebSocket信息来发送，这需要服务端进行缓存和重新装配。

Spring基于WebSocket的STOMP支持解决这个问题，因此应用可以配置STOMP 信息的最大规模，不考虑WebSocket服务端指定的信息规模。记住WebSocket信息规模是自动调整的，如果必要它们最少可以携带16K的WebSocket信息。

下面的例子展示了一个可能的配置：

```java
@Configuration
@EnableWebSocketMessageBroker
public class WebSocketConfig implements WebSocketMessageBrokerConfigurer {

    @Override
    public void configureWebSocketTransport(WebSocketTransportRegistration registration) {
        registration.setMessageSizeLimit(128 * 1024);
    }

    // ...

}
```

同等的xml配置

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:websocket="http://www.springframework.org/schema/websocket"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/websocket
        https://www.springframework.org/schema/websocket/spring-websocket.xsd">

    <websocket:message-broker>
        <websocket:transport message-size="131072" />
        <!-- ... -->
    </websocket:message-broker>

</beans>
```

一个关于改进的重要的点设计到使用多应用实例。现在，你不能使用简单broker。然而，当你使用全特征broker时（比如RabbitMQ)，每个应用连接到实例，从一个应用实例广播的信息可以通过broker被发送到连接到任何实例的WebSocket 客户端。

### 4.4.21 Monitoring 监控

当你使用**@EnableWebSocketMessageBroker**或者**<websocket:message-broker>**时，关键的基础设施组件自动收集用来提供应用状态内部监控的数据和统计。配置也声明了一个收集所有可用消息，并且默认每三十分钟在INFO级别记录日志的**WebSocketMessageBrokerStats**类的bean。这个bean会通过Spring的 MBeanExporter暴露给JMX为了在运行时观察（例如通过jdk的**jconsole**)。下面的列表总结了可用的信息：

#### Client WebSocket Sessions

​	**Current**

显示当前有多少客户端会话，并且有WebSocket、HTTP流和轮询的SockJS会话的进一步会话崩溃统	计。

​	**Total**

显示建立了多少会话的总数

​	**Abnormally Closed**

​		**Connect Failures**

连接建立后因为60秒内没有收到任何信息而关闭的。这通常是因为代理或者网络问题。

​		**Send Limit Exceeded**

会话关闭因为超出了配置的发送时间限制或者发送缓存限制，这通常是因为比较慢的客户端引起		的（查看前一个部分）。

​		**Transport Error**

会话因为传输错误关闭，例如从WebSocket连接或者HTTP请求和回复中读取或者写入失败。

​	**STOMP Frames**

处理的CONNECT,CONNECTED和DISCONNECT报文的总数量，显示多少客户端在STOMP级别上的连接。显示的DISCONNECT统计数目会低于真实数据，因为会话中断关闭或者没有发送DISCONNECT报文。

**STOMP Broker Relay**

​	**TCP Connections**

显示多少代表WebSocket会话的TCP连接建立到broker上。这个值应当等于客户端的WebSocket连接+1个附加的共享用于应用内部信息发送的”系统“连接。

​	**STOMP Frames**

发送到或者接收到的代表客户端的broker的CONNECT,CONNECTED和DISCONNECT报文的总数量。DISCONNECT报文发送给broker不管客户端WebSocket会话是否关闭。因此DISCONNECT报文数目稍低显示了broker主动关闭了连接（可能是因为一些心跳连接包没有按时到达，一个无效的输入报文或者其他）。

**Client Inbound Channel**

**clientInboundChannel**基于的线程池的统计数据提供了对进入系统的信息处理的健康监控。任务排队则显示应用处理信息的速度太慢。如果io任务阻碍了任务（例如，较慢的数据库查询，HTTP请求第三方API，等等），考虑增加线程池规模。

**Client Outbound Channel**

**clientOutboundChannel**基于的线程池的统计数据提供了对广播到客户端信息的健康监控。任务排队显示客户端消费信息的速度太慢。一个解决这个的方法是增加线程池规模来为估计的并发慢客户端提供空间。另一个选择是减少发送时间和发送数据缓存限制（查看前一节）。

**SockJS Task Scheduler**

用于发送心跳包的SockJS 定时任务线程池的统计数据。当在STOMP层级上协商心跳包时，SockJS心跳连接就停止。



### 4.4.22 Testing

当你使用Spring的基于WebSocket 的STOMP测试应用时，有两种主要的方法。第一种是写服务端测试来验证控制器的功能以及他们注解的信息处理方法。第二种是写端到端测试来测试有关的客户端和服务端。

这两种方法并不是完全独立的。相反的，二者都覆盖了全部的测试策略。服务端测试更加集中，并且容易写和维护。端到端完整性测试，更加完整测试更多内容，但是它们更多地涉及写和维护。

服务端测试的简单形式是写控制器的单元测试。然而，这个并不足够有效，因为多数的控制器依赖于它的注解，纯净的单元测试并不能测试到这个。

理想的情况是，测试运行时被调用控制器，更类似于测试使用Spring MVC测试框架测试处理HTTP请求的控制器的方法，即没有运行一个Servlet 容器，但是依赖于框架来调用注解控制器。在SpirngMVC测试中，你有两种可替代的选择，可以使用“基于上下文的”或者“独立的”设置：

* 在Spring TestContext框架的帮助下加载实际的Spring配置，注入**clientInboundChannel**作为测试域，并使用它发送信息。
* 手动设置最小的需要的Spring framework基础设施来调用控制器（例如**SimpAnnotationMethodMessageHandler**)并且直接传递信息给他。

两种场景都在tests for the stock portfolio 样例应用中提到了。

第二种方法即创建端到端的完整测试。对于这种，你需要运行一个嵌入模式的WebSocket 服务器，并且作为WebSocket客户端连接到并发送包含STOMP报文的WebSocket信息。test  for stock portfolio样例应用也提到到这种方法通过使用tomcat 作为嵌入式WebSocket 服务器，并使用简单STOMP客户端连接它来进行测试。

# 5 Other Web Frameworks





