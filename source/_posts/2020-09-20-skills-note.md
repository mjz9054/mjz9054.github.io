---
title: skills_note
date: 2020-09-20 18:52:32
tags:
---

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

## Vim

### Vim 键盘图
![](https://www.runoob.com/wp-content/uploads/2015/10/vi-vim-cheat-sheet-sch.gif)

### Command

| 功能 | 命令 | 备注 |
| --- | --- | --- |
| 复制当前行 | yy | 
| 删除当前行 | dd |
| 删除当前行向后n行 | ndd | 包括当前行 | 
| 删除当前行至最后一行 | dG |
| 删除当前行至第一行 | d1G |
| 向前删除一个字符 | X | 类似 backspace |  
| 向后删除一个字符 | x | 类似 del |
| 先后删除n个字符 | nX | 
| 粘贴至当前行的上一行 | P | 
| 粘贴至当前行的下一行 | p | 
| 重复前一个动作 | . | 
| 重做上一个动作 | Ctrl + r |
| 撤销 | u |
| 行首 | 0 | 或者 Home |
| 行尾 | $ | 或者 End | 
| 下一页 | Ctrl + f |
| 上一页 | Ctrl + b |
| 向下半页 | Ctrl + d |
| 向上半页 | Ctrl + u |
| 搜索 | /word | word 为搜索的内容 | 
| 下一个搜索结果 | n |
| 上一个搜索结果 | N |
| 合并当前行和下一行为一行 | J | 
| 保存并退出 | ZZ | 
| 不保存退出 | ZQ |
| 显示行号 | :set nu | 
| 取消显示行号 | :set nonu | 


参考：[Linux vi/vim](https://www.runoob.com/linux/linux-vim.html)

---
## Spring
### Spring `CommandLineRunner` & `ApplicationRunner`

当在 Spring boot 启动后，做一些初始化操作，可以使用`CommandLineRunner`这个接口。
`CommandLineRunner`接口的 Component 会在所有 Beans 都初始化之后，SpringApplication.run() 之前执行。

> Interface used to indicate that a bean should run when it is contained within a SpringApplication. Multiple CommandLineRunner beans can be defined within the same application context and can be ordered using the Ordered interface or Order @Order annotation.

`ApplicationRunner`做的事情和`CommandLineRunner`基本一致，区别在接收的参数的不同，`ApplicationRunner`接收的参数经过了 Spring 的处理，操作起来更简单直观。`--a=b` 形式的参数，可以直接通过使用`getOptionNames()`获取参数名，以及`getOptionValues("xxx")`获取对应的value。而`CommandLineRunner`接收的参数就是原始输出，需要自己去解析。

> If you need access to ApplicationArguments instead of the raw String array consider using ApplicationRunner.

---