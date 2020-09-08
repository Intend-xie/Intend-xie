---
title: Loadrunning容量测试中遇到的问题
date: 2020-08-30 22:58:10
comments: false
auto_excerpt: true
toc: true
tags: Loadrunning
categories: 
description:
---
此文仅是本人学习笔记。

## 录制完脚本，出错：Failed to load temporary action file(C\Users\ADMINI~1\AppData\LocaNTemp\vuac usr73),restoring original file.Check that the TMP directory is not full or write protected.
原因：
Action.c的文件丢失。
解决方法：
（1）创建一个新的脚本。
（2）在文件夹里找到其他的后缀为.c的文件用工具编辑文本，然后把东西拷出，拷到里新建的脚本里面，补上Action.c的文件的内容，然后重新运行。
## 大量并发会导致Error -26697: Missing CR/LF after body/trailer ("Transfer-Encoding: chunked")
原因：
不明。
解决方法：
未解决。
## 大量并发后报错Error -27796: Failed to connect to server "dangjian.gdaee.com.cn:8088": [10060] Connection timed out
网上查找的解决方法：
方法一：
在注册表HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters里，有如下两个键值：
TcpTimedWaitDelay
MaxUserPort
1,这里的TcpTimedWaitDelay默认值应该中是30s，所以这里，把这个值调小为5s（按需要调整）。
2,也可以把MaxUserPort调大（如果这个值不是最大值的话）。
此法不通！

方法二：
修改run time setting中的请求超时时间Preferences 中点击Options 其中有三项的参数可以一次都修改了，HTTP-request connect timeout，HTTP-request receieve timeout，
Step download timeout，分别建议修改为1000、1000、10000；run time setting设置完了后记住还需要在control组件的option的run time setting中设置相应的参数；
此法不通！

原因：
迭加数值设置为3
解决方法：
（1）设置run time setting中的run logic中的迭加数值设置为1。
![img](/images/CapacityTestingIssues1.png)
## 运行场景最后出现error -82034 Rendezvous release failed
原因：
集合点释放失败，可能内存太低导致。
解决方法：
（1）重新设置STOP vuser。
（2）修改集合点的超时时间，如由1秒改为30秒。
![img](/images/CapacityTestingIssues2.png)
## TPS中有Action_Transaction 和 vuser_init_Transaction
原因：
不明。
解决方法：
（1）run time setting--Miscellaneous--Automatic Transactions在脚本和场景设置中同时勾上这两项，保存后，再去掉勾选这两项，再保存。
![img](/images/CapacityTestingIssues3.png)

## Error -26377: No match found for the requested parameter "outboundFlight". Check whether the requested boundaries exist in the response data. Also, if the data you want to save exceeds 256 bytes, use web_set_max_html_param_len to increase the parameter size
原因：
开发更改接口，没有发现匹配请求的参数，响应数据中存在边界错误。
解决方法：
（1）修改边界值。
（2）注释掉没有匹配请求的参数。
## Error -27727: Step download timeout (120 seconds) has expired when downloading resource(s).
原因：
请求超时，默认是120 seconds。
解决方法：
（1）在Vuser Generator中的Vuser--->Run-Time Settings...---->Internet Protocol--->Preferences---->HTTP-request connect timeout (sec)和HTTP-request receive timeout (sec) 分别设置1000，Step download timeout (sec) 设置10000即可解决。
## Error -27796: Failed to connect to server "ip地址": [10060] Connection timed out
原因：
由于下载的速度慢导致超时，所以需要调整一下超时时间。
解决方法：
（1）修改run time setting中的请求超时时间Preferences 中点击Options 其中有三项的参数可以一次都修改了，HTTP-request connect timeout，HTTP-request receieve timeout，Step download timeout，分别建议修改为1000、1000、10000；run time setting设置完了后记住还需要在control组件的option的run time setting中设置相应的参数；
（2）Browser Emulation 中的Download non-HTML resources 选项去掉，点击OK即可。
（3）如果还是不行，设置runt time setting中的internet protocol-preferences中的advaced区域有一个winlnet replay instead of sockets选项，选项后再回放就成功了。切记此法只对windows系统起作用。
参考博客：https://blog.csdn.net/weixin_30856965/article/details/95607767
## Failed to Initialize. Reason: TimeOut 
原因：
因为某个虚拟用户在transaction初始化时超时了。
解决方法：
（1）调整 Run-timesetting－>Internet Protocol－>references－>Advaanced－>Options，将HTTP-request connect timeout,request receive timeout,和Step download timeout的时间都调成了最大1000s.
![img](/images/CapacityTestingIssues4.png)
（2）除了运行时设置里的首选项高级外，还有tools-options-timeout，可以在controller-tools-timeout,修改command timeout(seconds), 可以解决初始化超时问题。
![img](/images/CapacityTestingIssues5.png)