Core 核心技术
> Version 5.2.8

这部分参考文献覆盖所有的对spring framework是不可或缺的技术。
在这其中最重要的就是spring framework的控制反转容器。一个针对spring framework ioc容器的完全的补充被详尽的Spring AOP 技术覆盖。Spring framework具有它自己的AOP framework，概念上很容易理解，并且成功的定位了java企业编程中80%的AOP需求的甜区。
Spring 整合AspectJ(目前最丰富的——在特征术语上——确定的java企业开发的最成熟的AOP实现)也被提供。

#1.The IoC Container
这张覆盖了Spring 的控制反转容器

##1.1 介绍Spring IoC容器和Beans
这张介绍了Spring framework 的IoC实现的原则。IoC也被叫做依赖注入。它是一个根据对象定义它们的以来（即，其他它们一起工作的对象）只通过构造器参数，工厂方法参数，或者实例中的属性，当它创建或者从工厂方法中返回后。容器之后注入这些依赖到它创建的bean中。这个过程从根本上说是bean反转（控制反转，因为名称）它自己控制了初始化或定位了他自己的依赖通过直接类的构造或者一个像Service Locator 模式的机制。
**org.springframework.beans**和**org.springframework.context**包是SpringFramework IoC 容器的基础。**BeanFactory**接口提供了一个先进的配置机制能够管理任何类型的对象。**ApplicationContext**是**BeanFactory**的子接口，它添加了：
* 更容易的Spring AOP特征
* 信息源处理（为了国际化应用）
* 事件发布
* 应用层特定的上下文，例如为了网页应用**WebApplicationContext**

简单来说，**BeanFactory**提供配置框架和基本功能，**ApplicationContext**添加了更多企业适用的功能。**ApplicationContext**是**BeanFactory**的完全子集，专门用在这账作为Spring IoC 容器的描述。对于更多使用**BeanFactory**而不是**ApplicationContext**的信息，请查看The BeanFactory。

在Spring 中，组成你应用的骨干的对象，并且被Spring IoC容器管理的叫做beans。一个Bean是一个被Spring IoC初始化，组装和管理的对象。Beans，和它们的依赖，通过使用容器中的配置元数据来反映。

## 1.2 Container Overview
**org.springframework.context.ApplicationContext**接口代表SpringIoC容器，它负责初始话，配置以及装配beans。容器根据它的指示来初始化、配置和装配通过读取配置元数据。配置元数据在XML，Java注解或者Java code的方式呈现。它使你表达组成你应用的对象，以及这些对象的相互依存关系。
Spring也提供一些**ApplicationContext**接口的实现类。在独立的应用中，常见的是创建一个**ClassPathXmlApplicationContext**或者**FileSystemXmlApplicationContext**。当XML作为传统的定义配置元数据的方式，你可以使用java注解或者代码作为元数据格式配置容器通过提供少量的XML配置来声明支持额外的元数据形式。
在大多数应用场景中，实例化一个或更多的Spring IoC容器并不需要清晰的用户代码。例如，在网页应用场景中，一个简单的8行的样板web描述XML在**web.xml**文件中一般就足够（see Convenient ApplicationContext Instantiation for Web Applications）。如果你使用Spring Tools for Eclipse（一个Eclipse驱动的开发环境），你可以简单的创建这个模板配置通过几次鼠标点击或者键盘敲击。
下面的图形展示了高层次视角的Spring是如何工作的。你的应用类通过结合配置元数据，在**ApplicationContext**创建和初始化之后，你就拥有一个完全配置和可执行的系统或者应用。
![](./pic/ioc容器.jpg)

### 1.2.1 配置元数据
正如前面的图展示的，Spring IoC 容器消耗某种形式的配置元数据。这个元数据代表着，作为应用开发者的你，如何来告诉Spring 容器来实例化，配置和组装对象在你的应用中。
配置元数据传统的以简单易懂的XML格式提供，这将作为这章大多数使用的方法来传递Spring IoC容器的关键概念和特征。
> 基于XML的元数据并不是唯一允许的配置元数据形式。Spring IoC 容器它本身完全和配置实际的写入格式隔离开来。现在，许多开发者选择基于Java配置Spring 应用。

