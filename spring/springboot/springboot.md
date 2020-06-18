version2.2.6

# 1 Spring Boot Application

## 1.1 创建你自己的FailureAnalyzer

FailureAnalyzer是一个启动时拦截异常将其转化为可读信息的好方法，包装成FailureAnalysis。Spring Boot体哦那个这样的分析器用以分析上下文相关的异常，JSR-303验证以及其他。你也可以自己创建。

AbstractFailureAnalyzer是一个方便的FailureAnalyzer扩展用以检查特定类型的异常。你可以通过扩展该类来处理对应的异常。如果你不需要处理当前异常，返回null，给其他实现类处理该异常。

FailureAnalyzer 实现必须在META-INF/spring.factories 中进行注册。下面的例子注册了ProjectConstraintViolationFailureAnalyzer

```
org.springframework.boot.diagnostics.FailureAnalyzer=\
com.example.ProjectConstraintViolationFailureAnalyzer
```

> 如果你需要访问**BeanFactory**或者**Environment**，你的**FailureAnalyzer**可以直接实现**BeanFactoryAware**或者**EnvironmentAware**

## 1.2 自动配置的故障排错

The Spring Boot 自动配置尽最大努力“做正确的事情”，但是有时候也会失败，而且很难知道为什么。

在任何SpringBoot **ApplicationContext**中有一个真正有用的**ConditionEvaluationReport**。你可以看见它当你设置logging 输出为 **DEBUG**。如果你使用**spring-boot-actuator**，那里也有一个**conditions** 将报告以JSON格式渲染的endpoint。使用那个endpoint 来排错以及查看哪些特性被Springboot在运行时添加（或者没有添加）。

读源码或者javadoc的时候可能会有很多问题。当阅读源码时，请记住一下经验规则：

* 查看被叫做***AutoConfiguration**的类并阅读它们的源码。特别注意**@Conditional***注解的功能及作用时间。添加**--debug**到命令行或者系统属性**-Ddebug**以在控制台获得所有自动配置决定的日志输出。在一个启动actuator的运行的应用里，查看**condition** endpoint（/actuator/conditions或者JMX）都可以获得同样的信息。
* 查看**@ConfigurationProperties**类（例如 ServerProperties）并阅读所有可用的外部配置选项。**@ConfigurationProperties**注解有一个**name**属性作为外部属性的前缀。例如，ServerProperties 有一个**prefix="server"**,它的配置属性就是对应的server.port，server.address或者其他的。在一个启用actuator的运行的应用里，查看**configprops** endpoint。
* 查看**Binder**中用来精确的从**Environment**中拉去配置值**bind**方法使用，它通常会使用前缀
* 查看那些直接绑定到**Environment**的**@Value**注解
* 查看**@ConditionalOnExpression**切换特征开关以响应SpEL表达式的注解，通常需要从**Environment**取值



## 1.3 启动前自定义Environment或者ApplicationContext

一个**SpringApplication**包含**ApplicationListeners**和**ApplicationContextInitializers**，可以用来对context或者environment进行定制化配置。SpringBoot 从**META-INF/spring,factory**加载这些定制选项以内部使用。这里有一下几种注册额外的定制选项的方法：

* 编程化方法，每个应用，通过在**SpringApplication**启动前调用**addListeners**或者**addInitializers**方法
* 指令化方法，每个应用通过设定**context.initializer.classes**或者**context.listener.classes**属性
* 指令化方法，所有应用通过添加一个**META-INF/spring.factories**并将所有应用打包成为一个jar文件

**SpringApplication**发送一些特殊的**ApplicationEvents**给listeners（其中一些可能比context创建还早）并注册**ApplicationContext**的事件到listeners。查看"Spring Boot features"中的“Application Events and Listeners”以获得完整的列表。



# 4 Spring MVC

SpringBoot 很多starter都包含了SpringMVC。一些startery依赖于SpringMVC而不是直接包含它。这部分回答了一些常见的关于SpringMVC和SpringBoot的问题。

