# 查看cpu温度

cat /sys/class/thermal/thermal_zone0/temp

# 查看内存命令

## 1.cat /proc/meminfo  

内存使用情况

##  2.ps aux 

```
程序占用内存情况

   a 显示所有终端机下执行的进程，除了阶段作业领导者之外。
   u 以用户为主的格式来显示进程状况。
   x 显示所有进程，不以终端机来区分。
   USER：该 process 属于那个使用者账号的
   PID ：该 process 的号码
   %CPU：该 process 使用掉的 CPU 资源百分比
   %MEM：该 process 所占用的物理内存百分比
   VSZ ：该 process 使用掉的虚拟内存量 (Kbytes)
   RSS ：该 process 占用的固定的内存量 (Kbytes)/RSS 是常驻内存集（Resident Set Size），表示该进程分配的内存大小。
   TTY ：该 process 是在那个终端机上面运作，若与终端机无关，则显示 ?，另外， tty1-tty6 是本机上面的登入者程序，若为 pts/0 等等的，则表示为由网络连接进主机的程序。
   STAT：该程序目前的状态，主要的状态有
   R ：该程序目前正在运作，或者是可被运作
   S ：该程序目前正在睡眠当中 (可说是 idle 状态)，但可被某些讯号 (signal) 唤醒。
   T ：该程序目前正在侦测或者是停止了
   Z ：该程序应该已经终止，但是其父程序却无法正常的终止他，造成 zombie (疆尸) 程序的状态
   START：该 process 被触发启动的时间
   TIME ：该 process 实际使用 CPU 运作的时间
   COMMAND：该程序的实际指令
   VSS- Virtual Set Size 虚拟耗用内存（包含共享库占用的内存）
   RSS- Resident Set Size 实际使用物理内存（包含共享库占用的内存）
   PSS- Proportional Set Size 实际使用的物理内存（比例分配共享库占用的内存）
   USS- Unique Set Size 进程独自占用的物理内存（不包含共享库占用的内存）
```



## 3.top  ##内存和CPU信息

```
  第一行，任务队列信息，同 uptime 命令的执行结果，具体参数说明情况如下：
  14:06:23 — 当前系统时间
  up 70 days, 16:44 — 系统已经运行了70天16小时44分钟（在这期间系统没有重启过的吆！）
  2 users — 当前有2个用户登录系统
  load average: 1.15, 1.42, 1.44 — load average后面的三个数分别是1分钟、5分钟、15分钟的负载情况。
  load average数据是每隔5秒钟检查一次活跃的进程数，然后按特定算法计算出的数值。如果这个数除以逻辑CPU的数量，结果高于5的时候就表明系统在超负荷运转了。

  第二行，Tasks — 任务（进程），具体信息说明如下：
  系统现在共有206个进程，其中处于运行中的有1个，205个在休眠（sleep），stoped状态的有0个，zombie状态（僵尸）的有0个

  第三行，cpu状态信息，具体属性说明如下：
  5.9%us — 用户空间占用CPU的百分比。
  3.4% sy — 内核空间占用CPU的百分比。
  0.0% ni — 改变过优先级的进程占用CPU的百分比
  90.4% id — 空闲CPU百分比
  0.0% wa — IO等待占用CPU的百分比
  0.0% hi — 硬中断（Hardware IRQ）占用CPU的百分比
  0.2% si — 软中断（Software Interrupts）占用CPU的百分比

  第四行,内存状态，具体信息如下：
  32949016k total — 物理内存总量（32GB）
  14411180k used — 使用中的内存总量（14GB）
  18537836k free — 空闲内存总量（18GB）
  169884k buffers — 缓存的内存量 （169M）

  第五行，swap交换分区信息，具体信息说明如下：
  32764556k total — 交换区总量（32GB）
  0k used — 使用的交换区总量（0K）
  32764556k free — 空闲交换区总量（32GB）
  3612636k cached — 缓冲的交换区总量（3.6GB）

PID：当前运行进程的ID
  USER：进程属主
  PR：每个进程的优先级别
  NInice：反应一个进程“优先级”状态的值，其取值范围是-20至19，一
  　　　　共40个级别。这个值越小，表示进程”优先级”越高，而值越
  　　　　大“优先级”越低。一般会把nice值叫做静态优先级
  VIRT：进程占用的虚拟内存
  RES：进程占用的物理内存
  SHR：进程使用的共享内存
  S：进程的状态。S表示休眠，R表示正在运行，Z表示僵死状态，N表示
  　 该进程优先值为负数
  %CPU：进程占用CPU的使用率
  %MEM：进程使用的物理内存和总内存的百分比
  TIME+：该进程启动后占用的总的CPU时间，即占用CPU使用时间的累加值。
  COMMAND：进程启动命令名称
```



