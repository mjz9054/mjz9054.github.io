---
title: Install Jenkins on Docker
date: 2020-11-01 09:55:42
tags: [Jenkins, Docker]
---

实际上一直对持续继承不熟悉，经历了几个项目都是需要自己去设定Jenkins之后，觉得有必要去熟悉熟悉这方面的东西。

<!--more-->

在之前的开发过程中，持续集成是固定不变的，经历的项目都只需要关注功能的开发就好，后面的各种check都是安排好的，也就是说持续集成已经完善且几乎是不变的，甚至说在公司内部是通用的配置。在现在的公司里，经历都是客户的项目，每个客户都需要自己的持续集成，相互之间的环境以及需求都可能存在差异，那么这一套的搭建或者定制化，也就需要开发或者运维人员来完成，后续开发工程中还可能会有不断的改进和完善。

#### 获取镜像
```sh
    docker pull docker pull jenkins/jenkins:lts
```
这一步从 docker 的镜像仓库里获取长期支持的`lts` Jenkins 镜像，如果不指定，例如`jenkins/jenkins`则默认是去获取每周最新的镜像，也即当前最新的镜像。
在 Docker 网站上关于 Jenkin 的介绍里说，建议去 Jenkins 社区下载镜像，因为 Docker 里提供的镜像在`LTS 2.60.x`之后不会在进行更新，需要用户做出合适的选择。
而作为练习使用，对最新的版本并没有特别的需求，这里就直接从Docker上获取镜像

#### 安装
```sh
    docker run -p 8080:8080 -p 50000:50000 jenkins/jenkins
```
这个命令没有指定 Volume，那么和 Jenkins 相关的数据都会存储在容器里，不能够持久化。推荐进行持久化配置，可以将 Volume 映射到主机的文件系统上。

```sh
    docker run -p 8080:8080 -p 50000:50000 -v /var/jenkins_home:/var/jenkins_home jenkins/jenkins
```
指定主机上的`/var/jenkins_home`和虚拟机上的`/var/jenkins_home`目录进行映射，这样 Jenkins 的相关数据就可以做到持久化。
需要确保主机上的`/var/jenkins_home`目录能够被 Jenkins 用户访问。

注意： docker run 的时候是 `jenkins/jenkins`, 单写的 `jenkins` 所对应的镜像是一个废弃的镜像，会出现插件安装失败（提示需要更新值新版本Jenkins的问题）。

##### 主机上创建目录
```sh
    mkdir -p /var/jenkins_home
```
##### 修改目录权限
```sh
    chmod -R 1000 /var/jenkins_home
```
Mac 上可能还需要设置`File Sharing`。

#### 访问
跳过 Volume 的配置，执行完`docker run`命令之后，Jenkins 应该就 run 起来了。 在浏览器访问http://localhost:8080 就可以访问 Jenkins 了。

![](/images/jenkins/jenkins_install_localhost_8080.png)

此时，可以在执行 docker run 命令后的 Jenkins 启动日志里找到密码。
也可以连接bash至container，查看对应的密码文件
```sh
    docker exec -it [container_id] bash
```
连上之后，查看初始管理员密码
```sh
    cat /var/jenkins_home/secrets/initialAdminPassword
```

##### 安装插件
这里可以选择安装推荐插件，也可以后期按需安装
![](/images/jenkins/jenkins_install_suggest_plugins.png)

##### 创建管理员账号
![](/images/jenkins/jenkins_create_admin_user.png)

##### 准备完成
![](/images/jenkins/jenkins_ready.png)

##### 设置完成
![](/images/jenkins/jenkins_welcome.png)