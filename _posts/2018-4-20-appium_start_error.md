---
layout: post
title: appium start activity never started!
---

## appium启动问题
启动报错:original error 'activity' never start.

在我们首次启动app的过程中会遇到下面的报错，我们可以查看类似下面的日志：

![_config.yml]({{ site.baseurl }}/images/appium_start_error.png)

1. 我们可以看到报错日志，需要我们设置首次启动的activity:
2. aapt dump badging apk本机路径获取包信息
3. 在capabilities里面添加"appActivity": "com.XXXX.XXXX.activity.MainActivity"保存后便可以启动成功
