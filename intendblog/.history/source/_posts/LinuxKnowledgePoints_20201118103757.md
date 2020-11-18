---
title: LinuxKnowledgePoints
date: 2020-11-18 10:27:15
comments: false
auto_excerpt: true
toc: true
tags: linux
categories: 
description:
---
此文仅是本人学习笔记。

## 1.登录和退出系统
在用户启动Linux系统后，为保证系统的安全性，用户登录系统时，为了使系统能够识别自己，必须输入用户名和密码，经系统验证无误后方能进入系统。
通常在Linux有三类用户：
root：超级用户帐号类似于Windows2000中的Administrator一样，它对系统的访问和控制没有限制。
普通用户：这个帐号供普通用户使用，可以进行有限的操作。
进程用户：对进程请求资源的访问进行限制。 
## 2.关机命令：
shutdown 或 shutdown –h now/+n(立即或n分钟后关闭系统)
halt：关闭系统（其实就是调用shutdown –h）
init 0
## 3.重新启动命令：
shutdown –r
init 6
reboot 
## 4.常用命令的使用
获得帮助命令：help、man
列出当前路径命令：pwd
显示登录计算机的用户信息：who
参看最近系统使用者登录的信息：last
更换登录者命令：su
显示和设定系统的日期和时间命令：date
## 5.Linux命令格式
命令提示符标识了命令行的开始，用户可以在提示符后面输入任何命令及参数。 
$：普通用户登陆时的命令提示符
#：root用户登陆时的命令提示符。
Linux操作系统对于英文字符的处理是大小写敏感的，无论是文件名还是命令名都需要区分大小写。通常命令以小写方式输入。
命令的补全方式：
TAB：系统自动补全
：重新显示刚执行过的命令 
## 6.目录管理命令
6.1pwd：显示当前工作目录 
6.2ls：列文件目录,ls [可选项]  [子目录名] [文件名] 
不带任何选项(ls)：列出当前目录（root）下的子目录与文件，不包括隐藏文件。 
选项-l（ls -l）：列出当前目录（root）下的子目录与文件的详细信息 
选项-a（ls -a）：列出当前目录下的子目录与文件，包括那些隐藏文件，其中以“.”开头的文件是隐藏的
使用文件名作为参数（ls -l 文件名），将只显示指定文件的信息 
ls *[0-9]* 显示包含数字的文件名和目录名
6.3cd：改变当前工作目录,cd  [目录名]  
cd /home 进入 '/ home' 目录'
cd .. 返回上一级目录
cd ../.. 返回上两级目录
cd 进入个人的主目录
cd ~user1 进入个人的主目录
cd - 返回上次所在的目录
6.4mkdir：建立目录 ,mkdir  [可选项] [目录名] 
可创建一个目录或多个目录，多个目录用（空格）隔开 (mkdir t1 t2 t3)
加选项¬-p：递归建立两个以上的目录（创建一个多级目录）mkdir -p t1/ t2
6.5rmdir：删除目录 ,rmdir  [可选项] [目录名]
注意：要删除的目录必须是空目录 
可删除一个目录或多个目录，多个目录用（空格）隔开 (rmdir t1 t2 t3)
加选项¬-p：递归删除  rmdir -p t1/ t2
## 7.文件管理命令
file:查看文件类型，file  [可选项] 文件名 
touch:新建文件;修改文件时间属性，touch  [可选项] 文件名 
touch命令中参数指定的文件不存在时，touch命令将按照参数中的文件名字建立文件，该文件为空文件，文件的大小为“0”字节。
touch命令通常应用于为满足某些需求（如实验、测试）而建立临时文件的场合。  
cp:复制文件，cp  [选项] 源文件或目录 目标文件或目录 
cp file1 file2：将当前目录中的file1文件复制为file2文件 
cp file1 file2 lxq：将当前目录中的filel和file2两个文件复制到当前目录的子目录lxq中 
cp -r a/ b/：选项- r或-R， cp将递归复制该目录下所有的子目录和文件。此时目标文件必须为一个目录名。 
rm:删除文件，rm  [选项] 文件或目录 
rm f*：可以同时删除参数中指定的多个文件（f开头的文件）。 
rm -r 目录：rm命令与“-r”选项配合使用可以完整地删除整个目录，无需事先删除目录中的内容。如果没有使用-r选项，则rm不会删除目录。 
mv:文件移动与文件重命名，mv [选项] 源文件或目录 目标文件或目录 
find:查找文件，find  [起始目录][查找条件][操作]  
find / -name file1 从 '/' 开始进入根文件系统搜索文件和目录
find / -user user1 搜索属于用户 'user1' 的文件和目录
find /home/user1 -name \*.bin 在目录 '/ home/user1' 中搜索带有'.bin' 结尾的文件
find /usr/bin -type f -atime +100 搜索在过去100天内未被使用过的执行文件
find /usr/bin -type f -mtime -10 搜索在10天内被创建或者修改过的文件
find / -name \*.rpm -exec chmod 755 '{}' \; 搜索以 '.rpm' 结尾的文件并定义其权限
find / -xdev -name \*.rpm 搜索以 '.rpm' 结尾的文件，忽略光驱、捷盘等可移动设备 
## 8.Linux文件查看
文本文件查看命令
cat、more、less、head和tail
cat 和more的区别
相同点在于：都是用来查看文件内容的指令，两者用法基本相同
不同点在于：cat指令查看完毕后会自动返回到正常模式而more指令则需要用户手动退出查看模式
head和tail的区别
head命令用于显示文件的头部，不使用任何选项时，默认显示文件的最前10行内容。 
tail命令用于显示文件的尾部，不使用任何选项时，默认显示文件的最后10行内容。 
通过在head和tail命令中使用选项“-n”，可以设置显示文件的前n行或后n行。 
通配符：
？：代表任意的一个单字符
*：代表任意个字符（0、1或多个）
[…]：代表“…”指定的字符范围
文本处理：
	grep str /tmp/test            在文件 '/tmp/test' 中查找 "str"
	# grep ^str /tmp/test           在文件 '/tmp/test' 中查找以 "str" 开始的行
	# grep [0-9] /tmp/test         查找 '/tmp/test' 文件中所有包含数字的行
	# grep str -r /tmp/*             在目录 '/tmp' 及其子目录中查找 "str"
	# diff file1 file2                   找出两个文件的不同处
	# sdiff file1 file2                 以对比的方式显示两个文件的不同
