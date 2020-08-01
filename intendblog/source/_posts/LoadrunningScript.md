---
title: 手写loadrunning脚本
date: 2020-07-30 14:50:16
tags: Loadrunning
---
此文仅是本人学习笔记。

## 1、为什么要手写脚本
（1）浏览器兼容性不好，IE9或者以上不支持
（2）录制的脚本过长
（3）可能开发只提供接口，没有页面可以录制

## 2、常用函数
get的页面请求用web_url
表单提交web_submit_form
post数据请求用web_submit_data

## 3、抓包工具
浏览器自带工具：使用Chrome或者其他浏览，F12的network列表查看请求（刷新页面可以重新查看）
其他专业抓包工具：HttpWatch、Fiddler、BurpSuite…

## 4、loadrunner脚本创建
（1）点击鼠标--选择Insert--选择New step--选择类型--填写信息，填入相应参数
![选择New step](/images/LoadrunningScript1.png)
![选择类型](/images/LoadrunningScript2.png)
![填写信息](/images/LoadrunningScript3.png)
（2）生成脚本，并修改如下（
Ⅰ参数中的引号"前需要加斜杠\转译
如：json 对象
错误："Value={"cate":[{"fieldName":"BACCNAME","text":"功能分类名称 "}],"series":[{"fieldName":"SUMMONEY","text":"支出金额"}],"desc":[{"sqlField":false,"fieldName":"金额(万元)"}]}", 
正确："Value={\"cate\":[{\"fieldName\":\"BACCNAME\",\"text\":\"功能分类名称 \"}],\"series\":[{\"fieldName\":\"SUMMONEY\",\"text\":\"支出金额\"}],\"desc\":[{\"sqlField\":false,\"fieldName\":\"金额(万元)\"}]}",
Ⅱ手写脚本"Snapshot="为空
Ⅲ扩展中是请求后的静态资源js、css、woff
Ⅳ脚本写好后可通过回放，验证脚本的正确性
可参考：https://jingyan.baidu.com/article/9158e000138687a2541228b4.html

## 5、设置测试点
| 函数                     | 描述                             |
| ------------------------ | -------------------------------- |
| lr_start_sub_transaction | 标记子事务的开始                 |
| lr_start_transaction     | 标记事务的开始                   |
| lr_end_sub_transaction   | 标记子事务的结束以便进行性能分析 |
| lr_end_transaction       | 标记 LoadRunner 事务的结束       |

例子：
```javascript
lr_rendezvous("集合点");
    lr_start_transaction("登陆时间");
    web_submit_form("login.pl", 
        "Snapshot=", 
        ITEMDATA, 
        "Name=username", "Value=test1", ENDITEM, 
        "Name=password", "Value=123456", ENDITEM, 
        LAST);
lr_end_sub_transaction("登陆时间",LR_ABORT);
```

## 6、设置变量参数
（1）在loadrunner的进行编写脚本，或者一个网页登录界面进行录制脚本，录制完成之后，在脚本找登录的用户名，选中用户右键》》replace with a pararmeter。
![replace with a pararmeter](/images/LoadrunningScript4.png)
（2）弹出了一个为select or create parameter的框，可以对parameter name名称重名，也可不命名。---这样在代码脚本中的用户名就变为了一种颜色，变为参数名。
（3）需要对参数名进行参数化，可以点击菜单中的open parameter list的按钮，点击进入。可以看到的是newparam默认的一个参数了为xinling，需要在行中在添加数据，可点击add row添加行，输入数据双击value就可进行输入，输入网页中其它的用户名。
![设置参数](/images/LoadrunningScript5.png)
（4）参数化数据准备好之后，就进行执行了，在执行前，需要到run-time settings设置的界面中，run logic的选项界面中，把循环的次数改为2次，因准备数据只有两条了。
![run-time settings](/images/LoadrunningScript6.png)
![设置循环测试](/images/LoadrunningScript7.png)
（5）设置完成之后，可以点击loadrunner的界面中菜单运行按钮，等待脚本完成之后，可以在执行log看到执行的结果数据，是成功执行成功的。
![执行结果](/images/LoadrunningScript8.png)

