
重启X Window 
  Ctrl +Atl + Backspace

显示目前支持的语系
echo $LANG
修改语系
	$LANG=en_US

日期
	date
日历
	cal
	cal 2015		
	cal 3 2015  显示2015年3月日历
	cal day moth year

计算器
	bc

重置root密码
	重启系统按e键 显示
		root(hd0,0)
		kernel /vmlinuz-2.6.18-128.el5 ro root=LABEL=/ rhgb quiet 
initrd /initrd-2.6.18-128.el5.img
	光标移动到kernel 在最后输入 single
		/ rhgb quiet single
	按下Enter 在按 b 登录系统 使用passwd修改密码
	[root@www~]# passwd


档案权限与目录配置
帐号信息记录在 /etc/passwd 目录。
个人密码记录在 /etc/shadow
组名记录在 /etc/group

Linux 文件属性
chgrp 改变所属组权限
chgrp [-R] dirname/filename ...
	-R 递归调用

chgrp 组名 文件或目录


chown 改变所有者
[root@www ~]# chown [-R] 账号名称 档案戒目彔 
[root@www ~]# chown [-R] 账号名称:组名 档案戒目彔
chown 改变权限
	数字改变权限
	
权限字母对应数字
r:4 w:2 x:1

	chown 777 就是将所有的权限变成 rwxrwxrwx
	chown 654  对应 rw-r-xr—

	使用符号改变权限
	三组权限对应字母
	user : 	u
	group: 	g
	other: 	o
		 	a 代表全部
	
	chmod ugoa +-= rwx  dfile

	例如：
		chmod a+wx dfile  给所有的权限加上wx
		chmod go-x dfile   去掉group other 的 x 权限

Linux档案种类与扩展名
正规档案
			纯文本档(ASCII)   例如 cat ~/.bashrc
			二进制文件(binary) 例如 cat 命令
			数据格式文件(data) 例如 last  /var/log/wtmp cat则读出是乱码

目录(directory)：第一个属性为 [ d ]，例如 [drwxrwxrwx]。

连结档(link)： 
就是类似Windows系统底下的快捷方式，第一个属怅为 [ l ](英文L的小写)，例如 [lrwxrwxrwx] ；

设备与装置文件(device)：
例如硬盘，软盘
	区块(block) ：  [brw-rw----]  /dev/sda 第一个属性是b

字符(character)设备文件：
第一个属性为 [ c ] 例如，鼠标键盘
资料接口文件(sockets)
第一个属怅为 [ s ]， 最常在/var/run这个目彔中看到这种文件类型，这种类型的档案通常被用在网络上的数据承接

数据输送文件(FIFO, pipe)：
	他主要的目的在览决多个程序同时存取一个档案所造成的错误问题。 FIFO是first-in-first-out的缩写。第一个属性为[p] 。



Linux目彔配置的依据--FHS


Linux使用的哪个发行版本
	uname –r
    