## 9.Linux文本编辑器vi
文本输入：
要输入文本必须首先将工作模式转换为文本编辑模式，
在命令模式下键入i、I、a、A、o、O等命令中的任意一个
即可。此时在状态/命令区出现“--INSERT--”。
•	i   从当前的光标位置开始输入字符
•	I   光标移动到当前行的行首，开始输入字符
•	a   从当前光标的下一个位置，开始输入字符
•	A   光标移动到当前行的行尾，开始输入字符
•	o   在光标所在行之下新增一行
•	O   在光标所在行之上新增一行
•	r            替换当前字符
•	R            替换当前字符及其后的字符，直至按ESC键
•	s            从当前光标位置处开始，以输入的文本替代指定数目的字符
•	S            删除指定数目的行，并以所输入文本代替之
•	ncw或nCW     修改指定数目的字
•	n1，n2 co n3 将n1行到n2行之间的内容拷贝到第n3行下 
•	n1，n2 m n3  将n1行到n2行之间的内容移至到第n3行下 
•	n1，n2 d     将n1行到n2行之间的内容删除
打开文件
文件的打开与读取操作
•	:vi filename          
	打开或新建文件名为***的文件到vi 编辑器中,并将光标置于第一行首
•	:vi +n filename        
	打开文件，并将光标置于第n行首
•	:vi + filename          
	打开文件，并将光标置于最后一行首
•	:vi +/pattern filename      
	打开文件，并将光标置于第一个与pattern匹配的串处
•	:vi filename....filename     
	打开多个文件，依次进行编辑
•	:w                     
	将工作缓冲区的变化写入默认文件中
