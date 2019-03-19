---
title: android-studio-error-1
permalink: android-studio-error-1
toc: false
date: 2019-03-19 11:26:40
tags:
categories:
---

## 1
错误：
```
4417): Shutting down VM
05-10 10:59:46.084 E/AndroidRuntime( 4417): FATAL EXCEPTION: main
05-10 10:59:46.084 E/AndroidRuntime( 4417): Process: com.leeco.vehicle, PID: 4417
05-10 10:59:46.084 E/AndroidRuntime( 4417): android.view.InflateException: Binary XML file line #55: Binary XML file line #55: Error inflating class android.support.v7.widget.RecyclerView
05-10 10:59:46.084 E/AndroidRuntime( 4417): Caused by: android.view.InflateException: Binary XML file line #55: Error inflating class android.support.v7.widget.RecyclerView
05-10 10:59:46.084 E/AndroidRuntime( 4417): Caused by: java.lang.reflect.InvocationTargetException
05-10 10:59:46.084 E/AndroidRuntime( 4417):    at java.lang.reflect.Constructor.newInstance0(Native Method)
05-10 10:59:46.084 E/AndroidRuntime( 4417):    at java.lang.reflect.Constructor.newInstance(Constructor.java:334)
05-10 10:59:46.084 E/AndroidRuntime( 4417):    at android.view.LayoutInflater.createView(LayoutInflater.java:647)
05-10 10:59:46.084 E/AndroidRuntime( 4417):    at android.view.LayoutInflater.createViewFromTag(LayoutInflater.java:790)
05-10 10:59:46.084 E/AndroidRuntime( 4417):    at android.view.LayoutInflater.createViewFromTag(LayoutInflater.java:730)
05-10 10:59:46.084 E/AndroidRuntime( 4417):    at android.view.LayoutInflater.rInflate(LayoutInflater.java:863)
05-10 10:59:46.084 E/AndroidRuntime( 4417):    at android.view.LayoutInflater.rInflateChildren(LayoutInflater.java:824)
05-10 10:59:46.084 E/AndroidRuntime( 4417):    at android.view.LayoutInflater.inflate(LayoutInflater.java:515)
05-10 10:59:46.084 E/AndroidRuntime( 4417):    at android.view.LayoutInflater.inflate(LayoutInflater.java:423)
```

错误原因：没有导入recyclerview的support包