## 7、字符串参数化例子
###  1）对登录账号参数化
（1）确定参数
![确定参数](/images/LoadrunningScript9.png)
（2）新建参数，选中字符串点击鼠标右键，选择“replace with a parameter”菜单
![新增参数](/images/LoadrunningScript10.png)
（3）在弹框中填写参数名称，点击“OK”完成参数化
![填写参数名称](/images/LoadrunningScript11.png)
（4）参数化后，字符串被参数名替换
![参数名替换](/images/LoadrunningScript12.png)
（5）快捷键“ctrl+L”查看参数列表
![查看参数列表](/images/LoadrunningScript13.png)
###  2）密码参数化，与账号关联，使用户名和密码对应，便可登录成功
（1）选中字符串点击鼠标右键，选择“replace with a parameter”菜单
![选择“replace with a parameter”](/images/LoadrunningScript14.png)
（2）在弹框上填写名称，点击“properties...”打开配置窗口
![打开配置窗口](/images/LoadrunningScript15.png)
（3）参数配置窗口，file选择用户名参数的文件
![选择用户名参数的文件](/images/LoadrunningScript16.png)
（4）添加一列用于存放密码，点击“add column...”按钮，点击“OK”确认添加
![add column...](/images/LoadrunningScript17.png)
![添加字段](/images/LoadrunningScript18.png)
（5）配置select next row选项为“same line as username”，即下一行数据选择与用户名同一行，点击“close”
![select next row](/images/LoadrunningScript19.png)
（6）点击“OK”完成密码参数化
![完成密码参数化](/images/LoadrunningScript20.png)
（7）密码字符串被参数替换
![密码字符串被参数替换](/images/LoadrunningScript21.png)
（8）查看参数列表（ctrl+L）
![查看含密码的参数列表](/images/LoadrunningScript22.png)