•	:w filename             
	将工作缓冲区的变化写入名为***的文件中
•	:e filename              
	打开文件filename进行编辑
•	:r filename              
	读取文件内容到当前vi 编辑器中
Vi指令模式下常用命令
	:w       将编辑的文本存盘。
	:w!      若文件属性为“只读”时，强制存盘。
	:q      退出 vi（进入后没编辑过，q退出）。
	:q!      退出且不存盘（进入后编辑过不存盘，q！退出）。
	:wq      存盘并退出
命令行模式命令
指令	说明	指令	说明
0	移动光标到行首，等价[Home]	dd	删除光标所在行
$	移动光标到行尾，等价[End]	dnd	从光标当前开始删n行
PageDown	向下一页	yy	复制一行
PageUp	向上一页	P	粘贴复制的文字
d+方向键	删除文字	/string	从当前光标开始，向下查找指定的字符串
x	删除光标处的字符	?string	从当前光标开始，向上查找指定的字符串

## 10.用户账号文件、群组文件
10.1用户账号文件
	/etc/passwd：保存用户账号除了口令的其他信息，系统中的所有用户都可以读取其内容。不安全。
	例子：
	head -3  /etc/passwd---前3行信息，第一行是root超级管理员帐户
	tail -3  /etc/passwd---后三行信息，新建用户帐户添加在文件末尾
	“/etc/passwd”文件的每一行定义一个用户的属性。每个用户的属性包括七个部分，各部分以“：”分割，格式如下：用户账号的名称：口令（加密）：用户编号(uid )：用户组编号（gid )：用户全名：用户宿主目录：用户选用的命令解释器（Shell）
10.2用户口令文件
	/etc/shadow：保存加密的用户口令，只有管理员用户root才可以读取其中的内容。
	“/etc/shadow”文件的每一行定义一个用户的口令属性。每个口令的属性包括9个部分，各部分以“：”分割，格式如下：用户名：口令：最后一次修改时间：最大时间间隔：最小时间间隔：警告时间：不活动时间：失效时间：标志（未使用）
10.3组账号文件
	/etc/group：保存用户组除了口令的其他信息，系统中的所有用户都可以读取其内容。
	“/etc/group”文件的每一行定义一个组的属性。每个组的属性包括四个部分，各部分以“：”分割，格式如下：组名：组口令（加密）：组ID(gid )：组内用户列表
10.4组口令文件
	/etc/gshadow：用于定义用户组口令、组管理员等信息，只有管理员用户root才可以读取其中的内容。
	“/etc/gshadow”文件的每一行定义一个组的口令属性。每个口令的属性包括4个部分，各部分以“：”分割，格式如下：用户组名称：用户组口令：组的管理员帐号：属于该组的用户成员列表
## 11.用户帐号维护命令
useradd
1,添加用户帐号
	useradd 用户名：添加后需使用passwd命令设置口令才能登录
2,添加用户帐号时指定用户私有组
	useradd –g 组名 用户名
usermod
1,改变用户帐号名
	usermod –l 新用户登录名 当前用户登录名
2,锁定用户帐号
	usermod –L 用户帐号名：使其不能登录系统
3,解锁用户帐号
	usermod –U 用户帐号名
groupadd
1,建立普通组帐号名
	groupadd 组账号名
2,建立系统组账号
	groupadd –r 系统组账号名
groupmod
1,改变组帐号GID
	groupmod –g 新的GID名 用户组账号名
2,改变组帐号名
	groupmod –n 新的组名 原用户组名
groupdel
groupdel 组账号名称：删除指定的组账号
passwd
1,设置指定用户口令
	passwd  用户账号名
2,查询用户口令状态(只有root能用)
	passwd –S 用户账号名
3,锁定帐号
	passwd -l 用户账号名(只有root能用)
4,解锁用户帐号(只有root能用)
	passwd –u 用户账号名
5,删除用户口令
	passwd –d 用户帐号名