## 2 leaked serviceconnecttion
```
06-23 08:45:16.055 4478-4478/com.leeco.logpost E/ActivityThread: Activity com.ff.logpost.LogActivity has leaked IntentReceiver com.ff.iovcloud.repository.IOVCloudRepository$a$1@3daaf40 that was originally registered here. Are you missing a call to unregisterReceiver()?
    android.app.IntentReceiverLeaked: Activity com.ff.logpost.LogActivity has leaked IntentReceiver com.ff.iovcloud.repository.IOVCloudRepository$a$1@3daaf40 that was originally registered here. Are you missing a call to unregisterReceiver()?
        at android.app.LoadedApk$ReceiverDispatcher.<init>(LoadedApk.java:1351)
        at android.app.LoadedApk.getReceiverDispatcher(LoadedApk.java:1132)
        at android.app.ContextImpl.registerReceiverInternal(ContextImpl.java:1421)
        at android.app.ContextImpl.registerReceiver(ContextImpl.java:1394)
        at android.app.ContextImpl.registerReceiver(ContextImpl.java:1382)
        at android.content.ContextWrapper.registerReceiver(ContextWrapper.java:609)
        at com.ff.iovcloud.repository.IOVCloudRepository$a.v(Unknown Source:23)
        at com.ff.iovcloud.repository.IOVCloudRepository$a.d(Unknown Source:0)
        at com.ff.iovcloud.repository.IOVCloudRepository$1.a(Unknown Source:43)
        at com.ff.iovcloud.service.cloudmessage.IOVCloudMessageManager$s.onServiceConnected(Unknown Source:34)
        at android.app.LoadedApk$ServiceDispatcher.doConnected(LoadedApk.java:1652)
        at android.app.LoadedApk$ServiceDispatcher$RunConnection.run(LoadedApk.java:1681)
        at android.os.Handler.handleCallback(Handler.java:791)
        at android.os.Handler.dispatchMessage(Handler.java:99)
        at android.os.Looper.loop(Looper.java:165)
        at android.app.ActivityThread.main(ActivityThread.java:6504)
        at java.lang.reflect.Method.invoke(Native Method)
        at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:438)
        at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:807)
06-23 08:45:16.096 4478-4478/com.leeco.logpost E/ActivityThread: Activity com.ff.logpost.LogActivity has leaked ServiceConnection com.ff.iovcloud.service.cloudmessage.IOVCloudMessageManager$s@cd0e327 that was originally bound here
    android.app.ServiceConnectionLeaked: Activity com.ff.logpost.LogActivity has leaked ServiceConnection com.ff.iovcloud.service.cloudmessage.IOVCloudMessageManager$s@cd0e327 that was originally bound here
        at android.app.LoadedApk$ServiceDispatcher.<init>(LoadedApk.java:1532)
        at android.app.LoadedApk.getServiceDispatcher(LoadedApk.java:1424)
        at android.app.ContextImpl.bindServiceCommon(ContextImpl.java:1605)
        at android.app.ContextImpl.bindServiceAsUser(ContextImpl.java:1565)
        at android.content.ContextWrapper.bindServiceAsUser(ContextWrapper.java:691)
        at java.lang.reflect.Method.invoke(Native Method)
        at com.ff.iovcloud.service.cloudmessage.IOVCloudMessageManager.a(Unknown Source:33)
        at com.ff.iovcloud.service.cloudmessage.IOVCloudMessageManager.a(Unknown Source:102)
        at com.ff.iovcloud.service.cloudmessage.IOVCloudMessageManager.bindService(Unknown Source:21)
        at com.ff.iovcloud.repository.IOVCloudRepository.initializeRepository(Unknown Source:55)
        at com.ff.iovcloud.repository.IOVCloudRepository.initializeRepository(Unknown Source:1)
        at com.ff.iovcloud.repository.IOVCloudRepository.initializeRepository(Unknown Source:1)
        at com.ff.logpost.LogActivity.onResume(LogActivity.java:63)
        at android.app.Instrumentation.callActivityOnResume(Instrumentation.java:1356)
        at android.app.Activity.performResume(Activity.java:7108)
        at android.app.ActivityThread.performResumeActivity(ActivityThread.java:3559)
        at android.app.ActivityThread.handleResumeActivity(ActivityThread.java:3624)
        at android.app.ActivityThread.handleLaunchActivity(ActivityThread.java:2865)
        at android.app.ActivityThread.-wrap11(Unknown Source:0)
        at android.app.ActivityThread$H.handleMessage(ActivityThread.java:1589)
        at android.os.Handler.dispatchMessage(Handler.java:106)
        at android.os.Looper.loop(Looper.java:165)
        at android.app.ActivityThread.main(ActivityThread.java:6504)
        at java.lang.reflect.Method.invoke(Native Method)
        at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:438)
        at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:807)





06-23 07:31:50.734 D/CarNavBarController( 2428):  taskChanged: ComponentInfo{com.leeco.logpost/com.ff.logpost.LogActivity}
06-23 07:31:50.928 E/ActivityThread( 7079): Service com.ff.logpost.service.AutoPostService has leaked ServiceConnection com.ff.VehicleManager.interfaces.ClientServer$1@26f97e7 that was originally bound here
06-23 07:31:50.928 E/ActivityThread( 7079): android.app.ServiceConnectionLeaked: Service com.ff.logpost.service.AutoPostService has leaked ServiceConnection com.ff.VehicleManager.interfaces.ClientServer$1@26f97e7 that was originally bound here
06-23 07:31:50.928 E/ActivityThread( 7079): 	at com.ff.logpost.util.DriveModule.<init>(DriveModule.java:73)
06-23 07:31:50.928 E/ActivityThread( 7079): 	at com.ff.logpost.util.DriveModule.getInstance(DriveModule.java:65)
06-23 07:31:50.928 E/ActivityThread( 7079): 	at com.ff.logpost.core.LogPost.zipAndPost(LogPost.java:58)
06-23 07:31:50.928 E/ActivityThread( 7079): 	at com.ff.logpost.core.LogPost.startLogPost(LogPost.java:51)
06-23 07:31:50.928 E/ActivityThread( 7079): 	at com.ff.logpost.service.AutoPostService.startNorLogPost(AutoPostService.java:55)
06-23 07:31:50.928 E/ActivityThread( 7079): 	at com.ff.logpost.service.AutoPostService.-wrap0(Unknown Source:0)
06-23 07:31:50.928 E/ActivityThread( 7079): 	at com.ff.logpost.service.AutoPostService$1.accept(AutoPostService.java:33)
06-23 07:31:50.928 E/ActivityThread( 7079): 	at com.ff.logpost.service.AutoPostService$1.accept(AutoPostService.java:31)
06-23 07:31:50.931 I/com.leeco.logpost( 7079): android::hardware::configstore::V1_0::ISurfaceFlingerConfigs::hasWideColorDisplay retrieved: 0
06-23 07:31:51.040 I/ActivityManager(  710): Displayed com.leeco.logpost/com.ff.logpost.LogActivity: +425ms (total +863ms)
```