对于在Spring容器中使用其他形式的元数据的信息，查看：
* Annotation-based configuration:Spring 2.5 引入的支持基于注解的配置元数据
* java-based configuration:Spring3.0开始支持，许多javaConfig提供的特征成为了core Spring Framework的部分。这样，你可以通过使用Java而不是xml文件来定义外部bean到你的应用。为了使用这些新特性，查看 **@Configuration**，**@Bean**，**@Import**, **@DependOn**注解。
spring 配置由至少一个通常多于一个的有容器进行管理的bean定义组成。基于XML配置元数据在顶层的 **\<beans/\>**下以 **\<bean/>**的形式进行配置。Java配置通常使用在 **@Configuration**下的 **@Bean**注解。
这些bean定义和组成你应用的实际对象是一致的。一般的，你定义服务层对象，数据访问对象，表示层对象例如Struts**Action**实例，基础设施对象例如Hibernate **SessionFactories**，JMS**Queues** ，等等。一般的，不在容器中配置细粒度的领域对象，因为这通常是DAOs的职责和创建和加载领域对象的商业逻辑。然而，你可以使用Spring 整合 AspectJ来配置不在IoC容器控制=下创建的对象。查看Using AspectJ to dependency-inject domain objects with Spring。
下面的例子展示了基于XML的配置元数据的基本结构：
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="..." class="...">  
        <!-- collaborators and configuration for this bean go here -->
    </bean>

    <bean id="..." class="...">
        <!-- collaborators and configuration for this bean go here -->
    </bean>

    <!-- more bean definitions go here -->

</beans>
```
1. id属性是一个标识单独的bean定义的字符串
2. class属性是定义bean的类型，并且使用全限定名称

id属性的值能够引用合作的对象。XML引用合作的对象没有在这个例子里展现。查看Dependencies获取更多详细信息。

### 1.2.2初始化一个容器 
提供给一个**ApplicationContext**构造器的地点路径作为资源字符串来使容器从各种外部资源,如本地文件系统，Java**CLASSPATH**,等等，中加载配置元数据。
```xml
ApplicationContext context = new ClassPathXmlApplicationContext("services.xml","daos.xml");
```
> 你学习Spring IoC 容器后，可能需要知道更多有关Spring **Resource**抽象（正如Resources中所描述的)，它提供了一个方便的机制通过URI格式定义的地址来读取一个输入流。特别的，Resource路径能够被用于构造应用上下文，正如，Application Contexts and Resource Paths所描述的。
下面的例子展示了服务层对象的配置文件：
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <!-- services -->

    <bean id="petStore" class="org.springframework.samples.jpetstore.services.PetStoreServiceImpl">
        <property name="accountDao" ref="accountDao"/>
        <property name="itemDao" ref="itemDao"/>
        <!-- additional collaborators and configuration for this bean go here -->
    </bean>

    <!-- more bean definitions for services go here -->

</beans>

```
下面的例子展示了数据访问层的**daos.xml**文件：
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="accountDao"
        class="org.springframework.samples.jpetstore.dao.jpa.JpaAccountDao">
        <!-- additional collaborators and configuration for this bean go here -->
    </bean>

    <bean id="itemDao" class="org.springframework.samples.jpetstore.dao.jpa.JpaItemDao">
        <!-- additional collaborators and configuration for this bean go here -->
    </bean>

    <!-- more bean definitions for data access objects go here -->