## 12.权限管理
12.1文件
读(r)：允许读文件的内容
写(w)：允许向文件中写入数据
执行(x)：允许将文件作为程序执行
12.2目录
读(r)：允许查看目录中有哪些文件和目录
写(w)：允许在目录下创建(或删除)文件、目录
执行(x)：允许访问目录(用cd命令进入该目录，并查看目录中可读文件的目录)
12.3用户分类
文件所有者(owner)：建立文件、目录的用户
同组用户(group)：属于同一组群的用户，对属于该组群的文件有相同的访问权限
其它用户(other)：除了文件所有者、同组用户之外的其它用户
12.4表示方式
字母表示：每一文件或目录的访问权限都有三组，每组用三位表示，分别为文件属主的读、写和执行权限；与属主同组的用户的读、写和执行权限；系统中其他用户的读、写和执行权限。
数字表示法
字母表示形式  十进制表示形式 权限含义	字母表示形式  十进制表示形式 权限含义
- - -            0          无权限
- - x            1          可执行
- w -            2          可写
- w x            3         可写、执行	
r - -            4          可读
r - x            5         可读、执行
r w -            6        可读、写
r w x            7      可读、写、执行
12.5设置文件目录权限方法
chmod  [可选项] [权限]  目录或文件名 
1、文字设定法
chmod [who] [+ | - | =] [mode]  [文件名| 目录名]
2、数字设定法
chmod  [mode] 文件名
注意1：
+ 添加某个权限。 
- 取消某个权限。 
= 赋予给定权限并取消其他所有权限（如果有的话）。 
注意2：
0表示没有权限，1表示可执行权限，2表示可写权限，4表示可读权限，然后将其相加，其值的范围是0-7，用来表示一组“rwx”权限。因为有三个组，所以数字属性的格式应为3个从0到7的八进制数，其顺序是（u）（g）（o）。 
注意3：
u 表示“用户（user）”，即文件或目录的所有者。 
g 表示“同组（group）用户”，即与文件属主有相同组ID的所有用户。 
o 表示“其他（others）用户”。 
a 表示“所有（all）用户”。它是系统默认值。
注意4：
r 可读。 
w 可写。 
x 可执行，只有目标文件对某些用户是可执行时才追加x 属性。 
设置文件目录权限例子
$chmod g+r,o+r example 
$ chmod a+x sort 
$ chmod ug+w,o-x text 
$ chmod  ugo–x  mm.txt 
$ chmod  644  mm.txt
步骤：更改文件权限和所有者
#更改chen为登陆用户
[root@localhost root]#su chen
#以chen的身份创建文件chentest
[chen@localhost chen]$cat chentest
   陈的文件
   <ctrl+D>
