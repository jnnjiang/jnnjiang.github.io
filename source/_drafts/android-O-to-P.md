---
title: android-O-to-P
permalink: android-O-to-P
toc: false
date: 2019-01-28 17:28:04
tags:
categories:
---

error:
```

cn-nana.jiang <cn-nana.jiang@ff.com>

FAILED: out/target/common/obj/APPS/FactoryImage_intermediates/src/R.stamp out/target/common/obj/APPS/FactoryImage_intermediates/aapt.srcjar

frameworks/support/v7/appcompat/res/

ERROR: resource directory 'frameworks/support/design/res' does not exist
```
resolve
```
从Android.mk文件中，删除design相关的配置。因为升级到P之后，/framework/support/下面没有了design文件夹，其他库的结构也有变化，具体原因需要再研究下，尤其是每个Support库都实现了什么功能。
```