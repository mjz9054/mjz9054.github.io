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