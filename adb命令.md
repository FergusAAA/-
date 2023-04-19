# adb命令

## 目录

-   [连接adb](#连接adb)
-   [启动Activity](#启动Activity)
-   [删除普通的apk](#删除普通的apk)
-   [删除push的系统apk—1](#删除push的系统apk1)
-   [删除push的系统apk—2](#删除push的系统apk2)
-   [抓取日志](#抓取日志)
-   [抓取网络包](#抓取网络包)
-   [导出盒子某个路径下的文件](#导出盒子某个路径下的文件)
-   [杀进程](#杀进程)
-   [截图](#截图)
-   [清理缓存数据](#清理缓存数据)
-   [代理劫持](#代理劫持)
-   [查看当前进程内存](#查看当前进程内存)
-   [开启内存检测](#开启内存检测)
-   [打开布局边界](#打开布局边界)
-   [设置MAC](#设置MAC)
-   [基础shell命令](#基础shell命令)

# 连接adb

adb connect 10.10.49.27:112233

&#x20;                                                                                                          &#x20;

# 启动Activity

启动咪咕音乐miguapp：am start -n tv.icntv.migu/.activities.MainActivity

启动Activity 并带上intent参数 ：

&#x9;adb shell am start -n tv.icntv.ott/com.baymax.module.behavior.view\.BehaviorActivity --es key\_tab\_id 节目收藏

-   es key stringValue; 传递 String 参数;
-   ez key booleanValue; 传递 Boolean 参数；
-   ei key intValue; 传递 int 参数；
-   el key longValue; 传递 long 参数；
-   ef key floatValue; 传递 float 参数；

启动电视apk：am start -n tv.icntv.ott/.icntv

关闭app ：am force-stop tv.icntv.migu

# 删除普通的apk

adb uninstalll tv.icntv.migu

# 删除push的系统apk—1

adb shell

rm /system/app/icntv\*

rm -r /data/data/tv.icntv.ott

ps | grep icntv

kill \`ps |grep icntv | busybox awk '{print \$2}'\`

exit

adb push E:\icntv-viper-V5.1.010.16.07.08-new\.apk /system/app

adb reboot

***

***

# 删除push的系统apk—2

1.adb root

2.adb remount

3.adb shell

4.cd /system/app

5.ls 查看当前目录下的文件

6.rm -r XXX.apk

7.reboot

8.adb uninstalll tv.icntv.migu

# 抓取日志

adb logcat -c

adb logcat -v time > d:\201612261649.log

# 抓取网络包

adb shell tcpdump -i any -s 0 -w /data/1.pcap

adb pull /data/1.pcap \~/Desktop/0925.pcap

过滤网络包数据

http contains XXXX

# 导出盒子某个路径下的文件

adb pull /data/data/tv.icntv.ott/files/data/bootdata.xml d:/

# 杀进程

adb shell am force-stop 包名

adb shell

ps|grep xiri

kill 进程号

# 截图

（1）adb shell screencap -p /sdcard/screen.png

（2）adb pull /sdcard/screen.png Desktop/

# 清理缓存数据

adb shell pm clear 包名

# 代理劫持

-   设置代理&#x20;

    adb shell settings put global http\_proxy 192.168.27.54（本机IP）:8888（端口）
-   移除代理

    adb pull /data/data/com.android.providers.settings/databases/settings.db E:/123

    adb push E:/123/settings.db /data/data/com.android.providers.settings/databases

# 查看当前进程内存

adb shell dumpsys meminfo tv.icntv.ott

# 开启内存检测

adb shell monkey -p com.chinamobile.monitor 1

# 打开布局边界

adb shell setprop debug.layout true

# 设置MAC

adb shell setprop persist.sys.icntv.mac 58:b4:2d:6d:9c:4e

# 基础shell命令

-   创建文件夹

    mkdir (name)
-   创建文件

    vi filename
-   打印当前工作目录

    pwd&#x20;
-   编辑文件

    vi

    使用vi打开oldboy.py,默认是命令模式，需要输入a/i进入编辑模式,然后输入文本"Life is short,i use python"

    按下esc键，回到命令模式

    输入  :wq!  强制保存退出

    w write 写入

    q quit 退出

    ! 强制

    或者  :x 保存退出

    :q  不保存退出

    :q! 不保存强制退出
-   删除文件

    rm  test.txt&#x20;

    rm：是否删除 一般文件 "test.txt"? y &#x20;

    rm  homework &#x20;

    rm: 无法删除目录"homework": 是一个目录 &#x20;

    rm  -r  homework &#x20;

    rm：是否删除 目录 "homework"? y&#x20;
-   设置文件读写权限

    chromd命令

    4 读、2写、1执行

    chromd 755 file	当前用户可读可写可执行，其他用户可读可写不可执行

    chromd 700 file 当前用户可读可写可执行，其他用户不可读不可写不可执行
