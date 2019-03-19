---
title: Android-permission
permalink: Android-permission
toc: false
date: 2019-03-19 13:41:13
tags:
categories:
---
注意双声明权限 此处与activity声明权限不同 。Package要求某自定义权限时，需要同时使用<permission> Tag 和 <uses-permission> Tag

<permission
         android:name="com.hyman.demo.android.broadcast.permission.PERMISSION_PERMISSION" >
     </permission>
    <uses-permission android:name="com.hyman.demo.android.broadcast.permission.PERMISSION_PERMISSION"></uses-permission>
            