---
title: Charles Capture
date: 2020-10-03 09:45:49
tags: [Charles, Capture]
---

在进行 App 的开发过程中，时常需要通过抓包来帮助定位问题。通过抓包，可以了解到请求体，响应体，header， 耗时等等信息。这里记录下用 Charles 抓取 App 数据的过程。

<!--more--> 

### Charles 下载及安装

`Charles` [下载地址](https://www.charlesproxy.com/latest-release/download.do)，可以更加操作系统下载对应的版本。

下载完成之后，根据提示安装即可。

### Proxy 设置

设置 Charles 为代理服务器后，通过抓取到流经代理服务器的数据，来分析相应的请求。

启动 Charles 后，在 `Proxy` -> `Proxy Setting` 里设置代理服务器的参数，例如：端口号，默认不需要进行过多的设置。

在 Proxy Setting 也可以直接开启 `Mac OS Proxy`。开启之后，就可以抓取本机上的网络请求。

### 抓取 App 网络请求

首先在 `Charles` -> `Help` -> `Local Address` 查看代理服务器的地址；

然后在手机端的网络里设置代理服务器地址及端口号，地址可以从`Local Address`里找到，端口号可以从 `Proxy Setting`里找到，默认为 8888 。

### 抓取 HTTPS 网络请求

经过以上设置只有，可以抓取到电脑或者手机端的网络请求。不过有些请求是HTTPS加密的，这就需要在电脑或者手机上安装证书以及在 Charles 开启 `SSL Proxying`。

以手机端为例安装证书

在手机端浏览器(Safari)打开[chls.pro/ssl](chls.pro/ssl)，根据提示下载安装证书；

下载完成之后，证书会显示在`描述文件`里， 点击安装证书；

安装之后，需要在 `通用`-> `关于本机` -> `证书信任设置` 里信任证书。

不同版本的 iOS 可能略有不同，仅供参考。

### 开启 SSL Proxying

手机端安装完成证书之后，还需要在 Charles 里开启 `SSL Proxying`。

在 `Proxy` -> `SSL Proxy Setting` 里 添加需要 SSL 代理的站点，点击保存即可。


### 使用

经过以上设置之后，就可以在 Charles 里解析到 HTTPS 的请求及响应。

参考：[史上最强 Charles 抓包](https://juejin.im/post/6844903640272994317#heading-3)