## 4.1 写一个JSON REST Service

任何SpringBoot 应用中的**@RestController**注解的会默认以Jackson2渲染该classpath中的JSON response，如下所示：

```java
@RestController
public class MyController{
	@RequestMapping("/thing")
	public MyThing thing(){
		return new MyThing();
	}
}
```

只要**MyThing**能够被Jackson2序列化（对普通POJO或者Groovy对象），**localhost:8080/thing**默认提供JSON表示。这意味着，在浏览器你有时候会看到XML response，因为浏览器倾向于发送接受XML的请求头。



## 4.2 写一个XML REST Service

如果你在classpath上有Jackson XML 扩展（jackson-dataformat-xml），你可以使用它来渲染XML responses。前一个例子我们使用JSON会有效。为了使用Jackson XML 渲染，添加下面的依赖到你的项目。

```XML
<dependency>
	<groupId>com.fasterxml.jackson.dataformat</groupId>
</dependency>
```

如果Jackson的 XML 扩展不可用但是JAXB 可用给，满足向**Mything**中添加注解**@XmlRootElement**后，XML可以被渲染。如下所示：

```java
@XmlRootElement
public class Mything{
	private String name;
	//... getters and setters			
}
```

JAXB 只在高于 Java8的版本提供。如果你使用最近的java版本，你可以添加下面的依赖到你的项目：

```XML
<dependency>
	<groupId>org.glassfish.jaxb</groupid>
	<artifactId>jaxb-runtime</artifactId>
<dependency>	
```

> 为了使服务器渲染XML,你需要发送一个 **Accept:text/xml**（或者使用一个浏览器）



## 4.3 定制Jackson ObjectMapper

Spring MVC（客户端或者服务端）使用**HttpMessageConverters**在一次HTTP交互中来协商内容转变。如果Jackson在classpath中，你已经获得了自动配置的**Jackson2ObjectMapperBuilder**实例提供的默认的converter(s)。

SpringBoot 也有一些特征来使定制行为变得更加简单。

你可以使用environment配置**ObjectMapper**和**XmlMapper**实例。Jackson提供了一套简单开关特性扩展配置运行过程。Jackson中使用映射到environment中的六个Enum来配置：

| Enum                                                   | Property                                      | Values                                           |
| ------------------------------------------------------ | --------------------------------------------- | ------------------------------------------------ |
| com.fasterxml.jackson.data.bind.DeserializationFeature | spring.jackson.deserialization.<feature_name> | true,false                                       |
| com.fasterxml.jackson.core.jsonGenerator.Feature       | spring.jackson.generator.<feature_name>       | true,false                                       |
| com.fasterxml.jackson.data.bind.MapperFeature          | spring.jackson.mapper.<feature_name>          | true,false                                       |
| com.fasterxml.jackson.core.JsonParser.Feature          | spring.jackson.parser.<feature_name>          | true,false                                       |
| com.fasterxml.jackson.data.bind.SerializationFeature   | spring.jackson.serialization.<feature_name>   | ture,false                                       |
| com.fasterxml.jackson.annotation.JsonInclude.Include   | spring.jackson.default-property-inclusion     | always,non_null,non_absent,non_default,non_empty |

例如，为了整洁输出，设置**spring.jackson.serialization.indent_output=true**。多亏了**relaxed binding**的使用，**indent_output**不需要匹配相应的Enum 的INDENT_OUTPUT常量。

基于环境的配置被用于自动配置的**Jackson2ObjectMapperBuilder** bean 同时应用到任何builder创建的mappers包括自动配置的**ObjectMapper** bean。

context中的**Jackson2ObjectMapperBuilder**可以被一个或者多个**Jackson2ObjectMapperBuilderCustomizer** beans进行配置。这些配置bean可以被排序（Boot自身的配置者被具有order 0），使得新增的配置被应用在Boot的配置之前或者之后。

