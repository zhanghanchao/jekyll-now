---
layout: post
title: 测试中常用到的adb shell
---

* 杀掉adb服务 adb kill-server
* 启动服务 adb start-server
* 查看设备列表 adb devices
* 清除app数据 adb shell pm clear "packagename"
* 查看包信息 aapt dump badging 包名 grep launchable-activity
* 查看包的文件 aapt list 包名
* 查看日志 adb logcat | grep ActivityMannager
* 获取当前界面元素：adb shell dumpsys activity top
* 获取任务列表：adb shell dumpsys activity activities
* 获取app启动activity:adb shell dumpsys package packagename
* 启动app后，获取app入口 adb logcat | grep -i displayed
* resume app启动 adb shell am start -W -n packagename/welcomeactivity -S
* 杀掉app进程：adb shell am force-stop packagename
