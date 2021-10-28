# adb常用命令

## 一，连接

```shell
通过局域网连接,默认端口为5555 
adb connect 192.168.43.1:5555（ip:port）
通过usb连接，一般不需要输入连接命令
```

## 二，删除应用

```
adb   uninstall  com.voice.myapplication（包名）
```

## 三，安装apk

```sh
文件在电脑中，就执行
adb install -r "电脑文件位置"
文件在rom中，就执行
pm  install "rom的目录"
```

## 四，拉起apk

```sh
adb shell am start -n "com.voice.myapplication/com.voice.myapplication.MainActivity" (包名/类名)
```

## 五，上传文件

```sh
adb push "电脑文件地址" "rom文件地址"
```

## 六，下载文件

```sh
adb pull "rom文件地址" "电脑文件地址"
```

## 七，重新加载磁盘，并增加读写权限：

```sh
mount -o remount rw /system(磁盘或磁盘对应的目录)

有些需要修改文件
echo 1 > sys/kernel/debug/tracing/events/cgroup/cgroup_remount/enable
mount -o rw,remount /system
mount -o rw,remount /vendor
```

## 八，调用apk内容提供接口：

```sh
adb shell content query --uri content://stbconfig/livechannels
```

## 九，强制关闭apk

```shell
adb  shell am force-stop 包名
```

## 十，发送广播

```
db shell am broadcast -a <action> --es <字符参数> --ei 整型参数
```

## 十一，输入按键

```sh
adb shell input keyevent  82 
```

## 十二，查看包名

```sh
adb shell "pm list packages -f <| grep xxx>" 
```

## 十三，apk信息

```sh
dumpsys package 包名
```

## 十四，清理缓存

```sh
adb shell pm clear 包名
```

## 十五，日志输出

```sh
adb  logcat -vtime > "电脑地址"
```

## 十六，网络包

```
adb shell tcpdump -i any -p -s 0 -w /sdcard/tcpdump.pcap   不过滤任何数据
tcpdump -i any -s 0 -p -w /sdcard/tcpdump.pcap 'tcp[((tcp[12:1] & 0xf0) >> 2):4] = 0x47455420'  只抓http
```

## 十七，看内存使用情况

```sh
adb shell dumpsys meminfo cn.gd.snm.snmcm

单个应用可用最大内存主要对应的是这个值,它表示单个进程内存被限定在64m,即程序运行过程中实际只能使用64m内存，超出就会报OOM。（仅仅针对dalvik堆，不包括native堆）
adb shell  getprop | grep dalvik.vm.heapgrowthlimit 
adb shell  getprop | grep dalvik.vm.heapsize  
```

## 十八，录屏

```
adb shell screenrecord /sdcard/demo.mp4
```

## 十九，截图

```
adb shell /system/bin/screencap -p /sdcard/screenshot.png
```

## 二十，改分辨率

```sh
adb shell wm size 1920x1080
```

## 二十一，确认是否1080p

```sh
adb shell dumpsys window displays
getprop ro.sf.lcd_density
```

## 二十二，界面元素组成

```
adb shell uiautomator dump /sdcard/ui.xml
```

## 二十三，点击坐标

```sh
adb shell input tap 225 125
```

## 二十四，最顶activity

```
adb shell "dumpsys window windows | grep mFocus"
```

## 二十五，monkey测试

```sh
monkey -p cn.gd.snm.snmcm -v -v -v -s 300 --ignore-crashes --ignore-timeouts --ignore-security-exceptions --kill-process-after-error --pct-trackball 0 --pct-touch 0 --pct-motion 0 --pct-anyevent 0 --pct-flip 0 --pct-pinchzoom 0 --throttle 200 1200000
```