任何**com.fasterxml.jackson.databind.Module**会被自动配置的**Jackson2ObjectMapperBuilder**自动注册，并被应用到任何它创建的**ObjectMapper**实例。这提供了一个增加配置的全局机制。

如果你希望完全替代默认的**ObjectMapper**，定义一个该类的**@Bean**并且标记为**@Primary**，或者如果你更喜欢基于builderding的方式，定义一个**Jackson2ObjectMapperBuilder @Bean**。不论哪种方式都会禁用所有关于**ObjectMapper**的自动配置。

如果你提供任何类型的**MappingJackson2HttpMessageConverter**的**@Bean**，它们都会取代MVC中的默认配置。同时提供一些实用的**HttpMessageConverters**的bean（如果你使用默认的MVC配置随时都可以访问到）。它有一些有用的方法来访问默认和用户加强的消息转换器。

查看“Customize the @ResponseBody Rendering”部分和**WebMvcAutoConfiguration**源码获取更多详情。



## 4.4 定制@ResponseBody 渲染

Spring 使用**HttpMessageConverters**来渲染**@ResponseBody**（或者从**@RestController**获得的responses）。你可以添加额外的converters通过在SpringBoot context中添加合适类型的Bean。如果你添加的bean正是默认方式会使用的Bean类型（例如JSON转换的**MappingJackson2HttpMessageConverter**），它会代替默认的方式。一些实用的**HttpMessageConverters**的bean（如果你使用默认的MVC配置随时都可以访问到）。它有一些有用的方法来访问默认和用户加强的消息转换器（例如，如果你希望手动注入他们到定制的RestTemplate，它会很有用）。

正如在普通的MVC使用中，任何你提供的**WebMvcConfigurer** beans可以添加converters通过重载**configureMessageConverters**方法。然而不同于普通的MVC，你可以提供仅仅提供你需要的新增converters（因为Spring Boot使用相同的的机制来添加它的默认）。如果你选择选择不使用Spring 默认的MVC配置通过提供你的**@EnableWebMvc**配置，你可以完全控制手动配置所有配置通过使用**WebMvcConfigurationSupport**的**getMessageConverters**。

查看**WebMvcAutoConfiguration**源码获得更多详情。



## 4.5 处理Multipart File 上传

Spring Boot 使用 Servelet3 **javax.servlet.http.Part** API以支持文件上传。默认的，Spring Boot 配置SpringMVC支持最大1MB的单文件上传及最大10MB的单请求文件数据。你可以重写这些暴露在**MultipartProperties**类中的值，location是指中间数据的存储位置（例如，**/tmp**目录），threshold past 是数据刷新到硬盘的。例如，如果你希望上传文件没有限制，你可以将**spring.servlet.multipart.max-file-size**属性设置为-1。

当你想要在SpringMVC 控制器的handler方法中接受multipart 编码的文件数据作为**@RequestParam**注解的**MultipartFile**参数时，multipart 支持非常御用。

查看**MultipartAutoConfiguration**源文件获得更多详情。

>容器内置的multipart 上传比引入的外部依赖例如ApacheComons File Upload 上传更加推荐



## 4.6 开关Spring MVC DispatcherServlet

默认的所有内容从你的应用的root（/）进行提供。如果你需要映射到一个不同的路径，你可以如下配置：

```properties
spring.mvc.servlet.path=/acme		
```

如果你有其他的servlets你可以声明**Servlet**类型的**@Bean**或者为每个Servlet**ServletRegistrationBean**，Spring Boot会透明的将他们注册到容器。因为servlets使用这种方式注册，它们可以不通过调用它被映射到DispatcherServlet的sub-context。

配置**DispatcherSerlvet**不太常用，如果你真的需要使用，你需要提供一个**DispatcherServletPath**类型的**@Bean**来提供你定制的**DispatherServlet**的路径。



## 4.7 开关默认MVC配置

最简单的完全控制MVC配置的方式是提供你自己的**@Configuration**通过**@EnableWebMvc**注解。如果这么做，你需要自行配置所有MVC配置。



