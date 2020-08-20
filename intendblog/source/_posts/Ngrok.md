---
title: 使用Ngrok进行内网穿透
date: 2020-07-19 22:12:35
comments: false
auto_excerpt: true
toc: true
tags: Ngrok
categories: 
description: 
---
此文仅是本人学习笔记。

**1、什么是Ngrok**

Ngrok 是一个反向代理，通过在公共端点和本地运行的 Web 服务器之间建立一个安全的通道，实现内网主机的服务可以暴露给外网。Ngrok 可捕获和分析所有通道上的流量，便于后期分析和重放，所以 Ngrok可以很方便地协助服务端程序测试。Ngrok希望帮人节省更多的时间去编程。只需一个命令，便可将一个本地服务器暴露在NAT或防火墙后面的互联网。

**2、注册账号**

1、进入网站：http://www.ngrok.cc/
2、点击注册，填写信息
![网站](/images/ngrok1.png)
![注册](/images/ngrok2.png)

**3、开通隧道**

1、进行登录，选择隧道管理—开通隧道--美国Ngrok免费服务器（立即购买）
2、填写信息，点击确定添加，点击确定开通
![进入页面](/images/ngrok3.png)
![开通](/images/ngrok4.png)

**4、下载启动服务器**

1、点击客户端下载，跳转至下载页面，选择自己的对应系统（我的电脑为windows64位）进行下载
2、下载好后，进行解压，打开文件夹：windows_amd64，打开Sunny-Ngrok启动工具
3、在Sunny-Ngrok启动工具，输入隧道id，点击enter键，启动成功，可进行远程访问
![客户端下载](/images/ngrok5.png)
![下载](/images/ngrok6.png)
![输入ID](/images/ngrok7.png)
![启动成功](/images/ngrok8.png)