</beans>
```
在前面的例子里，服务层有**PetStoreServiceImpl**和两个数据访问层的对象**JpaAccountDao**和**JpaItemDao**（基于JPA的对象关系映射标准）。这个**property name**元素引用了另一个Bean定义。id和ref元素之间的联系表明了合作对象之间的依赖。查看配置对象依赖的细节，查看Dependencies。
#### 组合基于XML的配置元数据
能够在多个XML文件中贯穿的bean定义非常有用。通常一个xml配置文件代表你架构中的一个逻辑层或者模块。
你可以使用应用上下文构造器来从所有的这些XML片段中加载bean定义。这个构造器导入多**Resource**位置，正如前面所展示的。可替代的，使用一个或者多个 **\<import/>**元素来从其他文件中加载bean定义。下面是示例：
```xml
<beans>
    <import resource="services.xml"/>
    <import resource="resources/messageSource.xml"/>
    <import resource="/resources/themeSource.xml"/>

    <bean id="bean1" class="..."/>
    <bean id="bean2" class="..."/>
</beans>
```
在前面的例子里，外部的bean定义从三个文件中加载：**services.xml**,**messageSource.xml**，和**themeSource.xml**。所有的地点路径相对于当前进行导入的定义文件，因此services.xml在当前导入文件的相同目录或者classpath下，messageSource,xml和themeSource.xml在一个进行导入文件之下的**resource**位置。正如你所看到的，一个首位的斜杠会被忽略。然而，给与的这些路径都是相对路径，最好就是不使用斜杠。这些文件的内容被导入，包括最顶部的 **\<beans>**元素，必须要是有效的XMLbean定义，根据Spring Sechema。
> 可以但是不推荐的是通过“../”的相对路径来引用位于父目录中的文件。这样创建了一个不属于当前应用的文件依赖。特别的，这种引用不推荐使用在classpath中（例如，classpath:../services.xml）,运行时的处理方案会选择最近的classpath根目录，然后在它的父目录中查找，classpath的改变可能会使得它指示到一个错误的目录。
> <br/>你能够总是使用全限定名的资源位置来替代相对位置路径：例如，**file:C:/config/services.xml**或者**classpath:/config/services.xml**。然而，意识到你在连接你的应用配置到一个指定的绝对位置。通常通过间接指定到绝对位置是更好的选择，例如，通过"${...}"占位符这种能够通过JVM运行时解析的系统属性。

名称空间本身就提供了导入命令特征。更多的超出普通bean定义的配置特征在Spring 提供的XML名称空间中是可用的，例如，context和util名称空间。

#### Groovy bean 定义DSL
作为另一个外部元数据配置的例子，bean定义可能够表示为Spring Groovy bean 定义 DSL，正如Grails所使用的。典型的，这样的配置用在“.groovy”文件中如下所示：
```groovy
beans{
    dataSource(BasicDataSource){
        driverClassName = "org.hsqldb.jdbcDriver"
        url ="jdbc::hsqldb:mem:grailsDB"
        username="sa"
        password=""
        settings=[mynew:"setting"]
    }
    sessionFactory(SessionFactory){
        dataSource=datasource
    }
    myService(MyService){
        nestedBean ={AnnotherBean bean ->
            dataSource = dataSource
        }
    }
}
```
这种配置风格很大程度上等同于XML定义，并且支持Spring XML配置名称空间。它也允许引入XMLbean定义文件通过**importBeans**指令。
### 1.2.3 使用容器
**ApplicationContext**是用来维护不同的bean和它们的依赖的一个现金的工厂类接口。通过使用方法**T getBean(String name,Class<T> requiredType)**，你可以获得你bean的实例。
**ApplicationContext**让你读取bean定义，如下所示：
```java
// create and configure beans
ApplicationContext context = new ClassPathXmlApplicationContext("services.xml", "daos.xml");

// retrieve configured instance
PetStoreService service = context.getBean("petStore", PetStoreService.class);

// use configured instance
List<String> userList = service.getUsernameList();
```
```kotlin
import org.springframework.beans.factory.getBean

// create and configure beans
val context = ClassPathXmlApplicationContext("services.xml", "daos.xml")

