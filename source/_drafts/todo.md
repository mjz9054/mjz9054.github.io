---
title: todo
date: 2020-09-14 09:27:10
tags:
---

#### Unit test 不同jar包，注解等的不同之处
`assertj`, `junit`, `nhaarman`
`@ExtendWith`,`MockitoExtension`,`SpringExtension`
`org.junit.Test`,`org.junit.jupiter.api.Test`
`org.junit.Test`: 是来自 JUnit3, JUint4 的注解。如果项目中引入的是 JUnit5，而不需要要用到 JUint4 的时候，可以从依赖里面排除这个包。
`org.junit.jupiter.api.Test` : 是 Junit5 提供的注解。

#### log4j

#### 读书

#### Gradle

#### Jenkins

#### Python
用Python，爬取一些数据，做下可视化分析

#### 语言
英语
日语
粤语

### An Exception
org.springframework.web.client.ResourceAccessException: I/O error on POST request for "xxx url" cannot retry due to server authentication, in streaming mode; nested exception is java.net.HttpRetryException: cannot retry due to server authentication



#### MyISAM 与 InnoDB 对 B+ 树的不同使用
MyISAM 和 InnoDB 的索引都是使用 B+ 树的数据结构实现的。
MyISAM 索引和数据是不同的，可以理解为不同类型的数据，而InnoDB的索引也是数据，和具体数据无差。