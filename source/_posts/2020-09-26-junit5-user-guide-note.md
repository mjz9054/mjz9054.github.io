---
title: JUnit 5 User Guide Note
date: 2020-09-26 13:28:43
tags: [JUnit5, JUnit]
---

在项目里使用JUnit写单元测试的时候，时常遇到一个注解在不同的包里都定义了，例如`@Test`可能来自于`org.junit.Test`，也可能来自于`org.junit.jupiter.api.Test`。有时候总是有些迷惑，在查看了JUnit5的用户文档以及其他关于JUnit5的介绍之后，有了一些理解，这里记录一下，加深印象。

<!--more-->

## JUnit 5

`JUnit5`是由多个模块组成的。

> JUnit 5 = JUnit Platform + JUnit Jupiter + JUnit Vintage

`JUnit Platform`是测试框架在 JVM 上启动的基础。它还定义了`TestEngine`的API，可以用来开发基于 Platform 的测试框架。

`JUnit Jupiter`是`JUnit5`中用来编写测试以及扩展的编程模型及扩展模型的集合。`Jupiter`的子项目还提供了运行`Jupiter`测试的`TestEngine`。

`JUnit Vintage`提供兼容以往基于`JUnit3`, `JUint4`版本的测试引擎。

[JUnit5 User Guide](https://junit.org/junit5/docs/current/user-guide/)

## org.junit.Test 与 org.junit.jupiter.api.Test

`org.junit.Test` 是 JUnit5 之前所使用的注解，来自于`JUnit Vintage`口快。`org.junit.jupiter.api.Test` 是 JUnit5 新增的注解，来源于`JUnit Jupiter`模块。

如果项目使用的是Junit5 的来进行单元测试，那么为了避免在编写单元测试时产生疑惑或者不必要的选择，可以排除`JUnit Vintage`，还可以排除`junit:junit`。

以下是排除方法，并没有实际测试，待验证。
```XML
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
    <exclusions>
        <exclusion>
            <groupId>org.junit.vintage</groupId>
            <artifactId>junit-vintage-engine</artifactId>
        </exclusion>
        <exclusion>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
        </exclusion>
    </exclusions>
</dependency>
```

```Gradle
testImplementation("org.springframework.boot:spring-boot-starter-test") {
    exclude("org.junit.vintage:junit-vintage-engine")
    exclude("junit:junit")
}
```

## @ExtendWith

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