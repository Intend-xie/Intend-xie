---
title: hexo个人博客添加鼠标点击效果
date: 2020-08-21 11:50:06
comments: false
auto_excerpt: true
toc: true
tags: hexo
categories: 
description:
---
此文仅是本人学习笔记。

## 安装模型
```javascript
npm install live2d-widget-model-hijiki
```
## 配置：hexo博客的根目录下的配置文件_blank.yml，在最后添加以下代码
```javascript
live2d:
  enable: true
  scriptFrom: local
  model:
    use: live2d-widget-model-hijiki
  display:
    position: right
    width: 150
    height: 300
  mobile:
    show: true
```
## 在Hexo博客下找到自己使用的主题在文件夹source下新建love.js，love.js文件内容如下：
!function(e,t,a){function n(){c(".heart{width: 10px;height: 10px;position: fixed;background: #f00;transform: rotate(45deg);-webkit-transform: rotate(45deg);-moz-transform: rotate(45deg);}.heart:after,.heart:before{content: '';width: inherit;height: inherit;background: inherit;border-radius: 50%;-webkit-border-radius: 500%;-moz-border-radius: 50%;position: fixed;}.heart:after{top: -5px;}.heart:before{left: -5px;}"),o(),r()}function r(){for(var e=0;e<d.length;e++)d[e].alpha<=0?(t.body.removeChild(d[e].el),d.splice(e,1)):(d[e].y--,d[e].scale+=.004,d[e].alpha-=.013,d[e].el.style.cssText="left:"+d[e].x+"px;top:"+d[e].y+"px;opacity:"+d[e].alpha+";transform:scale("+d[e].scale+","+d[e].scale+") rotate(45deg);background:"+d[e].color+";z-index:99999");requestAnimationFrame(r)}function o(){var t="function"==typeof e.onclick&&e.onclick;e.onclick=function(e){t&&t(),i(e)}}function i(e){var a=t.createElement("div");a.className="heart",d.push({el:a,x:e.clientX-5,y:e.clientY-5,scale:1,alpha:1,color:s()}),t.body.appendChild(a)}function c(e){var a=t.createElement("style");a.type="text/css";try{a.appendChild(t.createTextNode(e))}catch(t){a.styleSheet.cssText=e}t.getElementsByTagName("head")[0].appendChild(a)}function s(){return"rgb("+~~(255*Math.random())+","+~~(255*Math.random())+","+~~(255*Math.random())+")"}var d=[];e.requestAnimationFrame=function(){return e.requestAnimationFrame||e.webkitRequestAnimationFrame||e.mozRequestAnimationFrame||e.oRequestAnimationFrame||e.msRequestAnimationFrame||function(e){setTimeout(e,1e3/60)}}(),n()}(window,document);
## 在主题文件夹下的layout文件夹下的_layout.ejs（我自己的是layout.ejs文件）配置文件里面的<head></head>标签里添加
```javascript
<script type="text/javascript" src="/love.js"></script>
```
参考博客：https://www.cnblogs.com/songsongblue/p/10911387.html