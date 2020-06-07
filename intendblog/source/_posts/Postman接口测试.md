---
title: Postman接口测试
date: 2020-06-07 18:28:26
tags: 测试
---

此文仅是本人学习笔记。

# 1、什么是接口

用于处理各个系统各个模块之间的数据。

# 2、接口的组成

|  组成  | 描述  |
|  ----  | ----  |
| URL  | 接口地址 |
| Method   | 接口类型 |
| Code  | 状态码 |
| Headers   | 请求头 |
| Response   | 返回数据 |
| Data   | 接口发送数据 |

# 3、Postman基础用法介绍

## (1)用法

选择接口类型，填写接口地址、请求头，点击send可获取返回数据。

## (2)发送数据的接口

①Get的发送数据
发送的数据之间写在URL，通过“？”间隔数据和地址
参数和参数之间用“&”间隔（也可通过params直接输入）

②Post的发送数据
数据填写到body里面，按照接口文档的内容选择的发送----请求头有写明
方式：form-data、x-www-form-urlencoded、raw、binary（具体可自行百度）
其中row又分为text、js、josn、html、xml

③注意：get和post类型接口的区别和特点
Get：数据直接在URL显示出来
     区别：输入参数长度有限制，所有数据直接显示在URL中可见，不安全。
     特点：一般使用get型的接口，是从数据库中去读取数据、查询比较多。
Post：post和get相反，数据输入于body中
     区别：输入的数据内容、大小没有限制，数据不能直接看到，更安全。
     特点：一般是对数据库写入、修改比较多。

④	Josn的格式：
{“key1”:“value”， “key2”:“value”， “key3”:{ “key”:“value”} }
▪前后用{}包裹起来
▪由key和value组成----key为参数，value为值，中间用“：”隔开
▪所有符号为英文标点符号
▪两个参数用“，”隔开，最后一个不用
▪JOSN格式里可以套用JOSN格式

## (3)状态码的含义

①常见状态码：
200：代表这个借口运行正常
400：接口发送的参数不正确
404：接口地址输入不正确
405：接口类型不正确
500：代表接口的代码有问题，内部服务器错误
②其他状态码：401,402,303,406,408…（可自行百度）

# 4、postman传递token参数，实现接口测试

⑴这里先设置环境变量，系统入口url在每个接口中都一样，设置成环境变量，便于维护。环境变量集名：rds。两个变量：url , token （token是为了下一步准准备）。
⑵新建登录接口请求，设置params(登录接口的账户&密码)。发请求到登录后，获取token。
⑶在Tests里面编写脚本，将获取到的token设置到环境变量token中。 同时Tests里面也可以加断言，判断该接口测试的结果。
⑷登录接口测试完后，查看环境变量，token值已被保存。

# 5、变量

分类：可分为全局变量和局部变量
区别：局部变量要选择变量才能生效
      全局变量不选择也会生效
步骤：
第一步：点击眼睛按钮进入局部变量
第二步：点击Add添加局部变量
第三步：点击输入参数（VARIABLE和CURRENT VALUE）
第四步：点击Add保存参数
第五步：点击切换参数
第六步：将要参数改为变量:替换为｛｛参数名｝｝后，点击send运行，得出结果

# 6、自定义脚本：JavaScript

## (1)脚本的区别：

Pre-request Script：控制发送的数据
Tests：控制返回的结果

## (2)常用代码：

官方说明文档：https://learning.postman.com/docs/postman/scripts/postman-sandbox-api-reference/

常用代码片段：
```javascript
// 获取response返回内容
var rsb = responseBody; // 是字符串格式
var res = JOSN.parse(responseBody);
 
// 获取环境变量
var v = pm.environment.get("变量名称");
 
// 设置环境变量 只能存储字符串，如果是对象的话则无法在下次运行时获取到内容
// 如需要存储JSON数据，可以用JSON.stringify(..)存储，再用JSON.parse(..)转化为对象使用
pm.environment.set("变量名称", 变量内容);
 
// 清除某个环境变量
pm.environment.unset("环境变量名");
 
// 获取全局变量和普通变量
var gb = pm.globals.get("全局变量名");
var nm = pm.variables.get("普通变量名");
 
// Javascript 获取变量类型
console.log( typeof pm.enviroment );
```
# 7、断言：自动判断是否成功

官方说明文档：https://learning.getpostman.com/docs/postman/scripts/test_examples/
断言语句参考：https://www.cnblogs.com/liruxian/p/10001539.html

举例说明：解析响应正文，并判断statusCode的值是200，message的值是”Success”
操作：我们需要解析JSON串了，所以，在SNIPPETS中找到”Response body:JSON value check”并点击，在其左边，断言代码自动添加，对代码进行修改：
```javascript
pm.expect(jsonData.value).to.eql(200);    //判断statusCode的值是200
pm.expect(jsonData.value).to.eql('Success');    //判断message的值是”Success”
```
点击Send，发送请求，PASS表示断言通过，FAIL表示断言失败。