## 4.8 定制 ViewResolvers

**ViewResolver**是SpringMVC的核心组件之一，将v**@Controller**中的视图名转换成实际的**View**实现。**ViewResolvers**通常用在UI应用中，而不是REST风格的服务（视图不用来渲染**@ResponseBody**）。Spring具有很多**ViewResolver**实现，本身不规定你需要使用哪种。Spring Boot 为你安装一两个，取决于它在你的classpath和应用context，依次尝试每一个知道它获得结果。如果你添加了自己定义的，你需要知道你的resolver添加的位置和次序。

**WebMvcAutoConfiguration**添加下面的**ViewResolvers**到你的上下文：

* **InternalResourceViewResolver**名为‘DefaultViewResolver’。这个定位了使用**DefaultServlet**（包括了静态资源和JSP页面，如果你选择这个）时的能够被渲染的物理资源。它应用一个前缀和一个后缀到view名称并在servlet context（默认为空但是可以通过**spring.mvc.view.prefix**和**spring.mvc.view.suffix**进行额外配置）路径中查找物理资源。你可以通过提供一个同类的bean来覆盖它。
* **BeanNameViewResolver**，名为"beanNameViewResolver"。这是一个获取**View**同名beans的ViewResolver链中非常有用的成员。它需要被覆盖或者替代。
* **ContentNegotiatingViewResolver **名为“viewResolver”，只有在实际的**view**类bean出现时才会被添加。这是一个‘主要的’解析器，代表所有其他的解析器，并试图匹配客户端发送的HTTP请求头中的‘Accept’字段。这里是一个有用的你可能可以学到关于**ContentNegotiatingViewResolver**更多的[博客](https://spring.io/blog/2013/06/03/content-negotiation-using-views)，或者你可以阅读源码来获取跟多详情。你可以关闭自动配置的**ContentNegotiatingViewResolver**通过定义一个名为‘viewResolver'的bean
* 如果你使用Thymeleaf，你有一个**ThymeleafViewResolver**名为‘thymeleafViewResolver'。它在资源里寻找匹配前后缀的view名。前缀属性名为**spring.thymeleaf.prefix**，后缀名为**spring.thymeleaf.suffix**。前缀与后缀值分别默认为’classpath:/templates/'和‘.html'。你可以提供一个同名bean来覆盖**ThymeleafResolver**。
* 如果你使用FreeMarker，你有一个名为'freeMarkerViewResolver'的**FreeMarkerViewResolver**.它在加载路径（通过**spring.freemarker.templateLoaderPath**来配置，默认为’classpath:/templates/‘）中查找匹配前后缀的资源。前缀通过**spring.freemarker.prefix**来配置，后缀通过**spring.freemarker.suffix**来配置。前后缀的默认值分别为空和’.ftlh'。你可以通过提供同名bean来覆盖**FreeMarkerViewResolver**。
* 如果你使用GroovyTemplate（如果**groovy-templates**在你的路径上），你会用到一个**GroovyMarkupViewResolver**名为‘groovyMarkupViewResolver'。它在加载路径查找匹配前后缀的资源（分别通过**spring.groovy.template.prefix**和**spring.groovy.template.suffix**来配置）。前后缀的默认值分别为’classpath:/tempaltes/'和'.tpl'。你可以通过提供同名bean来覆盖**GroovyMarkupViewResovler**。
* 如果你使用Mustache,你会用到名为‘MustacheViewResolver’的**MustacheViewResolver**。它寻找匹配前后缀的资源。前缀为**spring.mustache.prefix**，后缀为**spring.mustache.suffix**。默认值分别为‘classpath:/templates/’和‘.mustache’。你可以通过提供同名bean来覆盖**MustacheViewResolver**。

为了获得更多细节，你可以看下面章节：

* WebMvcAutoConfiguration
* ThymeleafAutoConfiguration
* FreeMarkerAutoConfiguration
* GroovyTemplateAutoConfiguration

’