#修改文件权限为chen及其所在组成员可读可写可执行，其他组成员只读
[chen@localhost root]$chmod 774 chentest
#Root用户将文件file.txt的属主修改为chen，属组修改为netadmin
[root@localhost root]#chown chen.netadmin file.txt
12.6更改属主和组
1、chown
chown [-R] <用户[:组]><文件或目录>
-R:表示对目录及其子目录进行递归设置
将文件file1的属主改成user1 
chown user1 file1
将文件file2的组改成user1
chown :user1 file2
将文件file3的属主和组都改成user1
chown user1:user1 file3
将mydir目录及其子目录下所有文件和目录的属主和组改成user1
chown –R user1:user1 mydir
2、umask
设置文件或目录的默认权限
将默认权限改为拥有者读、写、执行，同组用户读、执行，其它用户读。
umask u=rwx,g=rx,o=r
umask 023
3、chgrp
chgrp group file
改变文件或目录组群
文件data2的组别改为staff
chgrp staff data2
## 13.磁盘分区
IDE接口的硬盘采用“hdxN”的文件名格式表示，其中“x”是英文字母，指分区所在的硬盘，第一块硬盘用“a”表示，第二块用“b”表示，依次类推；“N”是数字，1~4表示主分区，5开始之后的数字表示逻辑分区。
SCSI接口的硬盘代号由sda开始算起。目前常见的USB接口的优盘或者USB外接式硬盘，在Linux下仿真成SCSI设备，代号也是从sda开始算起。
## 14.Linux文件系统
14.1Linux文件系统类型
EXT2：正在被逐渐淘汰 
EXT3：在EXT2文件系统的基础上添加了“日志”功能 
Swap：在Linux系统的交换分区中使用  
注：对于微软公司的文件系统格式FAT32和NTFS，Linux能够部分地进行支持，大多数Linux系统支持FAT32文件系统的读写和NTFS的只读，而不能支持NTFS文件系统的写入。
14.2虚拟文件系统VFS
Linux可以支持多种不同的文件系统，并给Linux的其它部分和用户提供统一的文件操作接口，虚拟文件系统（VFS, Virtual File System）是实现这一功能的关键。通过虚拟文件系统，人们可以方便地向Linux增加新的文件系统。 
VFS实际上是用户进程与实际文件系统之间的一种接口。虚拟文件系统隐藏了各种硬件的具体细节，为所有的设备提供了统一的接口，VFS提供了多达数十种不同的文件系统。
vfat:在linux中把DOS下所有FAT文件系统统称为vfat。
NFS:即网络文件系统，用于在unix系统间通过网络进行文件共享，用户可以把网络中NFS服务器提供的共享目录挂载到本地文件目录中，可以象对本地文件系统一样操作NFS文件系统中的内容。
## 15.Linux文件系统加载
mount  [-t vfstype]  [-o optoins]  device  dir 
1、-t 文件系统类型
Fat32为vfat；
fat16为msdos
CDROM为iso9660
Linux分区为ext2或ext3
ntfs为NTFS
auto自动检测文件系统
swap交换分区文件系统
2、-o 选项
ro以只读方式挂载
rw以读写方式挂载
codepage=xxx代码页，对于中文codepage=936；iocharset=xxx字符集，对于中文iocharset=gb2312或iocharset=cp936
loop	挂载ISO光盘镜像文件
3、device 要挂载的设备文件，在/dev目录下
4、dir 要挂载的路径
umount卸载
umount  [选项] [挂载点] [设备名] 
	用于卸载系统中不需要使用的文件系统
任务实施：
步骤1：查看磁盘分区。 
[root@localhost root]# fdisk -l
步骤2：创建挂载点
[root@localhost root]#mkdir /mnt/usb
步骤3：加载U盘
[root@localhost root]#mount –t msdos /dev/sdb1 /mnt/usb
步骤4：访问
[root@localhost root]#ls -l /mnt/usb
步骤5：查看磁盘空间
[root@localhost usb]#du -s
[root@localhost root]#df
步骤6：卸载
[root@localhost root]#umount /mnt/usb
补充-虚拟机添加一块硬盘
VM中添加一块SCSI硬盘，加载到目录/newfs中
(1)查看添加的盘名：#fdisk –l
(2)建立分区并格式化ext3文件系统
#fdisk /dev/设备名
#mkfs –t ext4 /dev/设备名
(3)建立挂载点: #mkdir /newfs
(4)加载: #mount /dev/设备名 /newfs
## 16.磁盘配额管理
16.1系统管理员用来监控和限制用户或组对磁盘的使用工具。保证所有用户都拥有自己独立的文件系统空间，确保用户使用系统的公平性和安全性
16.2两方面限制
限制用户和组可以拥有的inode数(文件数)
限制分配给用户或组的磁盘块数目(以千字节为单位)
16.3三个概念
硬限制：超过此设定值后不能继续存储新文件
软限制：超过此设定值仍可继续存储，但系统发出警告信息，建议清理以释放更多空间
时限：超过软限制多长时间之内可继续存储文件
16.4磁盘配额步骤
编辑/etc/fstab启用quota功能
	(1)备份fstab：#cp /etc/fstab /etc/fstab.backup
	(2)在相应分区上修改挂载参数，在option上添加usrquota或grpquota：#vi /etc/fstab
	(3)重新挂载文件系统或重启：#mount -a
在设置限额的文件系统上创建quota文件，重新生成磁盘用量表
	#quotacheck -avug
