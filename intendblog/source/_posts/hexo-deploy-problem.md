---
title: hexo发生error：spawn failed错误的解决方法
date: 2020-07-19 23:29:13
comments: false
auto_excerpt: true
toc: true
tags: hexo
categories: 
description:
---
此文仅是本人学习笔记。

**问题描述：**

部署博客是出现出现错误：
Error: Spawn failed
at ChildProcess.<anonymous> (D:\Develop\VSCode-workspace\intendblog\node_modules\_hexo-util@1.9.1@hexo-util\lib\spawn.js:51:21)
at ChildProcess.emit (events.js:310:20)
at ChildProcess.cp.emit (D:\Develop\VSCode-workspace\intendblog\node_modules\_cross-spawn@7.0.3@cross-spawn\lib\enoent.js:34:29)
at Process.ChildProcess._handle.onexit (internal/child_process.js:275:12) 

**解决办法：**

1.	删除.deploy_git文件夹;
2.	然后，依次执行：
```javascript
hexo clean
hexo g
hexo d
```