## 4.free

```text
total : 总计物理内存的大小。
used : 已使用多大。
free : 可用有多少。
Shared : 多个进程共享的内存总额。
Buffers/cached : 磁盘缓存的大小。
-/+ buffers/cached) :
used:已使用多大;
free:可用有多少。
```



# 查看磁盘使用情况：

## 1. df -m 

以Mb为单位显示磁盘使用量和占用率

## 2.du：

评估文件系统的磁盘使用量（常用于评估目录所占容量）



# apt-get更新

```text
sudo apt-get update 
sudo apt-get upgrade
```



# 更换软件源(含列表)

```text
#2018-8
sudo nano /etc/apt/sources.list

deb http://mirrors.ustc.edu.cn/raspbian/raspbian/ stretch main contrib non-free
deb-src http://mirrors.ustc.edu.cn/raspbian/raspbian/ stretch main contrib non-free
#我这里用的是中科大的源，我的raspbian版本是stretch，如果是jessie或其他版本可以自行修改。

#2019-3
一键换源
直接执行以下两行命令，即可替换将官方默认软件源替换为中科大或清华镜像源。
2018.05.18更新：新的默认源为raspbian.raspberrypi.org
因此一键换源相应改为
sudo sed -i 's#://raspbian.raspberrypi.org#s://mirrors.tuna.tsinghua.edu.cn/raspbian#g' /etc/apt/sources.list
sudo sed -i 's#://archive.raspberrypi.org/debian#s://mirrors.tuna.tsinghua.edu.cn/raspberrypi#g' /etc/apt/sources.list.d/raspi.list
```

```sh
【软件源列表】：

中国科学技术大学
Raspbian http://mirrors.ustc.edu.cn/raspbian/raspbian/

阿里云
Raspbian http://mirrors.aliyun.com/raspbian/raspbian/

清华大学
Raspbian http://mirrors.tuna.tsinghua.edu.cn/raspbian/raspbian/

华中科技大学
Raspbian http://mirrors.hustunique.com/raspbian/raspbian/
Arch Linux ARM http://mirrors.hustunique.com/archlinuxarm/

华南农业大学（华南用户）
Raspbian http://mirrors.scau.edu.cn/raspbian/
 
大连东软信息学院源（北方用户）
Raspbian http://mirrors.neusoft.edu.cn/raspbian/raspbian/

重庆大学源（中西部用户）
Raspbian http://mirrors.cqu.edu.cn/Raspbian/raspbian/

中山大学 已跳转至中国科学技术大学源
Raspbian http://mirror.sysu.edu.cn/raspbian/raspbian/
 
新加坡国立大学
Raspbian http://mirror.nus.edu.sg/raspbian/raspbian
```

```sh
保存sources.list文件以后修改rapsi.list文件：
sudo nano /etc/apt/sources.list.d/raspi.list
#将原有内容用#注释掉
deb http://mirrors.aliyun.com/raspbian/raspbian/ buster main
deb-src http://mirrors.aliyun.com/raspbian/raspbian/ buster main
```

