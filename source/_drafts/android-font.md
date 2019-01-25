---
title: android-font
permalink: android-font
toc: false
date: 2019-01-25 10:04:09
tags:
categories:
---
最近了解了一下字体，发现彻底解释明白这件事情真的很不容易。

## android:fontWeight属性
值是int，范围是1~1000，系统默认字体的weight是400
常用属性值和通常的名字对应关系如下
| Value | Common weight name |
|-------|--------------------|
|100    |thin
|200	|Extra Light
|300	|Light
|400	|Normal
|500	|Medium
|600	|Semi Bold
|700	|Bold
|800	|Extra Bold
|900	|Black

## 从Android 7.0开始，支持通过资源文件的方式引用字库


通常我们在xml文件用引用字体，都是修改一下几个属性
```
```

西方国家字母体系分为两类：衬线字体（serif）以及无衬线体（sans serif）。
衬线字体，意思是在字的笔画开始、结束的地方有额外的装饰，而且笔画的粗细会有所不同。
无衬线体是无衬线字体，没有这些额外的装饰，而且笔画的粗细差不多。