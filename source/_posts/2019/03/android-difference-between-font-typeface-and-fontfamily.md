---
title: android Font,Typeface,FontFamily之间的差别
permalink: android-difference-between-font-typeface-and-fontfamily
comments: true
toc: false
date: 2019-03-20 22:36:47
updated: 2019-03-20 22:36:47
tags:
    - 字体
categories:
    - Android
    - 字体
---

# 背景
Font和Typeface经常被错误的互换使用。然而它们之间却是有一些不同的。
# Font
大约在十五世纪，当打印机手工打字时，他们必须从一个巨大的盒子里拿出真正的金属字母、数字和符号。如下图：
![图1](https://mindgruve.com/wp/wp-content/uploads/2013/05/xmetal-font-box.jpg.pagespeed.ic.KY10H3va6i.webp)
图1

这个收集字符的容器可以被叫做`Font`
现在，`font`指的是包含各种字体的数字文件，而不是一盒金属字体。
<!-- more -->

# Typeface
![图2](https://mindgruve.com/wp/wp-content/uploads/2013/05/xnews-gothic-2.png.pagespeed.ic.MInj5TZxF_.webp)
图2

Typeface描述了字体中包含的字符的整体外观。如图2是一种New Gothic字体（Font）。
> 你可能有一个容器装的是News Gothic字体，有一个容器装的是News Gothic Bold字体，一个容器装News Gothic Light字体，每个容器里都是一种News Gothic字体。
它们只是拥有不同的厚度（weight），但其定义的特征仍然是相同的。

下图或许可以很好的解释Typeface：
![图3](https://mindgruve.com/wp/wp-content/uploads/2013/05/xsmith-font-family-2.png.pagespeed.ic.Nr7dxeCJM0.webp)
图3

`typeface`通常可以和`font family`互换。再举个例子：
> 一个家庭有三胞胎：John Smith, Jack Smith, and Tom Smith。他们拥有相同的样貌，但是体重（weight）不同：一个瘦点儿，另一个胖点儿。他们一起组成了`Smith family`。

在印刷术上，John，Jack，Tom代表着不同的字体，但是他们一起组成了`Smith Typeface`

# Font Family
在Android中，`font family`是一组相关字体的集体，例如Arial字体，那么`font family`将包含`Arial regular`，`Arial Bold`，`Arial Itatic`，`Arial Bold Itatic`，`Arial Black`等字体。

总之：`typeface`是一种设计，`font`是一个文件，`font family`是一个相关字体的文件集合。


参考：
[Typeface vs Font: What’s the Difference?](https://mindgruve.com/blog/advertising/typeface-vs-font-what-is-the-difference)
[What’s the Difference Between a Font, a Typeface, and a Font Family?](https://www.howtogeek.com/325644/whats-the-difference-between-a-font-a-typeface-and-a-font-family/)