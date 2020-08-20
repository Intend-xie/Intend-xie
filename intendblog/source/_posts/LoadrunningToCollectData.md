---
title: Loadrunning收集数据
date: 2020-08-11 11:07:34
comments: false
auto_excerpt: true
toc: true
tags: Loadrunning
categories: 
description:
---
此文仅是本人学习笔记。

## 服务器监控数据
### （一）准备监控工具
1.打开crt，择新建连接 ；
![img](/images/LoadrunningToCollectData1.png)
2.输入IP地址， IP地址为：192.168.1.210；
![img](/images/LoadrunningToCollectData2.png)
3.输入用户名及，点击OK；
![img](/images/LoadrunningToCollectData3.png)
4.输入账号密码：wjl/123456，可点击保存密码，这时已经登录上了；
![img](/images/LoadrunningToCollectData4.png)
### （二）监控命令
1.先在crt界面输入命令dstat -tcdnm -output xxxx.csv（如181116jzdl.csv注：命名要规范181116表示当天时间，jz表示基准测试，dl表示场景名称，如果是容量测试，可加上用户数量（181116rldl20.csv位置可自己喜好来调整；
![img](/images/LoadrunningToCollectData5.png)
2.再打开controller点击开始场景；
![img](/images/LoadrunningToCollectData6.png)
3.回到crt运行之前输入的命令（回车， 查看idl（空闲CPU，目标CPU占用率：≤80%
![img](/images/LoadrunningToCollectData7.png)
4.当场景运行完毕，则在crt这边Ctrl+C停止日志输出。
![img](/images/LoadrunningToCollectData8.png)
### （三）数据保存整理
1.crt输入下载命令sz rlxzsp20log.csv，择保存路径，可把日志文件下载到本地，该文件可用excel打开编辑；
![img](/images/LoadrunningToCollectData9.png)
打开后：
![img](/images/LoadrunningToCollectData10.png)
2.先在gh之间新增一列用在存放CPU的使用率：
计算公式为：（user+sys/sum（CPU总数回车得到CPU使用率；
![img](/images/LoadrunningToCollectData11.png)
照下图操作；
![img](/images/LoadrunningToCollectData12.png)
![img](/images/LoadrunningToCollectData13.png)
这些多余的数据需要删掉；
（判断方法的话，一般运行场景的压测的时候，CPU会有明显的变化。简单来说，你启动运行场景和结束场景运行，这个前后时间里，监控命令是否有多出的监控信息。）
![img](/images/LoadrunningToCollectData14.png)
3.再求出CPU使用率的平均值，再求出内存使用率的平均值；
![img](/images/LoadrunningToCollectData15.png)
4.在求内存使用率：计算公式为：used/sum（总数；
![img](/images/LoadrunningToCollectData16.png)
5.再求内存使用率平均值；
![img](/images/LoadrunningToCollectData17.png)
6.把CPU使用率的平均值和内存使用率平均值填到测试报告的表格里；
![img](/images/LoadrunningToCollectData18.png)
计算网络利用率，公式为send/(2.56*1024*1024)
![img](/images/LoadrunningToCollectData19.png)
### （四）遇到的问题
1.执行监控命令
[root@localhost /]# dstat -tcdnm 200805jzdl.csv
-bash: dstat: 未找到命令
![img](/images/LoadrunningToCollectData20.png)
2.安装dstat
yum install -y dstat
![img](/images/LoadrunningToCollectData21.png)
3.上传文件到linux服务器
securecrt 按下ALT+P就开启新的会话 进行ftp操作。
输入put C:/Users/Administrator/Desktop/dstat-0.7.2-12.el7.noarch.rpm上传
上传成功，在查看所在位置：pwd
![img](/images/LoadrunningToCollectData22.png)
4.安装
输入rpm -ivh dstat-0.7.2-12.el7.noarch.rpm进行安装
![img](/images/LoadrunningToCollectData23.png)
5.监控
dstat -tcdnm -output xxxx.csv
dstat -tcdnm xxxx.csv
执行后都报错
![img](/images/LoadrunningToCollectData24.png)
执行dstat、dstat -tcdnm都成功
![img](/images/LoadrunningToCollectData25.png)
![img](/images/LoadrunningToCollectData26.png)
发现output需要—output才能执行
执行dstat -tcdnm --output xxxx.csv成功
![img](/images/LoadrunningToCollectData27.png)
5.从linux服务器下载文件
securecrt 按下ALT+P就开启新的会话 进行ftp操作。
输入get 200805jzdl.csv下载
![img](/images/LoadrunningToCollectData28.png)
其他应用了解地址：https://wenwen.sogou.com/z/q799956086.htm