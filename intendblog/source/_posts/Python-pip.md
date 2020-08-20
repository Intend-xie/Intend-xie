---
title: CMD命令模式使用pip提示Did not provide a command
date: 2020-06-21 17:59:51
comments: false
auto_excerpt: true
toc: true
tags: Python
categories: 
description: 
---
此文仅是本人学习笔记。

问题：python安装后pip用不了，但是cmd命令窗口提示：Did not provide a command
![问题](/images/Python-pip1.png)
首先，使用where pip找到pip的安装目录，我的目录为第三个，D:\Python\Python38\Scripts\pip.exe
![pip目录](/images/Python-pip2.png)
其次，配置环境变量
打开环境变量配置窗口：此电脑--》属性--》左上侧的高级系统设置--》高级--》环境变量
在之前的环境变量Path最后添加，如果最后已经有英文的“;”分号，则不需要添加分号了，直接添加你的目录。如果没有则在后面添加英文分号“;”和你的pip目录，我的为“D:\Python\Python38\Scripts\”，添加完成之后，最好是在内容的最后面直接添加一个英文的“;”，习惯问题，方便下次配置其他环境变量时忘记添加而造成不能使用。
![修改环境变量](/images/Python-pip3.png)
因此每次使用pip命令安装东西的时候都需要先进入到pip所在目录去执行pip install。----这样的操作比较麻烦。
因此我在使用pip命令的时候做了区分，我直接使用pip3(因为我的版本是3.0的)，发现环境变量配置的确实没有问题，原来使用pip3来执行装就可以了
![区分pip](/images/Python-pip4.png)
所以在安装的时候使用pip3 install 来进行安装就可以了。
注意：如果您的版本是pip2，那么就用pip2 install来安装就可以了。