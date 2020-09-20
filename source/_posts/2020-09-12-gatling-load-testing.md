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


## Gatling 报告分析
### 响应时间分布柱状图
### 各请求响应图表
### active users
### 详细响应时间分布


## 监控工具
### sleuth
### zipkin
### Prometheus
