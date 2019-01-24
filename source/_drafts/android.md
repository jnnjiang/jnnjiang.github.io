---
title: android
permalink: android
toc: false
date: 2019-01-17 17:07:34
tags:
categories:
---
工具只是为了提高开发效率，而我现在最应该做的是梳理Android所有的基础知识，并深入理解框架，把对jetpack等工具的学习放在最后，当你系统的掌握了知识之后，所有的变种都是很好理解的。
从现在起，按部就班的做自己最该做的事。

https://google-developer-training.github.io/android-developer-advanced-course-concepts/
https://google-developer-training.github.io/android-developer-fundamentals-course-concepts-v2/unit-1-get-started/lesson-1-build-your-first-app/1-0-c-introduction-to-android/1-0-c-introduction-to-android.html


## Keeping your code and your users more secure
You need to take precautions to make your code, and the user's experience when they use your app, as secure as possible.

Use tools such as ProGuard, which is provided in Android Studio. ProGuard detects and removes unused classes, fields, methods, and attributes.
Encrypt all of your app's code and resources while packaging the app.
To protect critical user information such as logins and passwords, secure your communication channel to protect data in transit across the internet, as well as data at rest on the device.

## Understanding the Android manifest
Before the Android system can start an app component such as an Activity, the system must know that the Activity exists. It does so by reading the app's AndroidManifest.xml file, which describes all of the components of your Android app. Each Activity must be listed in this XML file, along with all components for the app.
`android:allowBackup="true"`自动备份用户数据，api>=23是，默认是true，设备会自动将用户数据备份到云端，API<=22时，须用户手动设成true。

The minSdkVersion and targetSdkVersion settings in build.gradle will override any AndroidManifest.xml settings for the minimum SDK version and the target SDK version. gradle文件中的sdk版本配置信息会覆盖AndroidManifest.xml文件中的配置信息。
[android常用的groovy语法](http://google.github.io/android-gradle-dsl/current/index.html)

https://developer.android.com/courses/
https://material.io/design/color/#color-theme-creation
https://developer.android.com/guide/topics/ui/look-and-feel/themes
https://www.color-hex.com/
