---
layout: post
title: app性能采集
---
1. 启动时间，录屏拆帧
* adb shell screenrecord --time-linit 10 /sdcard/video.mp4
* ffmpeg -i user/arvin/video.mp4 -r 10 -threads 2 user/xxx/android-capture-%05d.png
* -r 10 :表示1S10帧 
* -threads 2:如果是8核 就用6去解析；如果是6核，用2去解析更快
1. CPU
* adb shell top | grep packagename
* CPU详细信息：adb shell dumpsys cpuinfo packagename

2. 内存
* adb shell dumpsys meminfo 进程消耗内存列表
* android的虚拟机是dalvik的虚拟机，内存超过最大使用内存的时候就会OOM
* 查看进程可用的最大内存：adb shell getprop dalvik.vm.heapgrowthlimit

3. 流量：
* 测试前打开飞行模式，关闭飞行模式可将流量清零
* 先拿主要进程id
* 流量：adb shell cat /proc/#pid#/net/dev
* 消耗流量=上行+下行
