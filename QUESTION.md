## 1 什么是 Spring Framework？

Spring makes it easy to create Java enterprise applications. It provides everything you need to embrace the Java language in an enterprise environment, with support for Groovy and Kotlin as alternative languages on the JVM, and with the flexibility to create many kinds of architectures depending on an application’s needs.

## 2 Spring Framework 有哪些核心模块？
```
spring-core：Spring 基础 API 模块，如资源管理，泛型处理
spring-beans：Spring Bean 相关，如依赖查找，依赖注入
spring-aop : Spring AOP 处理，如动态代理，AOP 字节码提升
spring-context : 事件驱动、注解驱动，模块驱动等
spring-expression：Spring 表达式语言模块
```
## 3 Spring Framework 的优势和不足是什么?

## 4 什么是 IoC ？

简单地说，IoC 是反转控制，类似于好莱坞原则，主要有依赖查找和依赖注入实现

## 5 依赖查找和依赖注入的区别？

答：依赖查找是主动或手动的依赖查找方式，通常需要依赖容器或标准 API 实现。而依赖注入则是手动或自动依赖绑定的方式，无需依赖特定的容器和 API

## 6 Spring 作为 IoC 容器有什么优势？

典型的 IoC 管理，依赖查找和依赖注入、AOP 抽象、事务抽象、事件机制、SPI 扩展、强大的第三方整合、易测试性、更好的面向对象

## 7 什么是 Spring IoC 容器？

Spring Framework implementation of the Inversion of Control (IoC) principle. IoC is also known as dependency injection (DI). It is a process whereby objects define their dependencies (that is, the other objects they work with) only through constructor arguments, arguments to a factory method, or properties that are set on the object instance after it is constructed or returned from a factory method. The container then injects those dependencies when it creates the bean.

## 8 BeanFactory 与 FactoryBean？

BeanFactory 是 IoC 底层容器

FactoryBean 是 创建 Bean 的一种方式，帮助实现复杂的初始化逻辑

## 9 Spring IoC 容器启动时做了哪些准备？

IoC 配置元信息读取和解析、IoC 容器生命周期、Spring 事件发布、国际化等，更多答案将在后续专题章节逐一讨论

## 10 如何注册一个 Spring Bean？

通过 BeanDefinition 和外部单体对象来注册

## 11 什么是 Spring BeanDefinition？

回顾“定义 Spring Bean” 和 “BeanDefinition 元信息”

## 12 Spring 容器是怎样管理注册 Bean

将在后续专题章节详细讨论，如：IoC 配置元信息读取和解析、依赖查找和注入以及 Bean 生命周期等。

## 13 有多少种依赖注入的方式？

构造器注入、Setter 注入、字段注入、方法注入、接口回调注入

## 14 你偏好构造器注入还是 Setter 注入？

两种依赖注入的方式均可使用，如果是必须依赖的话，那么推荐使用构造器注入，Setter 注入用于可选依赖。

## 15 Spring 依赖注入的来源有哪些？

答案将《Spring IoC依赖来源》章节中继续讨论

## 16 注入和查找的依赖来源是否相同？

否，依赖查找的来源仅限于 Spring BeanDefinition 以及单例对象，而依赖注入的来源还包括 Resolvable Dependency 以及@Value 所标注的外部化配置

## 17 单例对象能在 IoC 容器启动后注册吗？

 可以的，单例对象的注册与 BeanDefinition 不同，BeanDefinition 会 被 ConfigurableListableBeanFactory#freezeConfiguration() 方法影响，从而冻结注册，单例对象则没有这个限制。

## 18 Spring依赖注入的来源有哪些？

- Spring BeanDefinition

- 单例对象

- Resolvable Dependency

- @Value 外部化配置

## 19 Spring 內建的 Bean 作用域有几种？

singleton、prototype、request、session、application 以及 websocket

## 20 singleton Bean 是否在一个应用是唯一的？

否，singleton bean 仅在当前 Spring IoC 容器（BeanFactory）中是单例对象。

## 21 “application”Bean 是否被其他方案替代？

可以的，实际上，“application” Bean 与“singleton” Bean 没有本质区别

## 22 - BeanPostProcessor 的使用场景有哪些？

BeanPostProcessor 提供 Spring Bean 初始化前和初始化后的生命周期回调，分别对应postProcessBeforeInitialization以及postProcessAfterInitialization 方法，允许对关心的 Bean 进行扩展，甚至是替换。

加分项：其中，ApplicationContext 相关的 Aware 回调也是基于BeanPostProcessor 实现，即ApplicationContextAwareProcessor

## 23 BeanFactoryPostProcessor 与BeanPostProcessor 的区别

BeanFactoryPostProcessor 是 Spring BeanFactory（实际为ConfigurableListableBeanFactory） 的后置处理器，用于扩展BeanFactory，或通过 BeanFactory 进行依赖查找和依赖注入。

加分项：BeanFactoryPostProcessor必须有 Spring ApplicationContext执行，BeanFactory无法与其直接交互。

而BeanPostProcessor则直接与BeanFactory关联，属于N对1 的关系。

## 24 BeanFactory 是怎样处理 Bean 生命周期？

BeanFactory 的默认实现为 DefaultListableBeanFactory，其中 Bean生命周期与方法映射如下：

- BeanDefinition 注册阶段 - registerBeanDefinition

- BeanDefinition 合并阶段 - getMergedBeanDefinition

- Bean 实例化前阶段 - resolveBeforeInstantiation

- Bean 实例化阶段 - createBeanInstance

- Bean 初始化后阶段 - populateBean

- Bean 属性赋值前阶段 - populateBean

- Bean 属性赋值阶段 - populateBean

- Bean Aware 接口回调阶段 - initializeBean

- Bean 初始化前阶段 - initializeBean

- Bean 初始化阶段 - initializeBean

- Bean 初始化后阶段 - initializeBean

- Bean 初始化完成阶段 - preInstantiateSingletons

- Bean 销毁前阶段 - destroyBean

- Bean 销毁阶段 - destroyBean

## 25 Spring 內建 XML Schema 常见有哪些？
      命名空间 所属模块 Schema 资源 URL
      beans spring-beans https://www.springframework.org/schema/beans/spring-beans.xsd
      context spring-context https://www.springframework.org/schema/context/springcontext.xsd
      aop spring-aop https://www.springframework.org/schema/aop/spring-aop.xsd
      tx spring-tx https://www.springframework.org/schema/tx/spring-tx.xsd
      util spring-beans https://www.springframework.org/schema/util/spring-util.xsd
      tool spring-beans https://www.springframework.org/schema/tool/spring-tool.xsd

## 26

## 27



