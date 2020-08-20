---
title: 博客地址拒绝我的访问
date: 2020-08-04 10:33:36
comments: false
auto_excerpt: true
toc: true
tags: hexo
categories: 
description:
---
此文仅是本人学习笔记。

## 问题：我的博客（https://intend-xie.github.io/）被拒绝访问

您的连接不是私密连接
攻击者可能会试图从 **intend-xie.github.io** 窃取您的信息（例如：密码、通讯内容或信用卡信息）。了解详情
NET::ERR_CERT_AUTHORITY_INVALID
![问题](/images/GitHub-rejects-connection-request1.png)

## 解决方法
1、在cmd中，ping intend-xie.github.io,得到IP
![步骤1](/images/GitHub-rejects-connection-request2.png)
2、将其ip和域名添加到hosts文件（目录：C:\Windows\System32\drivers\etc）中
![步骤2-1](/images/GitHub-rejects-connection-request3.png)
![步骤2-2](/images/GitHub-rejects-connection-request4.png)
3、	如果还不行，可通过打开Dns检测|Dns查询 - 站长工具：http://tool.chinaz.com/dns
4、在检测输入栏中输入博客地址（intend-xie.github.io）
![步骤3、4](/images/GitHub-rejects-connection-request5.png)
5、把检测列表里某个IP（对应TTL值最小和最大的IP我尝试了都可以，其他有兴趣可以试试）输入到hosts里，并对应写上博客地址
![步骤5](/images/GitHub-rejects-connection-request6.png)
6、问题的思路
通过下面两个链接进行了解解决，具体可进行查看：
https://www.jianshu.com/p/5b72495f4548
https://segmentfault.com/q/1010000010264567