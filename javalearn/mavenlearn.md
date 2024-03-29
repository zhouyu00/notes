# What is maven

# Feature Summary 特性总结
下面是Ｍaven总的来说(in a nutshell)的关键特性：
＊　简单的依照最佳实践的项目创建－几秒钟就能获得一个


#　Maven Users Centre

## Running Maven Tools
### Maven Phases　Maven阶段
尽管很难全部列出，这些都是最常见的默认执行的生命阶段
* validate: 验证项目是正确的并且所有的信息都是必要的
* compile: 编译项目的源码
*  test:　使用一个单元测试框架来测试编译的源码。这些测试需要被打包和部署
* package: 打包编译后的代码并且以可共享的形式例如JAR打包 
* integration-test: 执行并且部署包如果整合到一个完整性测试能够被运行的环境是必要的
* verify: 运行所有检查包有效性和满足质量标准的检查
* install: 安装到本地仓库，或者本地作为其他仓库的依赖
* deploy: 在一个系统或者环境中完成，讲最终的包发送到远程仓库分享给其他的开发者或者项目

下面有两个不在上面默认列表中的阶段：
* clean: 清除之前的builds创建的工程
* site: 生成项目文档
阶段是对应到潜在的目标，每个阶段执行的特殊目标依赖于项目打包的目标。

## Getting Started Guide

### Introduction to the Building Lifecycle
#### Build Lifecycle Basics　构建生命周期基础
maven基于几个构建生命周期的中心概念。这是构建和分享一个特定的制品（项目）清楚定义的几个过程。
对于构建项目的人，这意味着只需要少数几个命令就可以构建任何maven项目，POM会保证他们得到他们想要的
有三个内置的构建生命周期：default,clean和site。default生命周期操作你的项目部署，clean生命周期操作项目的清理，site生命周期操作你项目的web站点

#### Usual Command Line Calls
#### A Build Phase is Made Up of Plugin Goals
然而，尽管构建阶段代表了构建生命周期的一个特定的步骤，但是它的行为责任可能会发生变化。