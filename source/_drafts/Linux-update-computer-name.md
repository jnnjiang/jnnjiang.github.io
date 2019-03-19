---
title: Linux-update-computer-name
permalink: Linux-update-computer-name
toc: false
date: 2019-03-19 13:47:37
tags:
categories:
---
Ubuntu 更改计算机的名字：
打开/etc/hostname文件直接更改

更改之后，每次执行sudo 时会报如下警告（假设计算机的名字为abc）：
sudo: unable to resolve host abc


虽然sudo 还是可以正常执行, 但是警告讯息每次都出来,而这只是机器在反解上的问题, 所以就直接从/etc/hosts 设定, 让abc(hostname) 可以解回127.0.0.1 的IP 即可.

```
在127.0.0.1 localhost 后面加上主机名称(hostname) 即可, /etc/hosts 内容修改成如下: 
127.0.0.1      localhost abc  #要保证这个名字与 /etc/hostname中的主机名一致才有效
# 或改成下面这两行 
#127.0.0.1    localhost 
#127.0.0.1    abc
这样设完后, 使用sudo 就不会再有那个提示信息了。
```