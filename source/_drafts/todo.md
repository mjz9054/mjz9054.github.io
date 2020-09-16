---
title: todo
date: 2020-09-14 09:27:10
tags:
---

#### Vim
#### Xpath
#### Zipkin
#### Unit test 不同jar包，注解等的不同之处
#### log4j

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


#### MyISAM 与 InnoDB 对 B+ 树的不同使用
MyISAM 和 InnoDB 的索引都是使用 B+ 树的数据结构实现的。
MyISAM 索引和数据是不同的，可以理解为不同类型的数据，而InnoDB的索引也是数据，和具体数据无差。