// retrieve configured instance
val service = context.getBean<PetStoreService>("petStore")

// use configured instance
var userList = service.getUsernameList()
```
在groovy配置下，启动显得非常类似。它有一个不同的上下文实现作为Groovy检测（但是也能够解析XML bean定义）。下面展示了Groovy 配置：
```java
ApplicationContext context = new GenericGroovyApplicationContext("services.groovy", "daos.groovy");

```
```groovy
val context = GenericGroovyApplicationContext("services.groovy", "daos.groovy")

```
最灵活的变量是**GenericApplicationContext**结合了读取器代表，例如，带着XML文件的**XmlBeanDefinitionReader**， 如下所示：
```java
GenericApplicationContext context = new GenericApplicationContext();
new XmlBeanDefinitionReader(context).loadBeanDefinitions("services.xml", "daos.xml");
context.refresh();
```
```groovy
val context = GenericApplicationContext()
XmlBeanDefinitionReader(context).loadBeanDefinitions("services.xml", "daos.xml")
context.refresh();
```
你可以使用**GroovyBeanDefinitionReader**来处理Groovy文件如下所示：
```java
GenericApplicationContext context = new GenericApplicationContext();
new GroovyBeanDefinitionReader(context).loadBeanDefinitions("services.groovy", "daos.groovy");
context.refresh();
```
```groovy
val context = GenericApplicationContext()
GroovyBeanDefinitionReader(context).loadBeanDefinitions("services.groovy", "daos.groovy")
context.refresh()
```
你可以混合匹配这样的读取器代表在相同的**ApplicationContext**，从不同的配置源读取bean。
你可以使用getBean来取回你的bean的实例。**ApplicationContext**接口具有一些其他的方法来取回bean，但是理智的说，你的应用代码一般用不到他们。事实上，你的应用代码应当不会调用getbean()方法，这样就根本不会依赖Spring API。例如，Spring 整合web框架提供了依赖注入给各种web框架组件例如控制器和JSF管理bean，使得你通过元数据声明指定bean依赖（例如自动注入注解）。
## 1.3 Bean Overview
一个Spring IoC容器管理一个或者更多bean。这些bean通过你提供给容器的元数据进行创建（例如，以XML\<bean/>）。
在容器内部，bean定义以**BeanDefinition**对象的形式出现，它（在其他信息以内）包含如下元数据：
* 一个包限定类名：一般的,bean的实际实现类被定义
* Bean行为配置元素，能够表示bean在容器中的行为（范围，生命周期，等等）
* 引用其他bean来保证当前bean的正常工作。这些引用被称作合作者和依赖
* 其他的配置设定在新创建的对象中设置，例如，管理连接池的bean中的pool或者使用的连接数目

这些元数据转变成了组成每个bean定义的一系列属性。下面的表格描述了这些属性：

![](./pic/beanDefinition.jpg)

除了包含bean定义包含了创建一个特定bean的信息，**ApplicationContext**实现也允许（用户）注册在容器之外创建的已经存在的对象。这可以访问通过ApplicationContext的BeanFactory通过**getBeanFactory()**方法，能够返回BeanFactory的**DefaultListableBeanFactory**的实现。**DefaultListableBeanFactory**支持注册通过**registerSingleton(..)**和**registerBeanDefinition(..)**方法。然而，一般的应用单独的工作通过普通的bean定义源文件。
> Bean的元数据和手动提供的单例实例需要越早注册越好，为了容器能够恰当的在自动注入和其他自省步骤进行处理。覆盖已经存在的元数据和单例实例在某种程度上支持，在运行时新bean的注册（并发的访问factory）并不被官方支持，并且可能导致并发访问错误，bean容器中不一致的状态，或者两者都有。

### 1.3.1 Naming Beans
每个bean有一个或者更多的指示器。这些指示器在控制它们的bean的容器类必须是唯一的。一个bean通常只有一个指示器。然而，如果需要不止一个，另外的可以被视作别名。
在基于XML的配置元数据中，你使用id属性，name属性或者一起来指定bean指示器。id属性使你清晰地特指一个id。惯例地，这些名称是字母和数字的（'myBean'，'someService'，等），但是他们也可以包含特别多字母。如果希望为bean引入其他的bean，你可以定义他们在name属性处，通过逗号，分号或者空格来分隔其他名称。作为一个历史记录，在Spring3.1版本之前，id属性被定义为xsd:ID类，限制了可能的字符。3.1版本，id属性被定义为了xsd:string类。这意味着id的唯一性是通过容器来维护的，而不是XML解析器。
你不被要求为bean提供一个name或者id。如果你没有清楚地为bean提供一个name或者id，容器会为bean生成一个独特的名称。然而如果你需要使用name来引用bean，通过使用ref元素或者一个Service Locator 风格的lookup，你需要提供一个名称。不需要提供name的动机请参考使用内部bean或者自动注入的合作者。
> Baan 命名惯例
> <br/>惯例是命名bean时使用标准的Java惯例来命名实例领域名称。这意味着，bean使用小写字母开头和驼峰格式。例如此类的名称包括，**accountManager**，**accountService**，**userDao**，**loginController**，等等。
> <br/>命名bean的一致性使得你的配置文件易读易理解。同时，如果你使用Spring AOP,当你应用给一个advice到一系列bean中时，它能起到很大的帮助。

> 扫描了classpath的组件后，Spring 为没有命名的组件生成名称，遵从前面描述的规则：根本上，采用简单类名，并将首字母转为小写。然而在某些特殊的例子中超过一个或者多个字母是大写字母，原始形式被保存。这些规则被**java.beans.Introspector.decepitalize**（Spring使用的）定义。

#### 为Bean Definition 之外的Bean创建别名
在bean定义里，你可以为bean提供不止一个名称，通过使用一个名称的id属性，或者多个name属性的结合。这些名称相当于同一个bean的别名，并且在一些场景下很有用，例如，使得应用中的每个组件通过使用对组件特定的bean名称来引用一个共同的依赖。
然而指定所有的bean的别名并不总是充足的。有时候需要在其他的地方为bean指定别名。这在巨大的系统中需要在不同的子系统中进行分散的配置，每个子系统具有自己的一套对象定义。在基于XML的配置元数据中，你可以使用**\<alias/>**元素来完成，如下所示：
```xml
<alias name="fromName" alias="toName"/>
```
在这个例子里，bean（在同一个容器）名为fromName，在使用别名定义后，被命名为toName。
例如，子系统A的配置元数据引用一个数据源通过**subsystemA-dataSource**。子系统B的数据源引用可能就叫做**subsystemB-dataSource**。当在主应用中组合这些子系统是，主系统连接到这些数据源通过**myApp-dataSource**。这三个名称都连接到同一个对象，你可以添加如下的别名定义到配置元数据中：
```xml
<alias name="myApp-dataSource" alias="subsystemA-dataSource"/>
<alias name="myApp-dataSource" alias="subsystemB-dataSource"/>
```
这样每个组件以及主应用都能够访问到数据源通过一个独特名称，并且能够保证不与其他的定义冲突（有效的创造了一个名称空间），它们能够引用相同的bean。
> Java-configuration
> <br/>如果你使用java配置，@Bean注解能够被用来配置别名，查看@Bean注解获取更多细节

### 1.3.2 初始化Bean
bean定义是创建一个或者更多对象的重要的菜谱。当容器请求或者使用配置元数据分装的bean定义来创建一个实际的对象时，会进行查找。
如果你使用XML的配置元数据，你定义对象对象类型被初始化为bean元素的class属性。这个class属性（在内部及BeanDefinition的Class属性）通常是必须的。（查看Instantiation by Using an Instance Factory Method and Bean Definition Inheritance获取更多异常）你可以以两种方式来使用Class属性：
* 一般的，在容器通过构造器反射直接创建bean是进行制定，某种程度上等同于new操作符
* 指定实际类型在调用静态工厂方法时，在更少见的例子中容器在类上调用一个静态工厂方法来创建bean。这个从调用的静态工厂方法返回的对象类型可能是同样的类，也可能是一个完全不同的类。
> 内部类名
> <br/>如果你想配置一个静态嵌套类的bean定义，你需要使用嵌套类的二进制名
> <br/>例如，如果您你有一个叫做SomeThing的类在com.example的包里，并且SomeThing有一个叫做OtherThing的嵌套静态类，bean定义中的class属性的值就是com.example.SomeThing$OtherThing。
> <br/>这意味着$字符用来分割嵌套类名和外部类名

#### 构造器初始化
当你创建了一个带构造器方法的bean，所有普通的类能够被Spring使用和兼容。这意味着类不需要实现特定的接口或者以某种指定的方式编写。简单地指定bean类就足够了。然而，取决于你使用指定bean的IoC，你可能需要定义默认（空）构造器。
Spring IoC差不多能管理所有你需要管理的类。它不局限于管理真正的JavaBean。大多数Spring使用者更喜欢使用带有默认构造器（空参数）和合适的setters和getters来容器中指定属性。你也可以使用更加异国风味的无bean风格类在你的容器中。例如你需要使用一个传统的连接池绝对不能附着javaBean配置，Spring也可以管理它。
XML配置元数据，你可以如下定义你的bean类：
```xml
<bean id="exampleBean" class="examples.ExampleBean"/>

