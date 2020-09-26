---
title: JUnit 5 User Guide Note
date: 2020-09-26 13:28:43
tags: [JUnit5, JUnit]
---

在项目里使用JUnit写单元测试的时候，时常遇到一个注解在不同的包里都定义了，例如`@Test`可能来自于`org.junit.Test`，也可能来自于`org.junit.jupiter.api.Test`。有时候总是有些迷惑，在查看了JUnit5的用户文档以及其他关于JUnit5的介绍之后，有了一些理解，这里记录一下，加深印象。

<!--more-->

### JUnit 5

  `JUnit5`是由多个模块组成的。
> JUnit 5 = JUnit Platform + JUnit Jupiter + JUnit Vintage

`JUnit Platform`是测试框架在 JVM 上启动的基础。它还定义了`TestEngine`的API，可以用来开发基于 Platform 的测试框架。

`JUnit Jupiter`是`JUnit5`中用来编写测试以及扩展的编程模型及扩展模型的集合。`Jupiter`的子项目还提供了运行`Jupiter`测试的`TestEngine`。

`JUnit Vintage`提供兼容以往基于`JUnit3`, `JUint4`版本的测试引擎。

### @ExtendWith

`@ExtendWith` 是 `@RunWith`的进化。

MockitoExtension 与 MockitoJUnitRunner
```JAVA
// 等价
@ExtendWith(MockitoExtension.class) // JUnit 5
@RunWith(MockitoJUnitRunner.class) // JUnit 4
```

SpringExtension 与 SpringJUnit4ClassRunner
```JAVA
// 等价
@ExtendWith(SpringExtension.class) // JUnit 5
@RunWith(SpringJUnit4ClassRunner.class) // JUnit 4
```

`MockitoExtension` 与 `SpringExtension`

 MockitoExtension 主要用来 `@Mock`和`@InjectMocks`这样的注解，它不会加载到很多不需要的 Spring 组件。 SpringExtension 则额外支持了`@MockBean`的注解，它会加载 Spring 运行所需要的一些组件。

一般在不需要 Spring 容器配合完成单元测试的情况下，使用`MockitoExtension`即可，这样启动速度会相对快一些。