## 8、关联函数
###  一、什么是关联
关联（correlation）：脚本回放过程中，客户端发出请求，通过关联函数所定义的左右边界值（也就是关联规则），在服务器所响应的内容中查找，得到相应的值，已变量的形式替换录制时的静态值，从而向服务器发出正确的请求，这种动态获得服务器响应内容的方法被称作关联。也是把脚本中某些写死的数据，转变成动态的数据。
什么内容需要关联：当脚本中的数据每次回放都发生变化时，并且这个动态数据在后面的请求中需要发送给服务器，那么这个内容需要通过关联来询问服务器，获得该数据的变化结果。
例如：
1.登录字符串。带有会话 ID 或时间戳等动态数据的登录字符串。
2.日期/时间戳。使用日期或时间戳或者其他用户凭据的任意字符串。
3.常见前缀。后跟字符串的常见前缀，如 SessionID 或 CustomerID。
###  二、web_reg_save_param函数说明
语法：
```javascript
int web_reg_save_param(const char *ParamName, <list of Attributes>, LAST);
```
参数说明:
· ParamName: 存放得到的动态内容的参数名称。
· list of Attributes: 其它属性，包括：Notfound, LB, RB, RelFrameID, Search, ORD, SaveOffset, Convert, SaveLen。属性值不分大小写。
o Notfound: 当在返回信息中找不到要找的内容时应该怎么处理。
o Notfound=error: 当在返回信息中找不到要找的内容时，发出一个错误讯息。这是缺省值。
o Notfound=warning: 当在返回信息中找不到要找的内容时，只发出警告，脚本也会继续执行下去不会中断。
o LB( Left Boundary ) : 返回信息的左边界字串。该属性必须有，并且区分大小写。
o RB( Right Boundary ): 返回信息的右边界字串。该属性必须有，并且区分大小写。
o RelFrameID: 相对于URL而言，欲查找的网页的Frame。此属性质可以是All或是数字，该属性可有可无。
o Search : 返回信息的查找范围。可以是Headers，Body，Noresource，All(缺省)。该属性质可有可无。
o ORD : 说明第几次出现的左边界子串的匹配项才是需要的内容。该属性可有可无，缺省值是1。如为All，则将所有找到的内容储存起来。
o SaveOffset : 当找到匹配项后，从第几个字元开始存储到参数中。该属性不能为负数，缺省值为0。
o SaveLen ：当找到匹配项后，偏移量之后的几个字元存储到参数中。缺省值是-1，表示一直到结尾的整个字串都存入参数。
###  三、实例分析
1）查看页面源码 (PC端登录页面，获取用户id)
（1）在浏览器上登录到首页，查看源码
![查看源码](/images/LoadrunningScript23.png)
（2）查到需获取的字符串（在页面上搜索）
![获取的字符串](/images/LoadrunningScript24.png)
（3）确定左边界、右边界 及 字符串的数量（LB/RB/ORD）
左边界LB=userid=
右边界RB=';
数量为1，ord缺省
```javascript
web_reg_save_param(
       "userid",
       "LB=userid=",
       "RB=';",
       LAST)
```
2）调试脚本
（1）添加消息打印，打印参数值，设置断点（F9）
```javascript
lr_output_message("userid=%s",lr_eval_string("{userid}"));
```
![调试脚本](/images/LoadrunningScript25.png)
（2）F5回放脚本，查看replay log中消息打印结果
![F5回放脚本](/images/LoadrunningScript26.png)
（3）修改用户密码（即{username}和{password}的值），重新回放脚本，查看replay log消息打印结果（验证接口请求正确）
![查看replay log消息打印结果](/images/LoadrunningScript27.png)
调试结果通过的判定条件：
1、web_submit_data执行成功，
2、打印出来的参数值与页面源码中的值一致
3）关联参数有多个参数时，注意一下操作
```javascript
web_reg_save_param("TypeId","LB=\"type\":\"","RB=\",LAST);
web_submit_data()；
lr_output_message("TypeId=%s",lr_eval_string("{TypeId}"));
```
直接关联没有加"ORD=all"获取到的是第一个参数，不会获取其他参数；加上"ORD=all"，获取所有参数，以数组形成保存，可通过数组下标进行获取如{TypeId_1}。具体如下：
```javascript
web_reg_save_param("TypeId","LB=\"type\":\"","RB=\","ORD=all",LAST);
web_submit_data()；
lr_output_message("TypeId=%s",lr_eval_string("{TypeId_1}"));
```
4）如何取值LB、RB
1、不取变量值
2、不取中文
3、字段长度10个字符左右
5）转换说明符
| 转换说明符 | 说明                                    |
| ---------- | --------------------------------------- |
| %a(%A)     | 浮点数、十六进制数字和p-(P-)记数法(C99) |
| %c         | 字符                                    |
| %d         | 有符号十进制整数                        |
| %f         | 浮点数(包括float和doulbe)               |
| %e(%E)     | 浮点数指数输出[e-(E-)记数法]            |
| %g(%G)     | 请求头浮点数不显无意义的零"0"           |
| %i         | 有符号十进制整数(与%d相同)              |
| %u         | 无符号十进制整数                        |
| %o         | 八进制整数    e.g.     0123             |
| %x(%X)     | 十六进制整数0f(0F)   e.g.   0x1234      |
| %p         | 指针                                    |
| %s         | 字符串                                  |
| %%         | "%"                                     |
其中常用的主要是%d和%s，其他进行了解。

## 9、验证回放数据
1）	查看请求是否成功
查看replay log消息，查看接口是否请求成功
![查看replay log消息](/images/LoadrunningScript28.png)
回放https的问题：https://jingyan.baidu.com/article/9158e000138687a2541228b4.html
如遇到其他问题可自行百度处理
2）查看数据是否正确
（1）打开回放的显示窗口
步骤：点击tools—点击general options—选择display—勾选show run-time viewer during re]和auto arrange windo—打开回放的显示窗口
![点击general options](/images/LoadrunningScript29.png)
![选择display](/images/LoadrunningScript30.png)
（2）查看回放返回的数据与页面接口请求返回中的值是否一致