Linux 目录
目录
应该放置的内容
/bin
放置单人维护模式下还能被操作的指令。在/bin底下的指令可以被root与一般账号所使用，主要有: cat,chmod,chown,date,mv,mkdir,cp,bash等。
/boot
主要放置Linux核心以及开机选项与开机所需配置文件。Linux kernel常用的档名为：vmlinuz，如果使用的是grub这个开机管理程序，则还会存在/boot/grub/这个目录。
/dev
任何装置与接口设备都是以档案的形态存在与这个目录当中的。存取目录下的档案，就等于存取某个装置。比较重要的有/dev/null,/dev/zero, /dev/tty, /dev/lp*, /dev/hd*, /dev/sd* 等。
/etc
配置文件都放置在这个目录。例如账号密码文件，各种服务的启始档等。比较重要的有: /etc/inittab, /etc/init.d, /etc/modprobe.conf, /etc/X11, /etc/fstab, /etc/sysconfig
/home
系统默认的家目录。当新增一个一般使用者账号时，默认的用户家目录就会规范到这里来。比较重要的是，家目录有两种代号：
~：代表目前这个用户的家目录，
~dmtsai ：代表dmtsai的家目录
/lib
开机会用到的函数库，以及在/bin或/sbin地下指令会呼叫的函数库。尤其重要的是/lib/modules目录，因为该目录会放置核心相关的模块（驱动程序）!
/media
放置可移除的装置，包括软盘、光盘、DVD等装置。常见的档案名有：/media/floppy, /media/cdrom
/mnt
暂时挂载某些额外的装置
/opt
放置第三方软件的目录
/root
系统管理员的家目录。
/sbin
放置开机过程中所需要的，里面包括了开机、修复、还原系统所需要的指令。至于某些服务器软件一般放置在/usr/sbin当中。至于本机自行安装的软件所产生的系统执行文件(system binary)，则放置到/usr/local/sbin/当中了。
/srv
是一些网络服务启动后，这些服务所需要取用的数据目录。常见的服务器例如www,FTP等。
/tmp
一般用户或者是正在执行的程序暂时放置档案的地方。
/lost+found
使用标准ext2/ext3文件系统格式产生的一个目录。当文件系统发送错误时，将一些遗失的片段放置到这个目录下。
/proc
这个目录是一个 虚拟文件系统。他放置的数据都是在内存当中的，不占硬盘空间。例如系统核心，进程信息、周边装置的状态及网络状态等。比较重要的有 /proc/cpuinfo, /proc/dma, /proc/interrupts /proc/ioports /proc/net/* 等。
/sys
这个目录和/proc类似，主要记录与核心相关的信息，包括目前已加载的核心模块与核心侦测到的硬件装置信息等。

根目录与开机有关，开机过程中仅根目录会被挂载。因此根目录下与开机过程有关的目录必须与根目录放在同一分割区。
	/etc : 配置文件
	/bin : 重要执行文件
	/dev : 所需要的装置档案
	/lib : 执行档所需要的函数库与核心所需的模块
	/sbin : 重要的系统执行文件

/usr 的意义与内容
 usr 是 Uinx Software Resource的缩写。也就是Unix 操作系统资源所放置的目录。因为所有系统默认的软件（distribution发布者提供的软件）都放置到/usr底下，因此这个目录有点类似与windows系统的[c:\windows + c:\Program files] 。系统刚安装完毕这个目录会占用最多的硬盘容量。一般 /usr的次目录建议：
	
目录
应放置的档案
/usr/X11R6
为 X Window System 重要数据所放置的目录，之所以取名为X11R6 是因为最后的X版本为第11版，且该版的第6次释出
/usr/bin
绝大多数的用户可使用的指令都放在这里。
/usr/include
c/c++等程序语言的头文件。
/usr/lib/
包含各种应用软件的函数库、目标档案，以及不被一般使用者惯用的执行档或脚本。某些软件会提供一些特殊的指令来进行服务器的设定，这些指令也不会经常被系统管理员操作，那就会放到这个目录。
/usr/local
系统管理员在本机自行安装自己下载的软件（非distribution默认提供者）, 建议安装到此目录，这样会比较便于管理。举例来说，你的distribution提供的软件较旧，你想安装较新的软件但又不想移除旧版，此时你可以将新版软件安装于/usr/local/目录下，可与原先的旧版软件有分别。
/usr/sbin/
非系统正常运作需要的系统指令，最常见的就是某些网络服务器软件的服务器指令。
/usr/share/
放置共享文件的地方，在这个目录下放置的数据几乎是不分硬件架构均可读取的数据。
/usr/share/man 联机帮助文件
/usr/share/doc 软件杂项的文件说明
/usr/share/zoneinfo 与时区有关的档案
/usr/src
一般源代码建议放置到这里。核心原始码建议放置到/usr/src/linux目录下。



/var 的意义与内容
/var 在系统运作后才会渐渐占用硬盘容量的目录。因为/var目录主要针对常态性变动的档案，包括快取(cache). 登录档(log file)以及某些软件运作所产生的档案，包括程序档案(lock file, run file)。例如MySQL数据库的档案等。
目录
应放置的档案
/var/cache
应用程序本身运作过程中会产生的一些暂存档
/var/lib
程序本身实现过程中，需要使用到的数据库文件放置的目录。在此目录下各自的软件应该要有各自的目录。例如:/var/lib/mysql
/var/lock
某写资源一次只能被一个程序所使用。因此需要给该装置上锁。
/var/log
登录文件放置的目录！里面比较重要的档案如
/var/log/messages/ var/log/wtmp 等。
/var/mail
放置个人电子邮件
/var/run
某些程序或服务启动后，会将他们的PID放置到这个目录
/var/spool
放置一些队列数据。


档案与目录的管理
cd : 变换目录
pwd : 显示当前目录
mkdir : 创建目录
rmdir : 删除一个空的目录

cd  ~xq  去xq的家目录
cd -  回到刚才那个目录
cd 	回到家目录

pwd –P 显示当前目录真实链接



mkdir –mp 创建目录
-m 指定权限
-p 递归创建目录

mkdir –p dir1/dir2/dir3 递归创建目录
mkdir –m 777 d3 创建目录d3 权限是rwxrwxrwx

rmdir –p 删除空的目录
rmdir –p /dir1/dir2/dir3 递归删除这3个空的目录
如果要将目录及其下的所有东西删除使用 rm –r

执行文件路径的变量$PATH
使用 echo $PATH 显示当前执行文件的路径
给PATH添加路径
 	PATH=”$PATH”:/root 	将/root 添加到PATH

浏览档案与目录的命令　ls
	ls [-aAdfFhilnrRSt] 目录名
	ls [--color={never,auto,always}] 目录名称
	ls [--full-time] 目录名称

选项与参数:
-a : 全部的档案，连同隐藏档（开头为 . 的档案）一起列出来（常用）
-A : 全部档案，连同隐藏档，但不包括 . 与 .. 这两个目录
-d : 仅列出目录本身，而不是列出目录内的档案数据
-f : 直接列出结果，而不进行排序(ls预设会以档名排序)
-F : 根据档案、目录等信息，给予附加数据结构，例如：
	*：代表可执行文件； /：代表目录； =：代表 socket档案；|：代表FIFO档案；
-h : 将档案容量以人类较容易读的方式（例如 GB,KB 等等）列出来；
-i : 列出inode号码
-l : 长数据串行出
-n : 列出UID 与 GID 而非使用者与群组名称
-r : 将排序结果反向输出。
-R ： 连同子目录内容列出
-S ：以档案容量大小排序，而不是用档名排序；
-t : 依时间排序，而不是用档名。
--color=never : 不要依据档案特性给予颜色显示
--color=always : 显示颜色
--color=auto 自动决定
--full-time :  已完整时间模式输出
--time={atime,ctime}输出access时间或改变权限属性时间

复制、删除、移动 cp rm mv

cp 复制

cp [-adfilprsu] source dist
cp [options] source1 source2 ... directory

选项和参数
-a : 相当与-pdr
-d : 若原文为链接文件，则复制链接文件而非档案本身
-f : 强制，若目标档案已经存在且无法开启，则移除后在尝试一次
-i : 若目标文件已经存在，在覆盖时会询问
-l : 进行硬式连接的档案建立，而非复制档案本身
-p : 连同档案的属性一起复制过去，而非使用默认属性
-r : 递归持续复制
-s : 复制成为符号链接文件
-u : 若dest 比 source 旧才更新

rm(移除档案或目录)
rm [-fir] 档案或目录
选项与参数：
-f : 强制；
-i : 删除前提示
-r : 递归删除

特殊情况：已 ‘-’开头的档案删除方法：
用touch ./-aa-- 建立档案
1. rm ./-aa—
2. rm -- -aa—

mv移动档案与目录，或更名
mv[-fiu] source dest
mv[options] sourc1 source2 ... directory
选项与参数：
-f : 强制覆盖
-i : 提示
-u : 若目标档案已经存在，且source比较新，才会更新


获取路径的文件名与目录名称
[root@www ~]# basename /etc/sysconfig/network 
 
[root@www ~]# dirname /etc/sysconfig/network 
/etc/sysconfig <== 取得的变成目录名了！

档案内容查阅
cat 由第一行开始显示档案内容
tac 从最后一行开始显示
nl 显示的时候，顺道输出行号
more 一页一页显示档案内容
less 与 more 类似可以往前翻页
head只看头几行
tail只看尾巴几行
od已二进制的方式读取档案内容

cat [-AbEnTv]
选项与参数:
-A : 相当于 –vET 
-b : 列出行号，仅针对非空白行做行号显示，空白行不标行号
-E : 将结尾的断行字符$显示出来；
-n : 打印行号，连同空白行也会有行号，与-b的选项不同
-T : 将[tab]按键以^I显示
-v : 列出一些看不出来的特殊字符

	tac反向显示
	
	
nl（添加行号打印）
选项与参数：
-b :指定行号指定的方式：
		-b a ：无论是否为空行，也同样列出行号
		-b t ：如果有空行，空的那一行不要列出行号
-n : 列出行号表示的方法：
		-n ln : 行号在屏幕的最左方
		-n rn : 行号在自己字段的最右方显示，且不加0；
		-n rz : 行号在自己字段的最右方显示，且加0；
-w : 行号字段的占用的位数。

nl -b a –n rz –w 3 /etc/issue


可翻页检视

more (一页页翻动)
 空格键 ： 代表向下翻一页
 Enter : 向下翻一行
 /string : 向下搜索字符串
 :f     :立刻显示出文件名以及目前显示的行数
 q 		:退出
 b		:往后翻页

less(一页页翻动)
空格键 ： 向下翻动一页；
[pagedown]：向下翻动一页
[pageup]：向上翻动一页
/string :向下搜索
?string :向上搜索
n :重复前一个搜索
N :反向的重复前一个搜索
q : 离开

资料截取
head (取出前面几行)
-n : 后面接数字，代表显示行数

tail (取出后面几行)
-n : 后面接数字，代表显示几行
-f :表示持续侦测后面所接的档名，Ctrl+c 结束

	tail –n 20 /etc/sudo.conf  显示sudo.conf末尾10行
	持续侦测 /var/log/messages 的内容
	tail –f /var/log/messages

	例如，显示 /etc/sodu.conf的第11行到第20行的内容
	

非纯文本档案 od
od [-t TYPE]
-t : 后面可以接
	a : 默认的字符来输出
	c : 使用ascii 字符来输出
	d : 利用十进制来输出数据，每个整数占用size bytes;
	f : 利用浮点数来输出数据
	o : 利用八进制来输出数据
	x : 利用十六进制来输出数据

修改档案时间或建立新档 touch
touch [-acdmt] 档案
-a : 仅修订access time;
-c : 仅修改档案时间，若档案不存在则不建立档案
-d : 后面接欲修订的日期而不用目前的日期。
-m : 仅修改mtime;



档案与目录的默认权限与隐藏权限
系统隐藏属性使用chattr来设定，使用lsattr来查看。

档案预设权限 : umask
显示默认权限


022的意思是group和other权限 拿掉 w 权限

档案的隐藏属性
档案的隐藏属性只能在Ext2/Ext3的文件系统上面生效。
chattr[+-=][ASacdistu] 档案或目录名称
	+ : 增加特殊参数
: 移除
=  : 设定
	
	A: 若存取档案或目录时，他的访问时间atime将不会被修改。
	S：将档案进行同步写入
	a: 只能增加数据，而不能删除也不能修改数据，root 设定
	c: 压缩档案
	d: 当dump程序被执行的时候，设定d属性将可使该档案（或目录）不会被dump备份
	i: 不能删除，改名，修改，新增
	s: 删除无法恢复
	u: 删除可以恢复

显示档案的隐藏属性
lsattr [-adR] 档案或目录
-a : 将隐藏文件的属性也显示出来
-d : 如果接的目录，仅列出目录本身的属性
-R : 联通子目录的数量也一并列出。




档案特殊权限 : SUID,SGID,SBIT

Set UID
当s这个标志出现在档案拥有者的x权限上时【-rwsr-xr-x】，此时就被称为Set UID,简称特殊权限。

SUID 权限仅对二进制程序有效；
执行者对于该程序需要具有x的执行权限
本权限仅在执行该程序的过程中有效(run-time)
执行者将具有该程序拥有者的权限。

	以上的意思是，具有suid “s” 标志权限的二进制文件，在被运行的时候会获取root权限。

Set GID
当s 出现在组权限的x的位置时是Set GIG 【-rwx—s—x】
对二进制和目录都有效。

如何使用xq账号登录去执行locate时，那xq将会取得slocate群组的支持，因此能够去读取mlocate.db。

Sticky Bit
目前只针对目录有效：
	当用户对于目录具有w,x权限，亦即具有写入的权限时；
	当用户在该目录下建立档案或目录时，仅有自己与root才有权利删除该档案
例如/tmp 目录的权限


SUI/SGID/SBIT权限设定
	4 ： SUID
	2 ： SGID
	1 ： SBIT

将将档案权限改成[-rwsr-xr-x] chmod 4755 或者 chmod u=rws,go=rx;

观察文件类型:file
查看档案的基本数据：ASCII，data，binary 且是否使用动态函数库

file 档案



指令与档案的搜索

脚本文件的搜索
which [-a] command
-a:将所有由PATH目录中可以找到的指令均列出，而不止第一个被找到的指令名称
which  ifconfig

档案档名的搜索
whereis (寻找特定档案)
whereis [-bmsu] 档案或目录名
-b : 只找binary格式的档案
-m : 只找在说明文件manual路径下的档案
-s : 只找source来源档案
-u : 搜寻不在上述三个项目中的其他特殊档案


locate [-ir] keyword
-i : 忽略大小写的差异
-r : 后面可接正规表示法的显示方式
locate搜索的结果都在/var/lib/mlocate.db中。
更新数据库指令 updatedb

	updatedb ：根据/etc/updatedb.conf的设定去搜寻系统硬盘内的文件名，并更新/var/lib/mlocate内的数据库档案；
	locate : 依据/var/lib/mlocate内的数据库记载，找出用户输入的关键词文件名



磁盘与目录的容量
磁盘的整体数据在superblock区块，个别档案的容量在inode中记载。

df: 列出文件系统的整体磁盘使用量
du:评估文件系统的磁盘使用量

df [-ahikHTm] [目录]
-a ：列出所有的文件系统，包括系统特有的 /proc等
-k ：以KBytes的容量显示各文件系统
-m ：以MBytes的容量显示各文件系统；
-h ：以人们易阅读的GBytes,MBytes,KBytes等格式
-H ：以M=1000K取代M=1024K的进位方式；
-T ：连同该partition的filesystem名称
-i ：不用硬盘容量，而以inode的数量来显示

du [-ahskm]档案或目录名称
-a ：列出所有的档案与目录容量
-h ：以人们较易读的容量格式（G/M）显示
-s ：列出总量而已，而不列出每个各别的目录占用容量
-S ：不包括子目录下的总计，与-s有点差别
-k ：以KBytes列出容量显示
-m ：以MBytes列出容量显示

实体链接与符号链接: ln

Hard Link 实体链接，硬式连接
	每个档案都有一个inode，档案的内容由inode的记录来指向；
	想要读取该档案，必须要经过目录记录的文件名来指向到正确的inode号码才能 读取

Symbolic Link （符号链接）
建立一个独立的档案，而这个档案会让数据的读取指向他link的那个档案的档名！

ln [-sf] 来源文件 目标文件
-s ：如果不加任何参数就进行连接，那就是hard link, -s是symboliclink
-f ：如果 目标文件 存在时，就主动的将目标文件直接移除后在建立。

磁盘的分割、格式化、检验与挂载




档案与文件系统的压缩与打包
常见的压缩档格式
	*.Z compress	程序压缩的档案
	*.gz gzip		程序压缩的档案
	*.bz2 bzip2 	程序压缩的档案
	*.tar			tar程序打包的数据，并没有压缩过
	*.tar.gz		tar程序打包的档案，经过gzip压缩
	*.tar.bz2		tar程序打包的档案，经过bzip2压缩


gzip,zcat

gzip [-cdtv#] 档案名
-c : 将压缩的数据输出到屏幕是那个，可透过数据流重导向来处理
-d : 解压缩的参数
-t : 可以用来检验一个压缩文件的一致性
-v : 显示原档案/压缩文件案的压缩比等信息
-# : 压缩等级，-1最快，但是压缩比最差,-9最慢，默认-6

gzip –v file  输出file.gz 原文件不存在

使用 zcat 读出压缩文件的内容
zcat file.gz 读出档案内容

解压缩文档
gzip –d file.gz

bzip2,bzcat

bzip2取代了gzip并提供了更佳的压缩比。

bzip2[-cdkzv#] 档案名
-c : 将压缩的过程产生的数据输出到屏幕上
-d : 解压缩参数
-k : 保留源文件，而不会删除原始档案
-z : 压缩参数
-v : 显示原档案/压缩文件案的压缩比
-# ： 与gzip同样，-9最佳，-1最快

范例1：将/tmp/file.txt 以 bzip2压缩
bzip2 –v file.txt

范例2： 将范例1的档案内容读出
bzcat file.txt.bz2



打包指令tar
-c : 建立打包档案，可搭配-v 来查看过程中呗打包的档名(filename)
-t : 查看打包档案的内容
-x : 解打包 搭配-C 在特定目录解开
-j : 透过bzip2 的支持进行压缩/解压缩，档名最好是 *.tar.bz2
-z : 透过gzip 的支持进行压缩/解压缩, 档名最好是 *.tar.gz
-v : 将正在处理的文件名显示出来。
-f : 要处理的档名
-C 目录 ： 解压到特定目录
-p : 保留各备份数据的原本权限与属性，常用于备份(-c)重要的配置文件
-P : 保留绝对路径，亦即允许备份数据中含有根目录存在之意
--exclude =FILE: 在压缩过过程中，不要将FILE打包


压缩 tar –jcv –f filename.tar.bz2 要被压缩的档案或目录名称
查询 tar –jtv –f filename.tar.bz2
解压缩 tar –jxv –f filename.tar.gz2 –C 解压缩的目录

使用tar 备份 /etc目录


查阅 tar档案的数据内容（可查看文件名）与备份文件名有否根目录的意义


如果加上-v这个选项时，详细的档案权限/属性都会被列出来！

将根目录也备份下来


仅解开单一档案的方法



打包某目录，但不含该目录下的某些档案
