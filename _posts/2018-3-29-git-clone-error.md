---
layout: post
title: git clone 失败处理方法!
---

### git clone 出现下面错误
```html
remote: Counting objects: 1366, done.
remote: Compressing objects: 100% (3/3), done.
error: RPC failed; curl 56 LibreSSL SSL_read: SSL_ERROR_SYSCALL, errno 54
fatal: The remote end hung up unexpectedly
fatal: early EOF
fatal: index-pack failed
```

###  解决办法：

### 修改Git的传输字节限制即可。

#git config --global http.postBuffer  524288000
