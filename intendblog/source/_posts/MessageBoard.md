---
title: 启用 Valine 留言系统
date: 2020-08-20 19:38:55
comments: false
auto_excerpt: true
toc: true
tags: hexo
categories: 
description:
---
此文仅是本人学习笔记。

## 问题
博客应用blank主题，主题含有Valine 留言系统，功能提示：Code 401: 未经授权的操作，请检查你的AppId和AppKey.
![img](/images/MessageBoard1.png)

## 解决方法
**创建 LeanCloud 应用**
Valine 基于 LeanCloud 提供的数据服务，参考 Valine 的 [官方教程](https://valine.js.org/quickstart.html)，首先前往 [leancloud.cn](https://leancloud.cn/) 注册账号。
我选择的是华东节点，提交注册信息后LeanCloud提示国区账号必需实名制，否则无法创建应用。
创建了一个应用，命名为 `Valine`，方案选择开发版，即可以在一定的用量限制下免费运行。
![img](/images/MessageBoard2.png)
进入创建好的应用，就能获取到 `App ID` 和 `App Key`。
步骤：
(1)进入刚刚创建的应用，选择左下角的`设置`>`应用``Key`，然后就能看到你的`APP ID`和`APP Key`了。
![img](/images/MessageBoard3.png)
(2)然后，进入 `设置` > `安全中心` > `Web ``安全域名`，填写站点的域名并保存：
![img](/images/MessageBoard4.png)
**配置博客**
编辑 `source/_data/blank.yml`，找到对应的模块，修改配置如下：
```javascript
valine:
    enable: true 
    appid: <App ID>
    appkey: <App Key>
    notify: false 
    verify: false 
    placeholder: <留言编辑框里的默认文本>
    avatar: mm 
    guest_info: nick,mail,link 
    pageSize: 10 
    recordIP: false 
    serverURLs:
    emojiCDN: 
    enableQQ: true
```
再次部署 Hexo 后就能看到留言系统已经启用，可以进行留言了。
![img](/images/MessageBoard5.png)

参考博客：https://laytonsun.com/learning/2019-08/enable-comments.html