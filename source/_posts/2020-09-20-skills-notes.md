---
title: Skills Notes
date: 2020-09-20 18:52:32
tags: [Git, Vim, Spring]
---

这里主要用来记录一下开发过程中学习到的零散知识点或者是软件的使用技巧。先将点放在这里做草稿，等同一类型收集到一定程度，或者要对某一部分做整理时，再转移到其他更合适的位置。目前有`Git`，`Vim`，`Spring`的一些点。

## Git

### git 切换分支
#### 在建立本地分支，指定所对应的远程分支
```sh
$ git checkout -b dev origin/dev
```

#### 在本地建立分支，以当前所在分支为基础(如果不指定远程分支)
```sh
$ git checkout -b dev
```

#### 查看 project 有多少个分支
```sh
$ git branch -a // --all 本地和远程的所有分支
$ git branch -r // --remote 远程的所有分支
$ git branch -l // --list 本地所有分支
$ git branch -v // --verbose 本地分支（输出最后一次提交信息）
```
---

## Spring
### Spring `CommandLineRunner` & `ApplicationRunner`

当在 Spring boot 启动后，做一些初始化操作，可以使用`CommandLineRunner`这个接口。
`CommandLineRunner`接口的 Component 会在所有 Beans 都初始化之后，SpringApplication.run() 之前执行。

> Interface used to indicate that a bean should run when it is contained within a SpringApplication. Multiple CommandLineRunner beans can be defined within the same application context and can be ordered using the Ordered interface or Order @Order annotation.

`ApplicationRunner`做的事情和`CommandLineRunner`基本一致，区别在接收的参数的不同，`ApplicationRunner`接收的参数经过了 Spring 的处理，操作起来更简单直观。`--a=b` 形式的参数，可以直接通过使用`getOptionNames()`获取参数名，以及`getOptionValues("xxx")`获取对应的value。而`CommandLineRunner`接收的参数就是原始输出，需要自己去解析。

> If you need access to ApplicationArguments instead of the raw String array consider using ApplicationRunner.

---