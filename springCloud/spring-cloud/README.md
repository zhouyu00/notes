# 本工程的目的

Spring Cloud 速成班

## 部署Wiki

本Wiki使用Python3 + Sphinx构建，关于如何部署本地Wiki，参见：[Sphinx培训](http://fsdtraining.com/en/latest/pages/sphinx.html) 

## 本Wiki内容

1. Spring Boot Cloud 学习
   - 课程进度
   - 练习进度
   - github
2. 初识 Maven
   - Maven介绍
   - 多线程
   - 跳过测试
   - 编译失败后，接着编译
   - 编译到最后再报错
   - 使用 Nexus 本地私服
   - 使用 Aliyun 国内镜像
   - 指定 Repository 目录
   - Maven Properties
   - Maven Sources
   - Maven Proxy
     - 命令行设置
     - 配置文件
     - Dependency local Jar
   - Install Jar
   -  MAVEN 属性
     - 内置属性
     - POM属性
     - 自定义属性属性
     - setting属性
     - ava系统属性
     - 环境变量属性
   - MAVEN_OPTS
   - Nexus Security
   - Error in Eclipse
   - 参考
3. 初识 Git
   - 常见Git命令
   - Connecting with SSH
   - RPC
     - Web
     - SSH
   - API
4. 初识 Docker
   - 介绍
   - Install
     - Centos
     - Install Docker Compose
   - image and compose
   - command
   - 搭建 DB server
     - docker-compose.yml
     - mongo-init.sh
     - start.sh
   - 备份及迁移redis数据
   - Issue
   - 参考
5. Spring Boot CLI
   - 安装Spring Boot CLI
     - 从安装文件中手动安装
     - 使用SDKMAN!安装
     - 利用OSX Homebrew安装
     - 使用MacPorts安装
   - 开始使用CLI
   - 使用CLI初始化项目
   - 参考
6. Spring Boot 2.x 学习
   - Spring Boot 概述
   - 常规概念
     - PO
     - BO
     - VO
     - POJO
     - DTO
     - DAO
   - 快速上手
     - 在线界面初始化项目
     - 环境准备
     - pom.xml
     - 添加Code
     - 运行程序
     - IDE中执行
       - mvn执行
     -  创建 an Executable Jar
     - 部署
   - 参考
7. Spring Boot Controller
   - 理解 Controller
   - 实现REST服务
   - ResponseEntity
   - RequestMapping
   - Controller中获取参数
     - Controller方法的形参
     - HttpServletRequest
     - 通过Bean接收
     - @PathVariable
     - @ModelAttribute
     - @RequestParam
     - @RequestBody
     - @RequestHeader @CookieValue
   - Error Handling
8. Spring Boot Service
   - 理解 Service
   - @Autowired
   - 类中获取属性数据
     - @ConfigurationProperties
     - @Value
   - Error Handling for REST
   - Spring boot自定义注解
     - 使用自定义注解来统计方法的执行时间
       - 创建@AnalysisActuator
       - 创建Aspect
       - 使用
9. Spring Boot Pages
   - 理解 Pages
   - 模板引擎
     - Jsp
     - FreeMarker
     - Groovy
     - Thymeleaf
   - 页面获取数据
     - Model
     - ModelMap
     - ModelAndView
     - @ModelAttribute
   - webjars
10. Spring Boot Entity
   - 概要
   - Entity
     -  Annotation
       - @Id
       - @CreatedDate
       - @Column
       - @Transient
       - @Temporal
       - @Enumerated
   - 日期处理
     - 配置文件中配置
     - @JsonFormat
     - @DateTimeFormat
     - @Temporal
   - Relationship
     - one-to-one
       - Foreign Key
       - Shared Primary Key(推荐)
       - Join Table
     - one-to-many
       - Unidirectional
       - Unidirectional with @JoinColumn
       - Bidirectional(推荐)
     - many-to-many
   -  H2
     - 默认配置
     - 更改H2控制台的路径
   -  初始化数据库数据
   - 参考
11. Spring Data JPA
   - 依赖
   - 创建和删除JPA数据库
   - Query Creation
   - Using @Query
   - Using Named Parameters
   - Using SpEL Expressions
   - Modifying Queries
   - Init
   - 参考
12. Spring Data REST
   - 概要
   - Maven依赖
   - Demo
   - 参考
13. Spring Boot Redis
   - 开始使用Redis
   - Maven依赖
   - Configuration
   - Demo
     - pom
     - entity
     - repository
     - controller
     - application.properties
   - 参考
14. Spring Boot MongoDB
   - 开始使用MongoDB
   - Maven依赖
   - CRUD
     - Entity
     - Repository
     - Service
     - RestController
     - application.properties
     - Mongodb
   - 参考
15. Spring Boot Auto-Configuration
   - 理解auto-configuration
     - 学习auto-configuration如何工作的
   - 定制Spring Boot
     - 利用Spring Boot properties进行定制
     - 替换已生成的Bean
     - 禁用特定的auto-configuration类
     - 修改库的依赖
   - 基于属性的配置外部化
     - 属性的覆盖（overridden）顺序
     - 重命名application.properties文件
   - 外部配置应用程序属性
     -  使用@EnableConfigurationProperties注解
   - 基于日志记录的调优
     - 输出日志记录
   - 使用YAML配置文件
     - YAML里面的层级属性
     - 单一YAML文件中的多个profiles属性
   - 定制应用程序错误页面
   - Custom Starter with Spring Boot
   - 参考
16. Spring Boot Security
   - 概念
     - 启用Security
     - 覆盖默认用户和密码
     - 自定义配置
   - JWT
     - 术语
     - JWT
   - OAuth2
     - 概念
       - 快递员问题
       - 授权机制的设计
       - 互联网场景
       - 令牌与密码
       - oauth2-github demo
     - 最小化授权服务器
       - 添加依赖
       - 添加@EnableAuthorizationServer注释
       - 指定client ID 和 secret
     - 自定义授权服务器
       - 初始化用户
       - 自定义callback页面
   - 参考
17. Spring Boot Actuator
   - Actuator介绍
   -  启用Actuator
   - Spring Boot 1.X 中的Actuator
     - 分析Actuator的接口
     - 显示配置细节
     - 利用接口显示指标
     - 显示应用程序信息
     - 关闭应用程序
     - 自定义Actuator
       - 启用或禁用某个Actuator接口
       - 更改接口ID
       - 更改Actuator接口的灵敏度
       - 编写自定义健康指标
     - 创建一个自定义Endpoint
     - 对Actuator接口进行安全控制
     - Further Customization
   - Spring Boot 2.X 中的Actuator
     - 分析Actuator的接口
       - 启用或禁用某个Endpoint
     - 创建一个自定义endpoint
     - 显示git详细信息
       - 指定git地址
       - 显示全部信息
       - 关闭git.properties文件的创建
       - Verbosity
       - 过滤敏感信息
     - 对Actuator接口进行安全控制
   - spring-boot-admin
   - 参考
   - 小结
18. Spring Boot RESTful
   - 基于Spring Boot的微服务
     - bootstrap.yml和application.yml简介
     - 简单的微服务示例
   - Spring Data简介
     - Apache Ignite存储库
     - Spring Data MongoDB
     - Spring Data JPA
   - 小结
19. Springfox-Swagger2
   - Maven Dependency
   - Configuration
   - Verification
   - 参考
20. Spring Cloud
   - 原生云应用程序架构
     - 微服务架构
     - 微服务的优点
     - 微服务面临的挑战
   - 简介
     - 云和微服务程序的构造块
     - Spring Cloud应用
   - 配置Spring Cloud应用程序
   - 小结
21. Spring Cloud Config
   - 介绍
   - 配置Server
     - 搭建项目
     - 创建Git存储库
     - 检验内容
   - 配置Client
     - 搭建项目
     - 创建客户端属性文件
     - 检验内容
22. Spring Cloud Netflix
   - Netflix
22.2. 小结
23. Spring Cloud Eureka
   - 服务发现
   - Eureka
     - Eureka Server
     - Eureka Client
   - 发现REST服务
     - EurekaClient
     - DiscoveryClient
   - 使用REST服务
   - 负载平衡
   - 参考
24. Spring Cloud Feign
   - 介绍
   - 依赖
   - Feign Client
   - 自定义配置
     - 自定义Bean配置
     - 使用属性文件配置
     - Interceptors
   - Feign with Eureka
     - Hystrix
     - Logging
     - Error处理
   - 参考
25. Spring Cloud Zuul
   - Spring Cloud Zuul
   - 参考
26. ELK
   - Elasticsearch
   - Logstash
   - Kibana
   - 参考
27. Kubernetes学习
   - 参考
28. Assignment
   - Maven
     - 练习的目标
     - 练习的要求
   - CRUD
     - 练习的目标
     - 练习的要求
29. Spring Cloud Interview
   - 问题集
