---
title: android-p
permalink: android-p
toc: false
date: 2019-01-17 13:14:29
tags:
categories:
---
## changes
- Android 9 (API level 28):音乐播放器需要使用`foreground service`，从Android 9起，使用`foreground service`  必须申请权限`android.permission.FOREGROUND_SERVICE`该权限是个普通权限，申请就会被授予，但是如果不申请，运行`foreground service`时就会抛出异常` SecurityException`。
- 支持多个Camera，可以用过`getCameraIdList ()`获取所有系统可用的camera。
- 从非Activity的context启动一个Activity，需要传入flag`FLAG_ACTIVITY_NEW_TASK`，否则Activity将不能启动。
With Android 9, you cannot start an activity from a non-activity context unless you pass the intent flag FLAG_ACTIVITY_NEW_TASK. If you attempt to start an activity without passing this flag, the activity does not start, and the system prints a message to the log.
- 获取WiFi的 SSID 或 BSSID，也需要申请位置权限，即需要声明以下三个权限。
```
ACCESS_FINE_LOCATION or ACCESS_COARSE_LOCATION
ACCESS_WIFI_STATE
```
- 访问手机号或收集状态，需要权限组`CALL_LOG`
- Note that all Android Support Libraries also depend on some base level of the platform, for recent releases, that is Android 4.0 (API level 14) or higher.最近release的Support-Library，最低支持到API 14.也就是说即使是support-v4也不是最低支持到v4版本了。
- 引入了ImageDecoder类
- [提供权限发布格式](https://medium.com/googleplaydev/what-a-new-publishing-format-means-for-the-future-of-android-2e34981793a)