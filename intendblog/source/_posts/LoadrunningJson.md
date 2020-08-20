---
title: Loadrunning的web_custom_request函数
date: 2020-08-01 21:36:55
comments: false
auto_excerpt: true
toc: true
tags: Loadrunning
categories: 
description:
---
此文仅是本人学习笔记。

## 问题：loadrunning怎么请求json参数：
request payload
{"pageNo":1,"perPageSize":10,"type":"c","companyId":"CF9111CB233F46C290F662E0FAFA3F25","year":2020}
应该怎么请求？
用web_submit_data()函数，在回放脚本时，发现返回的数据总数返回上一接口的返回数据。
![问题](/images/LoadrunningJson1.png)

## 如何解决：
### 1、什么是request payload
Request Payload更准确的说是http request的payload body。一般用在数据通过POST请求或者PUT请求。它是HTTP请求中空行的后面那部分。（PS:这里涉及一个http常被问到的问题，http请求由哪几部分组成，一般是请求行，请求头，空行，请求体。payload body应该是对应请求体。）
这种请求 Content-Type 为 application/json，浏览器会认为这是复杂请求，先执行一次 OPTIONS 请求判断是否合法，如果服务器没有给出正确的回应，浏览器会在控制台报错：跨域请求。
具体可进入链接了解：https://segmentfault.com/a/1190000018774494
### 2、web_custom_request函数介绍
LoadRunner提供的web_custom_request函数可以用于实现参数的动态生成。在LoadRunner中，web_reg_save_param和custom_request都常于处理参数的动态生成。
web_reg_save_param函数是大家都已经熟悉的了，它的主要作用是从一个response中获得后续的request需要使用的数据，然后将其作为一个参数保存下来，供后续步骤使用。该方法在LoadRunner中被称为Correlation（关联）。
而web_custom_request函数则可以用于完全自定义向服务端发送的request。
web_custom_request方法的原型是：
int web_custom_request (const char *RequestName, <List of Attributes>,[EXTRARES, <List of Resource Attributes>,] LAST );
其中List of Attributes的主要项目是Method，URL和BODY等。
### 3、LoadRunner中web_custom_request 和 web_submit_data的差别
(1)实现的功能不同
web_submit_data只能发送POST类型的请求。
web_custom_request方法可以发送POST和GET类型的请求。
(2)请求数据提交方式不同
web_submit_data以"Name=属性名称,","Value=属性值" 方式提交数据。
web_custom_request以"Body=属性名称=属性值&属性名称=属性值"方式提交数据。
(3)上下文依赖不同
web_submit_data不依赖上下文，不管是否打开模块的链接页面，就直接向服务器发送post请求。
web_custom_request：会依赖上下文，即如果前面的页面打开失败或没有打开，则该操作就会失败，如：登陆一个论坛成功后，点击某个板块，然后发帖(写入帖子题目和内容，提交，相当于向服务器发送了一个post请求)，如果点击某个模块后打开链接页面失败，则web_custom_request就会失败，即依赖于板块的链接页面是否成功打开，如果没有打开，就不能进行后面的发帖了。
### 4、为什么选择web_custom_request函数自定义请求
web_custom_request函数自定义请求，所有web_submit_data方法发送的请求都可以使用web_custom_request来实现，web_custom_request可以实现web_submit_data无法实现的请求。
如：
"Name=pageNo", "Value=1", ENDITEM,
"Name=pdVersionId", "Value=\"2001\"", ENDITEM,
"Name=perPageSize", "Value=30", ENDITEM,
"Name=projectType", "Value=\"3\"", ENDITEM,
"Name=year", "Value=\"2020\"", ENDITEM,
如果我们想提交的某个属性包含包含多个值，它就无法处理了，只能通过多个web_submit_data来处理。
### 5、了解web_custom_request的参数
URL -  统一资源定位器，通常为请求链接地址
Method -  请求方法：POST、GET
TargetFrame -  包含当前链接或资源的frame的名称
EncType -  提交请求使用的编码类型(type of encoding)。EncType指定“Content-Type”请求头的值，比如“text/html”。web_custom_request不处理未编码的请求体。Body参数指定的请求体会使用指定的编码。
RecContentType -  指定了Content–Type  响应头的类型，比如text/html,application/x-javascript。当没有设置Resource属性时，用它来确定目标URL是否是可录制的资源。
Refer -  指定引用的页面
Body -  请求体
Mode - 录制级别：HTML、HTTP
可通过下方链接了解，这里就不具体描述，只描述我用到的。
https://blog.csdn.net/huilan_same/article/details/51603855?utm_medium=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.channel_param&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.channel_param
### 6、解决代码
代码如下：
web_custom_request(“getProjectList",
“URL=http://19.111.49.70/cacz/project/businessexpenditure/specialproject/specialprojectlist/getProjectList",
"Method=POST",
"RecContentType=application/json",
"EncType=application/json",
"Mode=HTML",
"Body={\"pageNo\":1,\"perPageSize\":10,\"type\":\"c\",\"companyId\":\"CF9111CB233F46C290F662E0FAFA3F25\",\"year\":2020},
LAST);


