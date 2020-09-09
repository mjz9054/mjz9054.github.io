---
title: Blog supported by Hexo
date: 2020-09-07 23:04:55
tags: [Hexo, maupassant]
---

本文是在 Mac 系统下，搭建 Hexo 支持的博客系统，事先需要安装好`Ruby`和`npm`相关依赖。

## 1. 安装 `hexo`, 并初始化项目
### 假设项目名称为`blog`
```shell
npm install hexo-cli -g
hexo init blog 
cd blog
npm install
hexo server
```
>  [Hexo commands](https://hexo.io/docs/commands)



## 2. 安装主题
主题以[`maupassant`](https://github.com/tufu9441/maupassant-hexo)为例进行安装
### 步骤1：下载并安装主题
```shell
$ cd blog
$ git clone https://github.com/tufu9441/maupassant-hexo.git themes/maupassant
$ npm install hexo-renderer-pug --save
$ npm install hexo-renderer-sass --save
```

### 步骤2：应用主题至项目
在项目的 `_config.yml` 中，修改 `theme: landscape` 为 `theme: maupassant`, 保存后 `hexo server` 运行，查看效果

> self_search - A jQuery-based local search engine, with the dependency on the plugin hexo-generator-search


## 3. 主题自定义

### 3.1 禁用部分页面，目前还未添加相应的页面，可以先禁用
理论上，应用完主题之后就可以正常访问博客了，但由于部分页面未提供，这里先注释这一部分

```YAML
# - page: about
#   directory: about/
#   icon: fa-user
# - page: rss
#   directory: atom.xml≥
#   icon: fa-rss
```

### 3.2 开启 `self_search`
`self_search`的功能需要`hexo-generator-search`插件的帮助。开启后，可以通过关键词搜索到文章。
#### 步骤1：安装 [`hexo-generator-search`](https://github.com/wzpan/hexo-generator-search) 插件
```sh
$ npm install hexo-generator-search --save
```

#### 步骤2： Options configuration in `_config.yml` file

```yml
search:
    path: search.xml
    field: post
    content: true
```

#### 步骤3： 启用 `self_search`
修改`maupassant`主题目录下的`_config.yml`, 修改`self_search: true`

 

## 4. 写文章
### 4.1 新建文章
#### 方式1. 手动在 `source/_post` 目录项创建 `Markdown` 文件
#### 方式2. 使用命令创建，无需指定文件类型
```sh
$ hexo new xxx 
```
默认将新建的文件放置在`_post` 目录下，可以通过修改`default_layout` in `_config_yml` 指向其他目录，或者手动指定
```sh
$ hexo new draft xxx 
```
这样，新建的文件就会放置在`draft`目录下，且不用关心该目录是否存在

### 4.2 多标签设置
在文章的顶部区域，配置 `tags: [tag1, tag2]` 即可。例如：
```markdown
---
title: Blog supported by Hexo
date: 2020-09-07 23:04:55
tags: [Hexo, maupassant]
---
```

### 4.3 图片引用
#### 4.3.1 来自网络
填写图片链接，直接引用 `![](url)`

#### 4.3.2 来自本地
可以在`source`目录下创建 images 目录，用于存放文章所需图片，然后在文章里引用: 
```sh
![](/images/image.jpg)
```

除了将图片放在`source`, 还可以将图片放置在文章所在目录，例如`_post`, 修改
```sh
post_asset_folder: true
```
这样在创建通过命令`hexo new blog_name`时，会在`_post`目录下生成`blog_name.md`和`blog_name`文件夹，可以将图片放置在`blog_name` 目录下。
当然，手动创建该文件夹也可以。


## 5. 文章发布

#### 步骤1： 修改项目配置文件`_config.yml`，配置上自己GitHub的地址
```YMAL
deploy:
  type: git
  repository: git@github.com:mjz9054/mjz9054.github.io.git
  branch: master
```
`repository`可以配置`https`，也可以配置`ssh`的地址

#### 步骤2： 安装 hexo-deployer-git 插件
自动部署需要`hexo-deployer-git`插件的帮助，否则不能自动找到`Git`
```sh
$ npm i hexo-deployer-git
```
相关命令：
发布文章至GitHub
```sh
hexo deploy # 或简写 hexo d
```
本地预览
```sh
hexo server # 或简写 hexo s 
```
执行命令后，可以访问 [localhost:4000](localhost:4000)，进行预览


## 6. 源文件管理

#### Git 配置
```sh
$ git init 
$ git remote add origin git@github.com:mjz9054/mjz9054.github.io.git
$ git remote -v
origin	git@github.com:mjz9054/mjz9054.github.io.git (fetch)
origin	git@github.com:mjz9054/mjz9054.github.io.git (push)
```

#### 创建分支
将源文件放置在分支上，`master`用于静态文件的存放.
分支`gh-pages`是 GitHub pages 的 tutorial 中提到的存放源文件的分支名，可以使用这个名字也可以不使用，自己能明白新建分支的意义即可。
```sh
$ git checkout --orphan gh-pages
```

#### 将文件推送至分支
```sh
$ git push --set-upstream origin gh-pages
```
需要在远端创建分支，需要加上额外参数，之后的推送就不需要了。

## 7. 其他
### Hexo tag plugin
> https://hexo.io/docs/tag-plugins.html

#### Examples
- codeblock

{% codeblock lang:javascript %}
    var v = "Hello World"
    alert("Hello World")
{% endcodeblock%}

- youtube
{% youtube lJIrF4YjHfQ %}

