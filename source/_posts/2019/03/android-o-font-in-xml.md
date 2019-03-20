---
title: android O 在xml文件中引用字体
permalink: android-o-font-in-xml
comments: true
toc: false
date: 2019-03-20 16:23:02
updated: 2019-03-20 16:23:02
tags:
categories:
    - Android
    - 字体
---

# 背景
Android 8.0（API 26 Oreo）引入了可以在xml文件中配置字体的新功能，在这之前，如果要改变字体样式，需要将字体文件放入Asset文件中，并在代码代码中通过getAsset()的方式，动态改变字体的样式。如果想在4.1（API 16）及更高的版本上使用该功能，需要引用Support Library 26.

# Android O在xml文件中配置字体
## 本地字体
### 直接在xml文件中引用字体
1.在`res/`文件夹下创建`font`文件夹，并将字体文件拷到`font`文件夹下，假设字体文件为：`myfont.otf`
2.在xml文件中通过`android:fontFamily`属性引用自定义的字体
```
<TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Text View"
        android:fontFamily="@font/myfont"/>
```
注：font文件名字只能由小写字母a-z，0-9，下划线_组成。
<!-- more -->
### 创建font family

字体系列是一组字体文件及其样式和权重详细信息。在Android中，您可以创建一个新的字体系列作为XML资源，并将其作为单个单元访问，而不是将每个样式和权重作为单独的资源引用。通过这样做，系统可以根据您尝试使用的文本样式选择正确的字体。（这里有个疑问，系统是怎么匹配字体的？？？）
1.在`res/font/`路径下，右键新建资源文件`lobster.xml`
2.打开此xml文件定义该字体的所有不同版本，以及其样式和权重属性：
```
<?xml version="1.0" encoding="utf-8"?>
<font-family xmlns:android="http://schemas.android.com/apk/res/android">
    <font
        android:fontStyle="normal"
        android:fontWeight="400"
        android:font="@font/lobster_regular" />
    <font
        android:fontStyle="italic"
        android:fontWeight="400"
        android:font="@font/lobster_italic" />
</font-family>
```
2.然后在xml文件像引用普通字体一样引用字体文件：
```
<TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:fontFamily="@font/lobster"/>
```
### 把font添加到style文件中
```
<style name="MyTextAppearance" parent="@android:style/TextAppearance.Small">
    <item name="android:fontFamily">@font/lobster</item>
</style>
```
### 在代码中使用font
```
Typeface typeface = getResources().getFont(R.font.myfont);
textView.setTypeface(typeface);
```

### 利用Support Library兼容至版本4.1版本（兼容到API 14，因为android:fontFamily是Android 4.1版本引入的）
1. 在`app/build.gragle`添加dependencies：
```
implementation 'com.android.support:appcompat-v7:26.0.0'
```
2. 创建font family文件
```
<?xml version="1.0" encoding="utf-8"?>
<font-family xmlns:app="http://schemas.android.com/apk/res-auto">
    <font app:fontStyle="normal" app:fontWeight="400" app:font="@font/myfont-Regular"/>
    <font app:fontStyle="italic" app:fontWeight="400" app:font="@font/myfont-Italic" />
</font-family>
```
注：需要用到app属性
3. 字体的引用同系统API
4. 在代码中引用字体
```
Typeface typeface = ResourcesCompat.getFont(context, R.font.myfont);
```
主要需要用到ResourcesCompat类。

### 4.1之前的版本自定义字体（只能通过代码引用）
1.在项目根目录下，新建`assets/fonts/`文件夹
2.将字体拷贝至文件夹下
3.在代码中引用
```
Typeface tf = Typeface.createFromAsset(getContext().getAssets(), "fonts/myfont.ttf"); 
TextViev textView = findViewById(R.id.textview);
textView.setTypeface(tf);
```

