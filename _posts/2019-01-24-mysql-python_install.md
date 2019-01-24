---
layout: post
title: mysql-python
---
## _mysql.c(42) : fatal error C1083: Cannot open include file: 'config-win.h':问题的解决
#接口自动化安装mysql-python出现如上问题

1. 在http://www.lfd.uci.edu/~gohlke/pythonlibs/#mysql-python下载对应的包版本，如果是win7 64位2.7版本的python，就下载
MySQL_python-1.2.5-cp27-none-win_amd64.whl

2. 然后在命令行执行pip install MySQL_python-1.2.5-cp27-none-win_amd64.whl

3. 当然需要在cmd下跳转到下载MySQL_python-1.2.5-cp27-none-win_amd64.whl的目录下，然后就安装成功了MySQL-python
