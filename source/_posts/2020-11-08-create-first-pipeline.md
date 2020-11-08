---
title: Create First Pipeline
date: 2020-11-08 11:51:43
tags:
---

当搭建好了 Jenkins 后，就可以借助它来实现自己的 Pipeline。

<!--more-->
简要步骤罗列
1. 需要创建一个 Java 的 project，Kotlin的也是可以的
2. 在 Project 中创建Jenkinsfile，编写 Pipeline 的相关脚本
3. 在 Jenkins 上创建 Job

### 创建项目
#### New Project
本次创建的是一个 gradle 的项目，首先选择`Spring Initlizar`，此时可以设定java的版本。

![](/images/jenkins/first_pipeline/jenkins_first_pipeline_create_project_step01.png)

*这里需要注意和Jenkins里保持一致。由于本机安装的是Java11，Jenkins上安装的是Java8，这里仍然可以选择Java11，可以再项目创建完成之后修改项目编译的目标版本*

#### 项目类型选择 Gradle
填写项目的基本信息，以及*选择`Type`为`Gradle Project`*
![](/images/jenkins/first_pipeline/jenkins_first_pipeline_create_project_step02.png)

#### 所需组件
选择所需的组件。这里仅做实验，并未勾选其他的组件。
![](/images/jenkins/first_pipeline/jenkins_first_pipeline_create_project_step03.png)

#### 项目基本信息
填写项目存储位置
![](/images/jenkins/first_pipeline/jenkins_first_pipeline_create_project_step04.png)

#### 修改项目兼容Java版本
在`build.gradle`中，将sourceCompatibility的值由`11`改为`1.8`。
```
sourceCompatibility = '1.8'
```
原因是因为实验所用的Jenkins上关联的Java版本的1.8，如果这里采用11，会导致构建失败。
当然，也可以通过升级Jenkins上的Java版本来规避这个问题。

### Jenkinsfile
在项目的根目录下创建名为`Jenkinsfile`的文件，并填写脚本内容。
```Groovy
pipeline {
    agent any
    stages {
        stage("Test") {
            steps {
                script {
                    echo 'Running Unit Test...'
                    sh './gradlew test --info'
                }
            }
        }
    }
}
```

### Git
由于需要把项目管理起来，所以需要将本地的项目和Git关联起来。
可以首先在提供代码托管的站点，例如：Github，Gitee，创建自己的repository。
创建完成之后，将本地Project和远端管理起来
```sh
cd demo
git init # 初始化
git add . # 添加文件
git commit -m "commit message" # 填写commit信息
git remote add origin git@gitee.com:[your_username]/[your_repository_name].git
git push -u origin master # 推送至远端 
```

### Jenkins Credential
建立Jenkins到指定repository之间的访问，需要提供相应的 Credential。
可以使用用户名和密码的方式，也可以使用SSH的方式。
![](/images/jenkins/first_pipeline/jenkins_first_pipeline_manage_credential.png)

使用`ssh-keygen`生成一对公钥和私钥
```sh
ssh-keygen -t rsa 
```
如果本机已有秘钥对，那么在重新生成的时候可以指定新生成的秘钥对的名称，防止覆盖本机的秘钥对

将公钥添加至Gitee

将私钥保存在Jenkins的Credential中

*使用完成后，新生成的秘钥对就可以从本机删除了，并无其他用处了*

### Pipeline
New Item
![](/images/jenkins/first_pipeline/jenkins_first_pipeline_new_item.png)

输入Pipeline名字，并选择Pipeline的类型
![](/images/jenkins/first_pipeline/jenkins_first_pipeline_typing_pipeline_name.png)

Definition
选择远端的repository地址，并指定对应的credential
![](/images/jenkins/first_pipeline/jenkins_first_pipeline_definition_pipeline.png)

Build Now
![](/images/jenkins/first_pipeline/jenkins_first_pipeline_build_now.png)

Build Successfully
![](/images/jenkins/first_pipeline/jenkins_first_pipeline_build_successfully.png)