### 总结：
鉴于以上两种情况，font family文件可以定义成兼容模式（由于现在兼容到4.1版本已经可以覆盖所有的设备，故不再考虑4.1之前的版本）
```
<font-family 
xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:app="http://schemas.android.com/apk/res-auto">
<font
        android:fontStyle="normal"
        android:fontWeight="400"
        android:font="@font/lobster_regular"
        app:fontStyle="normal"
        app:fontWeight="400"
        app:font="@font/lobster_regular" />
    
    <font
        android:fontStyle="italic"
        android:fontWeight="400"
        android:font="@font/lobster_italic"
        app:fontStyle="italic"
        app:fontWeight="400"
        app:font="@font/lobster_italic" />

</font-family>
```
## 在线字体
### 静态配置
打开 `app/src/main/res/layout/activity_main.xml`
选择 `Design` 面板
在 `Component Tree` 面板中, 打开 textview
在 `Attributes` 面板中, 打开 fontFamily 下拉列表并选择 More Fonts… （你可能需要点击 `View all attributes`才能看到 fontFamily）
选择字体家族 eg.`Adamina`
选择字体样式 eg.`Regular`
勾选`Create downloadable font`（如果勾选`add font to project`，字体将直接被下载到`res/font/`下）
点击OK，此时在`res/font/`下就会有我们想下载的字体。