<bean name="anotherExample" class="examples.ExampleBeanTwo"/>
```
对于提供参数给构造器的机制以及在对象创建后提供实例属性的，查看Injecting Dependencies。

#### 静态工厂方法实例化
当定义一个使用静态工厂方法创建的bean是，使用class属性来指定类并且使用factory-method来指定它的静态工厂方法。你可以调用这个方法（可选参数，如后面所说的）并且返回一个活动对象，它被看作是通过构造器创建的。在遗留代码里，这样的bean定义被称作静态工厂。
下面的bean定义指定了一通过工厂方法创建的bean。这个定义没有指定返回对象的类型，只有包括工厂方法的类名。在这个例子中，**createInstance()**方法应当是一个静态方法。下面的例子展示了如何指定工厂方法：
```xml
<bean id="clientService"
    class="examples.ClientService"
    factory-method="createInstance"/>
```
下面的例子指定了和前面bean定义工作的类：
```java
public class ClientService {
    private static ClientService clientService = new ClientService();
    private ClientService() {}

    public static ClientService createInstance() {
        return clientService;
    }
}
```
```kotlin
class ClientService private constructor() {
    companion object {
        private val clientService = ClientService()
        fun createInstance() = clientService
    }
}
```
对于提供参数给工厂方法和为工厂返回的对象实例设定属性的机制细节，查看 Dependencies and Configuration in Detail。
#### 通过使用实例工厂方法
类似于静态工厂方法，通过实例工厂方法调用一个容器中存在的bean的非静态的实例方法来创建新bean。为了使用这种机制，需要空出class属性，在factory-bean中指定当前容器中存在的包含创建对象的实例方法bean名称。设定factory-method为它的工厂方法，下面展示了如何配置这样的bean：
```xml
<!-- the factory bean, which contains a method called createInstance() -->
<bean id="serviceLocator" class="examples.DefaultServiceLocator">
    <!-- inject any dependencies required by this locator bean -->
