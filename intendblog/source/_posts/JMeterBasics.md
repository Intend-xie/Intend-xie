---
title: JMeter入门基础
date: 2020-08-17 11:12:23
tags: JMeter
---
此文仅是本人学习笔记。

## 一、jmeter介绍
1、 什么是jmeter
Apache JMeter是Apache组织开发的基于Java的压力测试工具。
2、 Jmeter可以做什么
(1) 接口测试----基础
(2) 性能测试
(3) 压力测试
(4) 数据库测试
(5) Java程序测试
3、 Jmeter优缺点
优点：
(1) 开源免费
(2) 支持多协议
(3) 轻量级
(4) 功能强大
缺点：
使用jmeter无法验证js程序，也无法验证页面UI，所以要需要和selenium配合来完成web2.0应用测试
## 二、jmeter安装
1、JMeter的下载与配置
下载地址：http://jmeter.apache.org/ 
按照下图进行下载
![img](/images/JMeterBasics1.png)
![img](/images/JMeterBasics2.png)
下载完成后，解压，目录结构如下
![img](/images/JMeterBasics3.png)
修改中文：进入bin目录，找到JMeter.bat文件，右键编辑文件，并修改如信息
``` bash
set JMETER_LANGUAGE=-Duser.language="**zh**" -Duser.region="**CN**"
```
![img](/images/JMeterBasics4.png)
到这保存退出就可以通过JMeter.bat运行JMeter了，但因为后续的测试可能会使用到一些拓展的插件，所以还需要导入jmeter-plugins-manager。
2、plugins-manager下载与安装
jmeter-plugins-manager下载地址：https://jmeter-plugins.org/install/Install/
![img](/images/JMeterBasics5.png)
下载完成后将jar包放入lib/ext
![img](/images/JMeterBasics6.png)
完成后即可启动jmeter
3、Jmeter启动与插件安装
执行jmeter.bat文件，弹出的控制台不可关闭。启动后如下：
注意：在linux系统需执行jmeter.sh文件
![img](/images/JMeterBasics7.png)
点击选项->plugins manager
![img](/images/JMeterBasics8.png)
Installed Plugins 为已安装的插件，Available Plugins 为可安装的插件 ，Upgrades为可更新的插件
勾选插件后，点击右下角的Apply Changes and Restart JMeter，安装后会自动重启JMeter，这里推荐安装3 Basic Graphs 和 jpgc - Standard Set
![img](/images/JMeterBasics9.png)
4、Badboy的下载
下载地址：http://www.badboy.com.au/
点击Download
![img](/images/JMeterBasics10.png)
选择最新版本下载
![img](/images/JMeterBasics11.png)
下载，安装
5、BadBoy的启动
进入安装文件夹，运行badboy.exe即可启动。
## 三、目录了解
1、bin目录
examples（例子）：该目录下存放Jmeter官方给的请求模板
report-template（报告模板）：该目录下存放Jmeter的报告模板（Jmeter是有自己的报告的）
templates（模板）：该目录下存放Jmeter的各类配置模板，例如：JDBC、Beanshell、ThinkTime等
jmeter.bat：Windows 的启动命令。
jmeter.log：日志文件。
jmeter.sh：Linux 系统下的启动文件。
jmeter.properties：系统配置文件，如配置编码格式。
jmeter-server.bat：Windows 分布测试要用到的服务器配置。
jmeter-server：Linux 分布式测试要用到的服务器配置。
2、docs目录
api：前面谈到Jmeter是开源的，此处便是它的API文档。
css：xxxx。
3、mage目录
部分图片资源
4、Extras目录
存放Build等配置，用于第三方集成构建
5、Lib目录
存放各类jar包，组件类函数类等
6、licenses目录
许可证书目录
7、printable_docs目录
用户手册
![img](/images/JMeterBasics12.png)
## 四、jmeter入门脚本
1、添加测试计划---当打开jmeter默认有一个测试计划.
![img](/images/JMeterBasics13.png)
2、添加线程组
鼠标在测试计划上---右键---添加---线程(用户)---线程组
![img](/images/JMeterBasics14.png)
3、添加HTTP请求
鼠标在线程组上---右键---添加---取样器---HTTP请求
![img](/images/JMeterBasics15.png)
4、配置HTTP请求
修改名称:发送百度请求
基本信息：
（1）填写协议:http
（2）填写服务器或IP:www.baidu.com
![img](/images/JMeterBasics16.png)
5、添加查看结果树
鼠标在线程组上---右键---添加---监听器---查看结果树
![img](/images/JMeterBasics17.png)
6、运行
注意：要保存后才能运行
![img](/images/JMeterBasics18.png)
![img](/images/JMeterBasics19.png)
7、查看结果
可点击text下拉选择请求结果的样式
![img](/images/JMeterBasics20.png)
知识点： 

| 功能     | 用例     |
| -------- | -------- |
| 测试计划 | 项目名称 |
| 线程组   | 业务流程 |
| HTTP请求 | 接口请求 |



## 五、线程用户
线程数:表示请求的虚拟用户数量
ramp-up:启动所有线程数所需要的时间(秒)
循环次数:线程数循环
![img](/images/JMeterBasics21.png)
注意：如果选择循环次数为永远，需要手动停止，会导致最后一个接口请求报错
## 六、取样器
作用:向服务器发送请求并且记录响应时间和响应内容
## 七、jmeter运行原理
1、jmeter是按照线程的方式来运行的
2、jmeterGUl模式运行测试脚本对电脑本身的资源消耗较大，无法实现大的并发和压力测试
3、使用命令行模式实现高并发和压力测试
4、使用GUl模式主要目的是编写和调面jmeter测试脚本
## 八、jmeter测试计划要素
使用jmeter编写测试脚本--要素
1、 测试计划
2、 在测试计划中至少有一个线程组
3、 在线程组中至少有一个取样器
4、 在测试计划中必须有监听器
## 九、jmeter录制脚本
1、使用badboy录制
（1）打开babboy在 地址栏中输入被测网址回车
（2）打开badboy时默认记录状态，输入网址直接操作即可
![img](/images/JMeterBasics22.png)
（3）操作完成--点击停止记录
![img](/images/JMeterBasics23.png)
（4）导出脚本：file--export to jmeter保存
2、在jmeter中打开已有文件
（1）jmeter脚本文件的后缀名.jmx
（2）在jmeter点击打开文件.选择文件路径,找到需要的文件进行打开
![img](/images/JMeterBasics24.png)
（3）添加查看结果树（不然看不到运行结果）
![img](/images/JMeterBasics25.png)
## 十、使用jmeter自身代理录制移动端（了解）
配置jmeter
1.打开jmeter创建新的测试计划
2.在测试计划下添加一个线程组
3.添加HTTP代理服务器
在测试计划下---右键--非测试元---HTTP代理服务
4.配置HTTP代理服务器
4.1端口号默认
4.2 https domains中填写电脑本地IP或localhost
查询电脑IP：打开cmd---执行ipconfig
4.3目标控制器选择测试计划>线程组
4.4点击启动按钮 ---点击OK
配置手机---打开手机端的 wifi设置
设置好了之后启动Jmeter代理服务器的 启动按钮（注意是里面的按钮）
然后就可以在手机端去操作业务了，可以正常的录制对应的app应用、微信公众号等业务，在线程组就会抓到对应的的请求
录制完成后，停止Jemter上的“HTTP代理服务器”，然后进行脚本调试
原理跟web端的脚本录制一样。脚本调试完成之后可以进行后续的压测了