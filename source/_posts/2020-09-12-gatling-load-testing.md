---
title: Gatling - Load testing
date: 2020-09-12 07:59:45
tags: [Gatling, Performance Testing]
---

## 为什么要做压力测试
1. 评估系统的能力
2. 验证系统的稳定性和可靠性
3. 对比，确认性能优化是否有效及程度
4. 瓶颈

## Gatling 
### Gatling 的优势
Gatling的高性能保证：`Scala`,`Akka`,`Netty`
`Html Report` 使得输出的报告更易读和共享
`DSL (domain-specific language)` 面向压测，使`inject`的问题简单明了。

### 脚本编写

Gatling中有几个术语：`Simulation`, `Scenario`, `Group`, `Request`, `Injection Profile`

![](/images/gatling_terminology.png)

#### `Simulation`
当写 script 时，都需要继承的接口，是测试脚本的基础

```JAVA
class BasicSimulation extends Simulation {
  val httpConf = http
    .baseURL("http://computer-database.gatling.io")
    .acceptHeader("text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8")
    .doNotTrackHeader("1")
    .acceptLanguageHeader("en-US,en;q=0.5")
    .acceptEncodingHeader("gzip, deflate")
    .userAgentHeader("Mozilla/5.0 (Windows NT 5.1; rv:31.0) Gecko/20100101 Firefox/31.0")

  val scn = scenario("BasicSimulation")
    .exec(http("request_1")
    .get("/"))
    .pause(5)

  setUp(
    scn.inject(atOnceUsers(1))
  ).protocols(httpConf)
}
```

#### `Scenario`
`Scenario` 是 `Group` 的编排，可用于模拟真实的行为。配合`Injection Profile`使用，设定压测时间，压测并发用户等等参数。

```JAVA
  val scn = scenario("BasicSimulation")
    .exec(http("request_1")
    .get("/"))
    .pause(5)

  setUp(
    scn.inject(atOnceUsers(1))
  ).protocols(httpConf)
  ```


#### `Group`
`Group` 是多个 `Request` 的合集，例如一个界面上设计的多个接口的调用，可以用 `Group` 组织在一起。

```JAVA
exec(http("request_1")
  .get("/"))
  .pause(5)
```

#### `Request`
`Request` 可以理解为 Script 的基本单元，对应每一个请求或者API。

####  `Inject Profile`
`Inject Profile` 采用 DSL 语言，简单明了，可以自由组合。
`Inject Profile` 有两种模式 ： `Open Mode` 和 `Close Mode`。 对比之下，`Open Mode` 主要是定义单位时间新增的用户，`Close Mode` 主要用于设置并发用户数。

> `open workload model`: you define the arrival rate of new virtual users; number of concurrent users inside the system is a consequence of the response times and the journey duration and you have no control over it
`closed workload model`: you define the number of concurrent users effectively inside the system; arrival rate is a consequence and you have no control over it

`Open Mode` 可能会导致系统内同时在线的用户或者说并发用户数不可控。 `Close Mode` 设定的就是系统中固定的用户数。

```JAVA
setUp(
  scn.inject(atOnceUsers(1))
).protocols(httpConf)
```

### 逻辑判断
[`Conditional statements`](https://gatling.io/docs/current/general/scenario/#conditional-statements)
#### doIf
```JAVA
doIf("${myBoolean}") {
  // executed if the session value stored in "myBoolean" is true
  exec(http("...").get("..."))
}

```
使用：当 `Session` 中的 `tokenId` 为空时，打印出 `Session`
```JAVA
doIf(session => session("tokenId").asOption[String].isEmpty) {
  exec { session =>
    println("Smoke process - Login", session)
    session
  }
}
```

#### doIfEquals
```JAVA
doIfEquals("${actualValue}", "expectedValue") {
  // executed if the session value stored in "actualValue" is equal to "expectedValue"
  exec(http("...").get("..."))
}
```

#### doIfOrElse
```JAVA
doIfOrElse(session => session("myKey").as[String].startsWith("admin")) {
  // executed if the session value stored in "myKey" starts with "admin"
  exec(http("if true").get("..."))
} {
  // executed if the session value stored in "myKey" does not start with "admin"
  exec(http("if false").get("..."))
}
```


## Gatling 报告分析
### 响应时间分布柱状图
统计请求响应时间分布以及失败请求的数量
![](/images/gatling_requests_response_time_preview.png)

### 各请求响应图表
统计各个API的响应时间，例如：50%，75%，95%，99% 的请求在多少ms内完成。
![](/images/gatling_requests_response_time_statistic.png)

### Active users
在测试期间，各时间点上，活跃的用户数统计
![](/images/gatling_active_users.png)

### 详细响应时间分布
测试过程中，请求的响应时间分布情况
![](/images/gatling_response_time_distribution.png)

### Active users 与 响应时间 对照
`Active users` 和 响应时间 的详细对照
![](/images/gatling_active_users_response_distribution.png)



## 监控工具
在做性能测试的时候，监控是不能少的。

### Sleuth (Spring Cloud Sleuth)
[`Sleuth`](https://spring.io/projects/spring-cloud-sleuth)用来追溯请求在各个服务之间的流转。每个请求有唯一的traceId，在不同的服务之间也会有不同的spanId，这些信息可以帮助查看请求在整个链路中的调用以及耗时情况。

### Zipkin
[`Zipkin`](https://zipkin.io/)和`Sleuth`搭配使用，是将`Sleuth`上报的链路信息可视化。

![](/images/gatling_zipkin_preview.png)

### Prometheus
[`Prometheus`](https://prometheus.io/)用来监控 pod 上的资源使用情况，还能够统计分析 pod 处理的请求。

### Grafana
[`Grafana`](https://grafana.com/)是将`Prometheus`统计的信息可视化。
![](/images/gatling_grafana_preview.png)