</bean>

<!-- the bean to be created via the factory bean -->
<bean id="clientService"
    factory-bean="serviceLocator"
    factory-method="createClientServiceInstance"/>
```

下面展示了相关的类：
```java
public class DefaultServiceLocator {

    private static ClientService clientService = new ClientServiceImpl();

    public ClientService createClientServiceInstance() {
        return clientService;
    }
}
```
```kotlin
class DefaultServiceLocator {
    companion object {
        private val clientService = ClientServiceImpl()
    }
    fun createClientServiceInstance(): ClientService {
        return clientService
    }
}
```
一个工厂类可以拥有不止一个工厂方法，如下所示：
```xml
<bean id="serviceLocator" class="examples.DefaultServiceLocator">
    <!-- inject any dependencies required by this locator bean -->
</bean>

<bean id="clientService"
    factory-bean="serviceLocator"
    factory-method="createClientServiceInstance"/>

<bean id="accountService"
    factory-bean="serviceLocator"
    factory-method="createAccountServiceInstance"/>
```
```java
public class DefaultServiceLocator {

    private static ClientService clientService = new ClientServiceImpl();

    private static AccountService accountService = new AccountServiceImpl();

    public ClientService createClientServiceInstance() {
        return clientService;
    }

    public AccountService createAccountServiceInstance() {
        return accountService;
    }
}
```
```kotlin
class DefaultServiceLocator {
    companion object {
        private val clientService = ClientServiceImpl()
        private val accountService = AccountServiceImpl()
    }

