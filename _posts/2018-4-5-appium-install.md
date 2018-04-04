### appium环境配置

## 一，安装jdk.

* 下载地址：http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html

* windows10环境变量配置
1. JAVA_HOME：C:\Program Files\Java\jdk1.8.0_161</br>
2. path: %JAVA_HOME%\bin</br>
3. 在命令行运行javac,java显示正常就算成功

## 二，安卓sdk.

* 下载地址：https://android-sdk.en.softonic.com/
* 下载完成后解压文件，配置sdk环境变量
1. ANDROID_HOME：C:\installexe\android-sdk_r24.4.1-windows\android-sdk-windows
2. path: %ANDROID_HOME%\platform-tools </br> %ANDROID_HOME%\tools </br> %ANDROID_HOME%\build-tools\27.0.3
3. 在命令行运行adb和aapt检测环境配置是否成功
* 运行SDKmanager.exe配置。</br>

![_config.yml]({{ site.baseurl }}/images/sdkmanager.png)

* 运行AVD manager.exe
1. 点击create
2. 设置模拟器参数 </br>

![_config.yml]({{ site.baseurl }}/images/AVDmanager1.png)

3. 启动模拟器 </br>

![_config.yml]({{ site.baseurl }}/images/AVDmanager2.png)

## nodejs安装
1. 下载地址：https://nodejs.org/en/download/current/
2. 安装完成后运行node -v查看安装是否成功

## appium-python-client
1. 下载地址：https://pypi.python.org/pypi/Appium-Python-Client
2. 解压文件后，cd到setup.py目录，运行命令python setup.py install

## appium-desktop
1. 下载地址：https://github.com/appium/appium-desktop/releases

## 按照以上步骤，初始环境基本完成