此时我们的项目会有如下变化
1. res/font/下多了Adamina.xml文件
```
<?xml version="1.0" encoding="utf-8"?>
<font-family xmlns:app="http://schemas.android.com/apk/res-auto"
        app:fontProviderAuthority="com.google.android.gms.fonts"
        app:fontProviderPackage="com.google.android.gms"
        app:fontProviderQuery="Adamina"
        app:fontProviderCerts="@array/com_google_android_gms_fonts_certs">
</font-family>
```
<font color=#f00>app:fontProviderFetchStrategy="blocking" 属性的作用？？？</font>
2. `res/values/`下增加了`font_certs.xml`和`preloaded_fonts.xml`
**font_certs.xml**:字体提供程序的签名
```
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <array name="com_google_android_gms_fonts_certs">
        <item>@array/com_google_android_gms_fonts_certs_dev</item>
        <item>@array/com_google_android_gms_fonts_certs_prod</item>
    </array>
    <string-array name="com_google_android_gms_fonts_certs_dev">
        <item>
            MIIEqDCCA5CgAwIBAgIJANWFuGx90071MA0GCSqGSIb3DQEBBAUAMIGUMQswCQYDVQQGEwJVUzETMBEGA1UECBMKQ2FsaWZvcm5pYTEWMBQGA1UEBxMNTW91bnRhaW4gVmlldzEQMA4GA1UEChMHQW5kcm9pZDEQMA4GA1UECxMHQW5kcm9pZDEQMA4GA1UEAxMHQW5kcm9pZDEiMCAGCSqGSIb3DQEJARYTYW5kcm9pZEBhbmRyb2lkLmNvbTAeFw0wODA0MTUyMzM2NTZaFw0zNTA5MDEyMzM2NTZaMIGUMQswCQYDVQQGEwJVUzETMBEGA1UECBMKQ2FsaWZvcm5pYTEWMBQGA1UEBxMNTW91bnRhaW4gVmlldzEQMA4GA1UEChMHQW5kcm9pZDEQMA4GA1UECxMHQW5kcm9pZDEQMA4GA1UEAxMHQW5kcm9pZDEiMCAGCSqGSIb3DQEJARYTYW5kcm9pZEBhbmRyb2lkLmNvbTCCASAwDQYJKoZIhvcNAQEBBQADggENADCCAQgCggEBANbOLggKv+IxTdGNs8/TGFy0PTP6DHThvbbR24kT9ixcOd9W+EaBPWW+wPPKQmsHxajtWjmQwWfna8mZuSeJS48LIgAZlKkpFeVyxW0qMBujb8X8ETrWy550NaFtI6t9+u7hZeTfHwqNvacKhp1RbE6dBRGWynwMVX8XW8N1+UjFaq6GCJukT4qmpN2afb8sCjUigq0GuMwYXrFVee74bQgLHWGJwPmvmLHC69EH6kWr22ijx4OKXlSIx2xT1AsSHee70w5iDBiK4aph27yH3TxkXy9V89TDdexAcKk/cVHYNnDBapcavl7y0RiQ4biu8ymM8Ga/nmzhRKya6G0cGw8CAQOjgfwwgfkwHQYDVR0OBBYEFI0cxb6VTEM8YYY6FbBMvAPyT+CyMIHJBgNVHSMEgcEwgb6AFI0cxb6VTEM8YYY6FbBMvAPyT+CyoYGapIGXMIGUMQswCQYDVQQGEwJVUzETMBEGA1UECBMKQ2FsaWZvcm5pYTEWMBQGA1UEBxMNTW91bnRhaW4gVmlldzEQMA4GA1UEChMHQW5kcm9pZDEQMA4GA1UECxMHQW5kcm9pZDEQMA4GA1UEAxMHQW5kcm9pZDEiMCAGCSqGSIb3DQEJARYTYW5kcm9pZEBhbmRyb2lkLmNvbYIJANWFuGx90071MAwGA1UdEwQFMAMBAf8wDQYJKoZIhvcNAQEEBQADggEBABnTDPEF+3iSP0wNfdIjIz1AlnrPzgAIHVvXxunW7SBrDhEglQZBbKJEk5kT0mtKoOD1JMrSu1xuTKEBahWRbqHsXclaXjoBADb0kkjVEJu/Lh5hgYZnOjvlba8Ld7HCKePCVePoTJBdI4fvugnL8TsgK05aIskyY0hKI9L8KfqfGTl1lzOv2KoWD0KWwtAWPoGChZxmQ+nBli+gwYMzM1vAkP+aayLe0a1EQimlOalO762r0GXO0ks+UeXde2Z4e+8S/pf7pITEI/tP+MxJTALw9QUWEv9lKTk+jkbqxbsh8nfBUapfKqYn0eidpwq2AzVp3juYl7//fKnaPhJD9gs=
        </item>
    </string-array>
    <string-array name="com_google_android_gms_fonts_certs_prod">
        <item>
            MIIEQzCCAyugAwIBAgIJAMLgh0ZkSjCNMA0GCSqGSIb3DQEBBAUAMHQxCzAJBgNVBAYTAlVTMRMwEQYDVQQIEwpDYWxpZm9ybmlhMRYwFAYDVQQHEw1Nb3VudGFpbiBWaWV3MRQwEgYDVQQKEwtHb29nbGUgSW5jLjEQMA4GA1UECxMHQW5kcm9pZDEQMA4GA1UEAxMHQW5kcm9pZDAeFw0wODA4MjEyMzEzMzRaFw0zNjAxMDcyMzEzMzRaMHQxCzAJBgNVBAYTAlVTMRMwEQYDVQQIEwpDYWxpZm9ybmlhMRYwFAYDVQQHEw1Nb3VudGFpbiBWaWV3MRQwEgYDVQQKEwtHb29nbGUgSW5jLjEQMA4GA1UECxMHQW5kcm9pZDEQMA4GA1UEAxMHQW5kcm9pZDCCASAwDQYJKoZIhvcNAQEBBQADggENADCCAQgCggEBAKtWLgDYO6IIrgqWbxJOKdoR8qtW0I9Y4sypEwPpt1TTcvZApxsdyxMJZ2JORland2qSGT2y5b+3JKkedxiLDmpHpDsz2WCbdxgxRczfey5YZnTJ4VZbH0xqWVW/8lGmPav5xVwnIiJS6HXk+BVKZF+JcWjAsb/GEuq/eFdpuzSqeYTcfi6idkyugwfYwXFU1+5fZKUaRKYCwkkFQVfcAs1fXA5V+++FGfvjJ/CxURaSxaBvGdGDhfXE28LWuT9ozCl5xw4Yq5OGazvV24mZVSoOO0yZ31j7kYvtwYK6NeADwbSxDdJEqO4k//0zOHKrUiGYXtqw/A0LFFtqoZKFjnkCAQOjgdkwgdYwHQYDVR0OBBYEFMd9jMIhF1Ylmn/Tgt9r45jk14alMIGmBgNVHSMEgZ4wgZuAFMd9jMIhF1Ylmn/Tgt9r45jk14aloXikdjB0MQswCQYDVQQGEwJVUzETMBEGA1UECBMKQ2FsaWZvcm5pYTEWMBQGA1UEBxMNTW91bnRhaW4gVmlldzEUMBIGA1UEChMLR29vZ2xlIEluYy4xEDAOBgNVBAsTB0FuZHJvaWQxEDAOBgNVBAMTB0FuZHJvaWSCCQDC4IdGZEowjTAMBgNVHRMEBTADAQH/MA0GCSqGSIb3DQEBBAUAA4IBAQBt0lLO74UwLDYKqs6Tm8/yzKkEu116FmH4rkaymUIE0P9KaMftGlMexFlaYjzmB2OxZyl6euNXEsQH8gjwyxCUKRJNexBiGcCEyj6z+a1fuHHvkiaai+KL8W1EyNmgjmyy8AW7P+LLlkR+ho5zEHatRbM/YAnqGcFh5iZBqpknHf1SKMXFh4dd239FJ1jWYfbMDMy3NS5CTMQ2XFI1MvcyUTdZPErjQfTbQe3aDQsQcafEQPD+nqActifKZ0Np0IS9L9kR/wbNvyz6ENwPiTrjV2KRkEjH78ZMcUQXg0L3BYHJ3lc69Vs5Ddf9uUGGMYldX3WfMBEmh/9iFBDAaTCK
        </item>
    </string-array>
</resources>
```
**preloaded_fonts.xml**:在安装和更新过程中加载的字体列表，以确保这些字体在启动应用程序时可用。
```
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <array name="preloaded_fonts" translatable="false">
        <item>@font/adamina</item>
    </array>
</resources>
```
3. AndroidManifest.xml文件中增加字体的meta-data信息 (<font color=#f00>meta-data信息的作用？？？？</font>)
```
 <meta-data
            android:name="preloaded_fonts"
            android:resource="@array/preloaded_fonts" />
```

### 动态加载
1. 我们需要一个线程等待字体，声明一个变量以保存：
```
private Handler fontHandler;
```
2. 添加一个 Method 来管理字体处理线程：
```
private Handler getFontHandlerThread() {
   if (fontHandler == null) {
       HandlerThread handlerThread = new HandlerThread("fonts");
       handlerThread.start();
       fontHandler = new Handler(handlerThread.getLooper());
   }
   return fontHandler;
}
```
3. 添加一个 Method 将 Typeface (参考 ) 应用于 Toolbar：
```
private void styleToolbar(Typeface typeface) {
   // this is gross but toolbar doesn't expose it's children
   for (int i = 0; i < toolbar.getChildCount(); i++) {
       View rawView = toolbar.getChildAt(i);
       if (!(rawView instanceof TextView)) {
           continue;
       }
TextView textView = (TextView) rawView;
       textView.setTypeface(typeface);
   }
}
```
4. 在 onCreate 中，从字体提供程序启动异步获取：
```
@Override
protected void onCreate(Bundle savedInstanceState) {
  ...
   FontRequest fontRequest = new FontRequest("com.google.android.gms.fonts",
           "com.google.android.gms",
           "name=Adamina",
           R.array.font_certs);
   FontsContractCompat.FontRequestCallback toolbarFontCallback =
           new FontsContractCompat.FontRequestCallback() {
               @Override public void onTypefaceRetrieved(Typeface typeface) {
                   // If we got our font apply it to the toolbar
                   styleToolbar(typeface);
               }
               @Override public void onTypefaceRequestFailed(int reason) {
                   Log.w(TAG, "Failed to fetch Toolbar font: " + reason);
               }
           };
  
   // Start async fetch on the handler thread
   FontsContractCompat.requestFont(this, fontRequest, toolbarFontCallback,
           getFontHandlerThread());
```
关于字体，想了解更多的，可以查看[Android 字体](https://jnnjiang.github.io/2019/03/18/android/font/android-font.html)