## 3crash
```
05-28 12:48:25.546 9726-9726/com.ff.logpost E/AndroidRuntime: FATAL EXCEPTION: main
    Process: com.ff.logpost, PID: 9726
    java.lang.IllegalArgumentException: Activity LogActivity does not have a parent activity name specified. (Did you forget to add the android.support.PARENT_ACTIVITY <meta-data>  element in your manifest?)
        at android.support.v4.app.NavUtils.navigateUpFromSameTask(NavUtils.java:81)
        at com.ff.logpost.LogActivity.onOptionsItemSelected(LogActivity.java:23)
        at android.app.Activity.onMenuItemSelected(Activity.java:3451)
        at android.support.v4.app.FragmentActivity.onMenuItemSelected(FragmentActivity.java:373)
        at android.support.v7.app.AppCompatActivity.onMenuItemSelected(AppCompatActivity.java:195)
        at android.support.v7.view.WindowCallbackWrapper.onMenuItemSelected(WindowCallbackWrapper.java:108)
        at android.support.v7.view.WindowCallbackWrapper.onMenuItemSelected(WindowCallbackWrapper.java:108)
        at android.support.v7.widget.ToolbarWidgetWrapper$1.onClick(ToolbarWidgetWrapper.java:187)
        at android.view.View.performClick(View.java:6339)
        at android.view.View$PerformClick.run(View.java:24823)
        at android.os.Handler.handleCallback(Handler.java:791)
        at android.os.Handler.dispatchMessage(Handler.java:99)
        at android.os.Looper.loop(Looper.java:165)
        at android.app.ActivityThread.main(ActivityThread.java:6504)
        at java.lang.reflect.Method.invoke(Native Method)
        at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:438)
        at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:807)
 ```

 ## 4
 ```
 Caused by: java.lang.ClassNotFoundException: Didn't find class "com.ff.logpost.StartActivity" on path: DexPathList[[zip file "/system/priv-app/FFLogPost/FFLogPost.apk"],nativeLibraryDirectories=[/system/priv-app/FFLogPost/lib/arm64, /system/lib64, /vendor/lib64, /system/lib64, /vendor/lib64]]
        at dalvik.system.BaseDexClassLoader.findClass(BaseDexClassLoader.java:125)
        at java.lang.ClassLoader.loadClass(ClassLoader.java:379)
        at java.lang.ClassLoader.loadClass(ClassLoader.java:312)
        at android.app.Instrumentation.newActivity(Instrumentation.java:1175)
        at android.app.ActivityThread.performLaunchActivity(ActivityThread.java:2669)
        at android.app.ActivityThread.handleLaunchActivity(ActivityThread.java:2859) 
        at android.app.ActivityThread.-wrap11(Unknown Source:0) 
        at android.app.ActivityThread$H.handleMessage(ActivityThread.java:1589) 
        at android.os.Handler.dispatchMessage(Handler.java:106) 
        at android.os.Looper.loop(Looper.java:165) 
        at android.app.ActivityThread.main(ActivityThread.java:6504) 
        at java.lang.reflect.Method.invoke(Native Method) 
        at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:438) 
        at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:807) 
```