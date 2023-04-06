---
title: Spy-debugger 移动端抓包调试工具的安装与使用
date: 2023-04-06 09:45:47
updated: 2023-04-06 09:45:47
tags: 接口
category: 软件测试
description: 介绍一个适用于移动端的抓包工具
sticky: 1
---

### 前言：

spy-debugger 是一个一站式页面调试、抓包工具。远程调试任何手机浏览器页面，任何手机移动端webview（如：微信，HybridApp等）。支持HTTP/HTTPS，无需USB连接设备。

## 一、特性：
```
1. 页面调试＋抓包
2. 操作简单，无需USB连接设备
3. 支持HTTPS。
4. spy-debugger内部集成了weinre、node-mitmproxy、AnyProxy。
5. 自动忽略原生App发起的https请求，只拦截webview发起的https请求。对使用了SSL
6. pinning技术的原生App不造成任何影响。
7. 可以配合其它代理工具一起使用(默认使用AnyProxy) (设置外部代理)
```

## 二、安装及配置:
### 第一步：安装spy-debugger
```shell
npm  install  -g   spy-debugger
```
输入之后会要求输入密码，确认后即可安装
![安装spy-debugger](https://k1ngr4m-github-1309147067.cos.ap-shanghai.myqcloud.com/img/test/%E5%AE%89%E8%A3%85spy-debugger.png)

### 第二步：连接Wi-Fi
手机和PC保持在同一网络下（比如同时连到一个Wi-Fi下）

### 第三步：设置代理
设置手机的HTTP代理，代理IP地址设置为PC的IP地址，端口为spy-debugger的启动端口(默认端口：9888)。

查看pc的ip地址：

mac：
![](https://k1ngr4m-github-1309147067.cos.ap-shanghai.myqcloud.com/img/test/mac%E6%9F%A5%E7%9C%8Bip01.png)
![](https://k1ngr4m-github-1309147067.cos.ap-shanghai.myqcloud.com/img/test/mac%E6%9F%A5%E7%9C%8Bip02.png)

- Android设置代理步骤：设置 - WLAN - 长按选中网络 - 修改网络 - 高级 - 代理设置 - 手动
- iOS设置代理步骤：设置 - 无线局域网 - 选中网络 - HTTP代理手动

### 第四步：启动
命令行输入
```shell
spy-debugger
```
按命令行提示用浏览器打开相应地址。

![启动spy-debugger](https://k1ngr4m-github-1309147067.cos.ap-shanghai.myqcloud.com/img/test/%E5%90%AF%E5%8A%A8spy-dubugger.png)

### 第五步：安装证书
安装证书，手机必须先设置完代理后再通过(非微信)手机浏览器访问以下链接：

http://spydebugger.com/cert 安装证书（手机首次调试需要安装证书，已安装了证书的手机无需重复安装)。

### 第六步：访问页面
用手机浏览器访问你要调试的页面即可。

![](https://k1ngr4m-github-1309147067.cos.ap-shanghai.myqcloud.com/img/test/spy-debugger%E9%A1%B5%E9%9D%A2%E8%B0%83%E8%AF%95%E7%95%8C%E9%9D%A2.png)

![](https://k1ngr4m-github-1309147067.cos.ap-shanghai.myqcloud.com/img/test/spy-debugger%E8%AF%B7%E6%B1%82%E6%8A%93%E5%8C%85%E7%95%8C%E9%9D%A2.png)

## 三、自定义选项
1. 端口
   (默认端口：9888)
```shell
spy-debugger -p 8888
```

2. 设置外部代理（默认使用AnyProxy）
```shell
spy-debugger -e http://127.0.0.1:8888
```

3. 是否允许weinre监控iframe加载的页面（默认： false）
```shell
spy-debugger  -i true
```

4. 设置页面内容为可编辑模式(默认： false)
```shell
spy-debugger -w true
```

5. 是否只拦截浏览器发起的https请求（默认： true）
```shell
spy-debugger -b false
```

有些浏览器发出的connect请求没有正确的携带userAgent，这个判断有时候会出错，如UC浏览器。这个时候需要设置为false。大多数情况建议启用默认配置：true，由于目前大量App应用自身（非WebView）发出的请求会使用到SSL pinning技术，自定义的证书将不能通过app的证书校验。

6. 是否允许HTTP缓存 (默认： false)
```shell
spy-debugger -c true
```

工具地址: https://github.com/wuchangming/spy-debugger.git