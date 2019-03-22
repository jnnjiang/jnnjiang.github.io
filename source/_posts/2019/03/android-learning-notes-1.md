---
title: android 学习笔记(1)—TextView 文本样式
permalink: android-learning-notes-1
comments: true
toc: true
date: 2019-03-22 09:56:24
updated: 2019-03-22 09:56:24
tags:
categories:
    - Android
    - TextView
---

在Android中，TextView中文本的样式
在Android中，TextView是一个非常重要的控件，用于显示文本，通常我们会在XML文件中使用`android:text`属性来设置文本，也可以在代码中通过调用`textView.setText()`方法来设置文本，这种方式设置的文本样式默认是使用robot字体的normal样式。有时因为需求，我们需要改变字体的样式，包括颜色、缩放、可点击性，删除线等，有时需要对TextView中所有的文本设置样式，有时只是需要更改其中某些字体的样式，下面针对不同的需要做下总结。

## 粗体
### 整体加粗
可以使用XML属性、styles、或者themes，也可以使用`Spans`或`HTML`标签
在XML文件中使用`android:textStyle="bold"`属性
``` XML
<TextView
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:textSize="32sp"
    android:textStyle="bold"
    />
```

或在代码中修改`Typeface`
```java
myTextView.setTypeface(Typeface.create(myTextView.getTypeface(),Typeface.BOLD));
```

或在代码中使用`StyleSpan`
```java
SpannableString string = new SpannableString("Text with\nBullet point");
string.setSpan(new StyleSpan(Typeface.BOLD),0,string.length(),Spanned.SPAN_EXCLUSIVE_EXCLUSIVE);
myTextView.setText(string);
```

或在代码中使用`HTML`标签
```HTML
String textBold = "<b>text bold</b>";
myTextView.setText(Html.fromHtml(textBold));
```

### 部分加粗
可以用`HTML`标签、`Spans`或者直接重写TextView的onDraw()方法绘制text。

## 单一样式 —— 单一样式用于整个TextView中文本
单一样式我们可以通过使用XML属性、styles、或者themes

## 使用XML属性
例如：将字体设为粗体，我们可以使用`android:textStyle="bold"`

```XML
<TextView
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:textSize="32sp"
    android:textStyle="bold"
    />
```

## 多种样式 —— 多种样式用于文本、字符或片段等
多种样式可以通过HTML标签、Spans或者自定TextView中text的绘制
## 使用HTML标签
Java：
```Java
String text = "My text <ul><li>bullet one</li><li>bullet two</li></ul>";
myTextView.setText(Html.fromHtml(text));
```

Kotlin：
```Kotlin
val text = "My text <ul><li>bullet one</li><li>bullet two</li></ul>"
myTextView.text = Html.fromHtml(text)
```
## 使用Spans
Spans允许你实现多种样式的text
例如：您可以利用BulletSpan自定义文本边距、项目符号和项目符号颜色之间的间隙。从android p开始，你甚至可以设置BulletSpan的半径。
Java
```Java
SpannableString spannable = new SpannableString("My text \nbullet one\nbullet two");
spannable.setSpan(
    new BulletSpan(gapWidthPx, accentColor),
    /* start index */ 9, /* end index */ 18,
    Spannable.SPAN_EXCLUSIVE_EXCLUSIVE);
spannable.setSpan(
     new BulletSpan(gapWidthPx, accentColor),
     /* start index */ 20, /* end index */ spannable.length(),
     Spannable.SPAN_EXCLUSIVE_EXCLUSIVE);
myTextView.setText(spannable);
```
Kotlin
```Kotlin
val spannable = SpannableString("My text \nbullet one\nbullet two")
spannable.setSpan(
    BulletSpan(gapWidthPx, accentColor),
    /* start index */ 9, /* end index */ 18,
    Spannable.SPAN_EXCLUSIVE_EXCLUSIVE)
spannable.setSpan(
     BulletSpan(gapWidthPx, accentColor),
     /* start index */ 20, /* end index */ spannable.length,
     Spannable.SPAN_EXCLUSIVE_EXCLUSIVE)
myTextView.text = spannable
```
在Android P中甚至可以设置BulletSpan的半径：
Java code：
```Java
SpannableString spannable = new SpannableString("My text \nbullet one\nbullet two");
spannable.setSpan(
    new BulletSpan(gapWidthPx, accentColor),
    /* start index */ 9, /* end index */ 18,
    Spannable.SPAN_EXCLUSIVE_EXCLUSIVE);
spannable.setSpan(
     new BulletSpan(gapWidthPx, accentColor, bulletRadius),
     /* start index */ 20, /* end index */ spannable.length(),
     Spannable.SPAN_EXCLUSIVE_EXCLUSIVE);
myTextView.setText(spannable);
```
Kotlin code：
Kotlin
```Kotlin
val spannable = SpannableString("My text \nbullet one\nbullet two")
spannable.setSpan(
    BulletSpan(gapWidthPx, accentColor),
    /* start index */ 9, /* end index */ 18,
    Spannable.SPAN_EXCLUSIVE_EXCLUSIVE)
spannable.setSpan(
     BulletSpan(gapWidthPx, accentColor, bulletRadius),
     /* start index */ 20, /* end index */ spannable.length,
     Spannable.SPAN_EXCLUSIVE_EXCLUSIVE)
myTextView.text = spannable
```

## 单一样式和多种样式可以混合使用
``` XML
<TextView
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:textColor="@color/blue"/>
```
```Kotlin
val spannable = SpannableString(“Text styling”)
spannable.setSpan(
     ForegroundColorSpan(Color.PINK), 
     0, 4, 
     Spannable.SPAN_EXCLUSIVE_EXCLUSIVE)
myTextView.text = spannable
```

非常好的文章
<https://medium.com/androiddevelopers/spantastic-text-styling-with-spans-17b0c16b4568>