分配用户和组的quota
	(1)设置用户的配额：#edquota –u username
	(2)将相同的配额设置复制给其他用户：#edquota –p<参考用户><待设置用户>
	(3)设置组的配额：#edquota –g groupname
	(4)设置软限制的宽限期：#edquota -t
启动配额设置
	(1)重启系统
	(2)执行命令：#quotaon -avug
查看磁盘配额
	(1)查看指定用户的quota设置：#quota [-ugv][<用户名>]
	(2)查看当前用户的quota设置：#quota [-ugv] 
	(3)查看所有用户的quota设置：#repquota [-augv]
## 17.文件压缩解压缩
17.1文件压缩可以减少文件的大小，这有两个明显的好处，一是可以减少存储空间，二是通过网络传输文件时，可以减少传输的时间。 
17.2Linux常用文件压缩解压缩命令
zip/unzip
gzip/gunzip 
具体分析：
zip  [选项] 文件名：打包和压缩文件 
•	-d：从压缩文件中抽走并删除
•	-g：增加而不重新压缩
•	-u：更新
•	-r：按目录结构递归压缩目录中所有文件
•	-m：压缩完成后删除源文件
unzip  [选项] 文件名 ：用于解压缩扩展名为.zip的压缩文件
•	1.-v：查看压缩文件目录，但不解压
•	2.-d：把压缩文件解压到指定目录下
•	3.-n：不覆盖已经存在的文件
gzip  [选项] 文件名：将文件压缩为后缀为.gz的压缩文件 
•	-d：对压缩文件解压
•	-l：对每个压缩文件显示详细信息，包括压缩文件的大小、未压缩文件的大小、压缩比、未压缩文件的名字
•	-r：参数为目录时，按目录结构递归地压缩目录中的所有文件
•	-v：对每个压缩和解压的文件显示文件名和压缩比
gunzip  [选项] 文件名：把gzip命令压缩的.gz文件进行解压缩
•	1.-v：显示解压缩文件的冗长结果
•	2.-r：递归处理，将指定目录下的所有文件及子目录一并处理
17.3Linux文件打包命令
tar
tar [选项] [打包文件名] [文件|目录] 
•	-c：创建tar包
•	-f：指定tar包的文件名
•	-v：显示处理文件信息的进度
•	-x：从备份文件中释放出来
•	-t：列出备份文件的内容
•	-z：用gzip命令来压缩/解压缩文件
•	-j：调用bzip2命令来压缩/解压缩文件
•	-r：向归档/压缩文件追加文件和目录
•	-u：更新文件
## 18.安装、升级、删除、查询RPM包
rpm  选项  RPM包的文件名 
1，查询
rpm –qa：查询系统中安装的所有RPM软件包
rpm –q 软件包名称：查询指定软件包是否安装
rpm –qi 软件包名称：查询系统中已安装软件包的描述信息
rpm –ql 软件包名称：查询系统中已安装软件包包含的文件列表
rpm –qf 文件全路径名：查询指定文件所属的软件包
2，安装
rpm –i RPM包全路径文件名：安装指定的RPM包到当前系统
rpm –ivh RPM包全路径文件名：安装并显示进度信息
注意：
i表示install
v表示verbose，显示较为详细信息
h表示hash，显示“#”表示安装进度
3，删除
rpm –e RPM包名称：从当前系统中删除已安装的软件包
4，升级
rpm –U RPM软件包全路径名：使用指定的PRM软件包对当前系统统一软件的较低级别版本进行升级
## 19.磁盘的加密测试步骤
安装软件包    yum install  cryptsetup 
查是否安装软件包 yum list all |grep cryptsetup
建立分区   fdisk  /dev/sdb 
格式化分区并设置密码 cryptsetup luksFormat  /dev/sdb8（大写YES）
启用加密分区
cryptsetup luksOpen  /dev/sdb8  testfs
创建文件系统 
mkfs -t ext4 /dev/mapper/testfs 
挂载文件系统mkdir /testfs mount  /dev/sdb8 /testfs 
卸载锁定加密盘
umount /testfs cryptsetup luksClose   testfs
验证是否可以再次挂载 mount  /dev/sdb8 /testfs