    fun createClientServiceInstance(): ClientService {
        return clientService
    }

    fun createAccountServiceInstance(): AccountService {
        return accountService
    }
}
```
这个方法展示了factory bean它可以通过依赖注入进行管理和配置。查看Dependencies and Configuration in Detail。
> 在Spring文档中，“factory bean”指的是在Spring容器中进行配置并且通过实例或者静态工厂方法创建对象的一类bean。对应的，**FactoryBean**（注意大写）代表的是Spring特有的工厂bean实现类。

#### 决定Bean的运行时类型
指定bean的运行时类型是一个需要决心的重大问题。一个bean元数据定义的特定类只是一个初始化类引用，可能结合一个声明的工厂方法，或者成为一个产生不同运行时bean类型的**FactoryBean**，或者根本不设置在实例级工厂方法（通过解析特定的factory-bean名称来替代）。另外的，AOP代理可能通过基于接口的代理在目标bean的实际类型（它实现的接口）有限暴露的接口进行封装。
推荐的方式是通过在运行时的特定bean上调用**BeanFactory.getType**以获取其真实的运行时类型。这将所有的情况都考虑在内，并且**BeanFactory.getType**将会返回同样的bean name。

## 1.4依赖
一个典型的企业应用不是由单独的对象组成的（或者按照Spring的术语叫做Bean）。即使简单的应用也需要几个对象一起工作来呈现给终端用户一个可用的应用。这就是接下来的部分解释如何从几个独立的bean 定义到一个完整实现的几个对象协作达成目标的应用。
### 1.4.1依赖注入
依赖注入是一个对象定义它们的依赖（即，共同工作的其他对象）仅仅通过构造器参数，传递参数到工厂方法，或者在实例构造后或者从工厂方法返回后设定对象实例的属性。容器在创建bean时会将依赖注入。这个过程从根本上反转（因此叫做控制反转）了bean控制初始化或者定位它的依赖通过直接的类构造或者Service Locater 模式。
当使用依赖注入来给对象提供它们的依赖时，代码更赶紧，并且解耦更有效。对象不再查找它自己的依赖，并且不需要知道他一来的位置或者依赖的类。作为结果，你的类更容易测试，有一起当依赖基于接口或者抽象基类，可以允许使用stub或者mock实现来进行单元测试。
DI存在两个主要的方式：基于构造器的依赖注入和基于Setter的依赖注入。
#### 基于构造器的依赖注入
基于构造器的依赖注入通过容器调用具有参数的构造器，每个都代表着一个依赖，来实现。调用一个具有特定参数的额静态工厂方法来构造bean是答题差不多的，这种方式对待构造器参数和静态工厂方法是类似的。下面的例子展示了一个类能够使用构造器来进行构造器注入：
```java
public class SimpleMovieLister {

    // the SimpleMovieLister has a dependency on a MovieFinder
    private MovieFinder movieFinder;

