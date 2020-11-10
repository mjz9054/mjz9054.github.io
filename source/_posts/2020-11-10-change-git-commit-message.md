---
title: Change Git Commit Message
date: 2020-11-10 17:39:01
tags:
---

开发过程中时常会遇到提交的 Commit 信息描述不够准确，那么就会遇到修改 Commit 消息的情况。开发过程中有过几次修改 Commit message 的经历，觉得这一块可以记录一下。

<!--more-->
对于 Commit Message 分为两种，一种是尚未提交的，另一种是已经提交的，他们的修改方式不一样，需要分别对待。

### 尚未 Push 的 Commit
尚未提交的Commit message的修改相对简单。
如果是最近的一次提交：
方式一：如果是最近的一次提交，其实可以选择 Revert 相关的 Commit，之后重新填写 Commit message。
方式二：添加`--amend`参数，用于更新最近一次提交的信息
```sh
git commit --amend -m "New commit message."
```
如果是之前的某一次提交：
步骤1：执行`git rebase`命令，选择`reword`
```sh
# Displays a list of the last 3 commits on the current branch
$ git rebase -i HEAD~3
```
步骤2：将`pick`改为`reword`
```
pick 5c5dafff change git commit message 03
pick 0cdde419 change git commit message 02
pick 0cxxxx19 change git commit message 01

# Rebase 6fxxxxx..xxxasafd onto 6f8wdwafsa (2 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup <commit> = like "squash", but discard this commit's log message
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
# .       create a merge commit using the original merge commit's
# .       message (or the oneline, if no original merge commit was
# .       specified). Use -c <commit> to reword the commit message.
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out
```
执行命令后，选择需要修改的message，将`pick`改为`reword`，相关的解释在紧跟着的注释里有。
步骤3：然后保存，命令行会提示输入新的Commit message，之后再保存即可。

### 已 Push 的 Commit
步骤1： 执行`git rebase -i xxx` 命令，和修改未提交的早期Commit message操作一致
```sh
# Displays a list of the last 3 commits on the current branch
$ git rebase -i HEAD~3
```
步骤2：找到对应的Commit，将`pick`修改为`reword`，保存并推出
步骤3：根据提示，输入新的message
步骤4：推送至远端
```sh
git push --force example-branch
```