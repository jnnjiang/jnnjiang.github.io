---
title: Android-IPC
permalink: Android-IPC
categories: Android
toc: false
date: 2019-01-19 13:45:06
tags:
---


### Service 和 Activity通信
service = com.ff.logpost.service.LogPostService$LogPostBinder@ef3ead8   同一个进程
service = android.os.BinderProxy@d67893a   不同的进程


不同进程中，一定要用AIDL进行IPC通信。