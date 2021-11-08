# mybatis 

##  配置
配置文档的顶层结构如下：
* configuration(配置)
  * properties(属性)
  * settings(设置)
  * typeAliases（类型别名）
  * typeHander(类型处理器)
  * objectFactory(对象工厂)
  * plugins(插件)
  * environments(环境配置)
    * environment(环境变量)
      * transactionManager(事务管理器)
      * dataSource(数据源)
    * databaseIdProvider(数据库厂商标识)
    * mappers(映射器)

多次配置的属性加载顺序
* 首先读取在properties元素体内指定的属性
* 然后根据properties中的resource属性读取类路径下的属性文件，或者根据url指定的路径读取属性文件，并覆盖之前读取的同名属性
* 最后读取作为方法参数传递的属性，并覆盖之前读取的同名属性

### properties

### settings
| 设置名|描述| 有效值| 默认值|
|-------|---|--------|------|
|cacheEnabled|全局性的开启或关闭所有映射器配置文件中已配置的任何缓存|true/false|true|
|lazyLoadingEnabled|延迟加载的全局开关。|||

|defaultSqlProviderType|