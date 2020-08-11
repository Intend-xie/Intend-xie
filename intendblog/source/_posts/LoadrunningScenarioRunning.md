---
title: Loadrunning脚本运行
date: 2020-08-11 10:19:14
tags: Loadrunning
---
此文仅是本人学习笔记。

## 一、启动场景控制台
1、启动控制台
![img](/images/LoadrunningScenarioRunning1.png)
![img](/images/LoadrunningScenarioRunning2.png)
添加脚本，选择脚本名称，点击“Add==》”按钮，再点击“OK”按钮
![img](/images/LoadrunningScenarioRunning3.png)
![img](/images/LoadrunningScenarioRunning4.png)
## 二、配置
1、设置generators 
![img](/images/LoadrunningScenarioRunning5.png)
Name填写为localhost，点击“OK”后，关闭Load Generators窗口
![img](/images/LoadrunningScenarioRunning6.png)
![img](/images/LoadrunningScenarioRunning7.png)
2、配置场景
![img](/images/LoadrunningScenarioRunning8.png)
1）选择模式，run mode有两种a、Real-world schedule，b、Basic schedule
a、Real-world schedule
![img](/images/LoadrunningScenarioRunning9.png)
初始化、启动阶段、运行阶段、停止阶段
（1）初始化按默认：a、全部初始化，b、设置单位时间逐步初始化，c、运行前初始化，默认c
（2）开始阶段：配置最大用户数，选择方式：同时和增压，默认增压：单位时间增压用户数、单位时间长度
（3）运行阶段：选择方式：到运行完成为止 和 持续运行，默认持续运行：配置运行时长
（4）停止阶段：选择方式：同时和减压，默认减压：配置单位时间减压用户数、单位时间长度
b、Basic schedule
![img](/images/LoadrunningScenarioRunning10.png)
初始化、启动阶段、运行阶段、【停止阶段】
用户总数：填写/修改“total：[  ]Vusers”的[  ]中数量
（1）初始化按默认：a、全部初始化，b、设置单位时间逐步初始化，c、运行前初始化，默认c
（2）开始阶段：选择方式：同时和增压，默认同时
（3）运行阶段：选择方式：“到运行完成为止”、“持续运行”和“一直运行不停”，默认“到运行完成为止”，选择持续运行则出现停止阶段
（4）停止阶段：选择方式：同时和减压
3、修改超时时间
![img](/images/LoadrunningScenarioRunning11.png)
打开“脚本运行时配置”框，选中“Internet protocol-preferences”，点击“options...”按钮进行配置
![img](/images/LoadrunningScenarioRunning12.png)
配置超时时间，http下的“请求连接超时”、“请求接收超时”、“请求存活超时”的时长，及general下的“下载超时”的时长
![img](/images/LoadrunningScenarioRunning13.png)
![img](/images/LoadrunningScenarioRunning14.png)
时长配置好后，点击“OK”再点击“OK”保存配置
![img](/images/LoadrunningScenarioRunning15.png)
## 三、视图配置及启动
1、配置运行监控视图
切换运行监控界面
![img](/images/LoadrunningScenarioRunning16.png)
![img](/images/LoadrunningScenarioRunning17.png)
配置图表个数，在图表区域点击鼠标右键，选择显示8张图表
![img](/images/LoadrunningScenarioRunning18.png)
8张图表
![img](/images/LoadrunningScenarioRunning19.png)
修改图表展示所需的图表，选中要修改的图表，双击左侧列表中需要的图表
running vusers，tran response time，tran/sec(passed)，total tran/sec(passed)，hits per second，throughput，connections per second，error statistics
![img](/images/LoadrunningScenarioRunning20.png)
2、运行场景
点击“start scenario”按钮
![img](/images/LoadrunningScenarioRunning21.png)
results directory already exists提示框上选择“是”，覆盖目录
![img](/images/LoadrunningScenarioRunning22.png)
场景运行中
![img](/images/LoadrunningScenarioRunning23.png)
3、运行结果
（1）运行时如tran response time，tran/sec(passed)，total tran/sec(passed)， error statistics没有图效果时需检查log看看问题
操作，点击右键，选择show vuser log
![img](/images/LoadrunningScenarioRunning24.png)
（2）设置run-time setting中log的配置
![img](/images/LoadrunningScenarioRunning25.png)
（3）重新运行脚本，可查看show vuser log
![img](/images/LoadrunningScenarioRunning26.png)
（4）如果还是没有图，检查一下事务点
``` bash
# 在脚本最开始的加上
lr_start_transaction();
# 在末尾加上
lr_end_transaction()
```