    // a constructor so that the Spring container can inject a MovieFinder
    public SimpleMovieLister(MovieFinder movieFinder) {
        this.movieFinder = movieFinder;
    }

    // business logic that actually uses the injected MovieFinder is omitted...
}
```

# 3 验证，数据绑定和类型转换
## 3.1 通过Spring Validator 接口来验证
Spring提供Validator接口特征供你用来验证对象，这个Validator接口通过使用一个Errors对象来工作，即，在验证的同时，验证器能通过Errors对象来报告错误。
考虑如下的小数据对象：
```java
public class Person {

    private String name;
    private int age;

    // the usual getters and setters...
}
```
下面的例子通过实现Validator的org.springframework.validation.Validator接口的两个方法提供了Person类的验证行为：
* supports(Class): 这个Validator是否能够验证提供的类实例
* validate(Object,org.springframework.validation.Errors): 验证给定的对象，并且为了防止验证错误，通过给定的Errors对象来注册。

实现一个Validator相当直接，尤其当你熟悉Spring Framework提供的ValidationUtils帮助类。下面的例子实现了Person实例的Validator：
```java
public class PersonValidator implements Validator {

    /**
     * This Validator validates only Person instances
     */
    public boolean supports(Class clazz) {
        return Person.class.equals(clazz);
    }

    public void validate(Object obj, Errors e) {
        ValidationUtils.rejectIfEmpty(e, "name", "name.empty");
        Person p = (Person) obj;
        if (p.getAge() < 0) {
            e.rejectValue("age", "negativevalue");
        } else if (p.getAge() > 110) {
            e.rejectValue("age", "too.darn.old");
        }
    }
}
```
这个ValidationUtils类使用静态的rejectIfEmpty(..)方法来拒绝name属性如果它时null或者为空字符串。你可以通过查看ValidationUtils的javadoc来查看它提供了哪些功能除了下面的例子提供的。

当实现一个单一Validator类在一个复杂对象内来验证一个嵌套对象是可能的时候，可能为每一个嵌套的对象封装验证逻辑为它自己的Validator实现是更好的做法。一个简单的复杂对象的例子可能是一个有两个String属性（firstname和secondname）以及一个复杂的Address秀i昂莱组成的。Address Object可能被独立于Customer使用，因此需要实现一个独立的AddressValidator。如果你需要你的CustomerValidator来重用AddresssValidator类包含的逻辑而不是复制粘贴，你可以在你的CustomerValidator中独立的注入和实例化一个AddressValidator,如下例子所示：
```java
public class CustomerValidator implements Validator {

    private final Validator addressValidator;

    public CustomerValidator(Validator addressValidator) {
        if (addressValidator == null) {
            throw new IllegalArgumentException("The supplied [Validator] is " +
                "required and must not be null.");
        }
        if (!addressValidator.supports(Address.class)) {
            throw new IllegalArgumentException("The supplied [Validator] must " +
                "support the validation of [Address] instances.");
        }
        this.addressValidator = addressValidator;
    }

    /**
     * This Validator validates Customer instances, and any subclasses of Customer too
     */
    public boolean supports(Class clazz) {
        return Customer.class.isAssignableFrom(clazz);
    }

    public void validate(Object target, Errors errors) {
        ValidationUtils.rejectIfEmptyOrWhitespace(errors, "firstName", "field.required");
        ValidationUtils.rejectIfEmptyOrWhitespace(errors, "surname", "field.required");
        Customer customer = (Customer) target;
        try {
            errors.pushNestedPath("address");
            ValidationUtils.invokeValidator(this.addressValidator, customer.getAddress(), errors);
        } finally {
            errors.popNestedPath();
        }
    }
}
```
验证的错误报告给Errors对象被传递给验证器。在Spring Web MVC中，你可以使用<spring:bind/>标签来检查错误信息，但是你也可以自己来检查Errors对象。更多关于方法的信息能够在javadoc中找到。