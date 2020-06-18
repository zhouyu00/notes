################################################
Spring Boot Auto-Configuration
################################################

理解auto-configuration
==============================

Set the debug=true in the application.properties file.

学习auto-configuration如何工作的
**************************************

To enable the auto-configuration magic, Spring Boot uses the @EnableAutoConfiguration annotation. Normally we use the @SpringBootApplication annotation which includes our @EnableAutoConfiguration annotation. The @EnableAutoConfiguration annotation enables the auto-configuration of Spring ApplicationContext by scanning the classpath components and registers the beans that are matching various Conditions.

定制Spring Boot
==============================
利用Spring Boot properties进行定制
**************************************
替换已生成的Bean
**************************************
禁用特定的auto-configuration类
**************************************
修改库的依赖
**************************************
基于属性的配置外部化
==============================
属性的覆盖（overridden）顺序
**************************************
重命名application.properties文件
**************************************
外部配置应用程序属性
==============================
使用@EnableConfigurationProperties注解
*********************************************
基于日志记录的调优
==============================
输出日志记录
**************
使用YAML配置文件
==============================
YAML里面的层级属性
****************************
单一YAML文件中的多个profiles属性
***********************************
定制应用程序错误页面
==============================

Custom Starter with Spring Boot
==================================
* https://www.javadevjournal.com/spring-boot/spring-boot-custom-starter/

参考
==============================
* https://docs.spring.io/spring-boot/docs/current/reference/html/appendix-auto-configuration-classes.html
* https://www.javadevjournal.com/spring-boot/how-spring-boot-auto-configuration-works/