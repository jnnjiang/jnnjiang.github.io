---
title: Android plurals源码分析
permalink: android-source-plurals
comments: true
toc: false
date: 2019-03-21 14:59:03
updated: 2019-03-21 14:59:03
tags:
    - plurals
    - 本地化
categories:
    - Android
    - 源码分析
---
由于不同语言对数量的语法规则不同，所以引入了plurals这种资源，plurals中quality的值有zero,one,two,few,many,和other，当时我们发现，有时我们定义的有些quality在调用是并不能得到预期的结果，这是因为不是所有的语言都能支持所有的quality值，而在我们调用`getQuantityString(@PluralsRes int id, int quantity)`方式时，系统是怎么返回的，需要从源码着手去分析。

我们从Android 8.0中frameworks/base/core/java/android/content/res/Resources.java的代码入手：
<!-- more -->
```
@NonNull
public String getQuantityString(@PluralsRes int id, int quantity, Object... formatArgs)
        throws NotFoundException {
    //容易看出，先根据quantity决定要使用的字符串
    String raw = getQuantityText(id, quantity).toString();

    //再进行占位符的替换工作
    return String.format(mResourcesImpl.getConfiguration().getLocales().get(0), raw,
            formatArgs);
}

@NonNull
public CharSequence getQuantityText(@PluralsRes int id, int quantity)
        throws NotFoundException {
    //依赖于ResourceImpl的实现
    return mResourcesImpl.getQuantityText(id, quantity);
}
```
跟进ResourceImpl中的getQuantityText函数：
```
CharSequence getQuantityText(@PluralsRes int id, int quantity) throws NotFoundException {
    //得到规则
    PluralRules rule = getPluralRule();

    //rule.select根据规则，得到quantity对应的QuanitiyCode，即"zero"、"one"、"other"等
    //之后再根据QuanitiyCode，的到具体的资源文件
    CharSequence res = mAssets.getResourceBagText(id,
            attrForQuantityCode(rule.select(quantity)));
    if (res != null) {
        return res;
    }

    //rule没能找到对应的QuanitiyCode时，就用"other"字段的定义
    res = mAssets.getResourceBagText(id, ID_OTHER);
    if (res != null) {
        return res;
    }

    //上面寻找资源文件出问题，就抛出异常
    throw new NotFoundException("Plural resource ID #0x" + Integer.toHexString(id)
        + " quantity=" + quantity
        + " item=" + rule.select(quantity));
}
```
这里我们首先看一下getPluralRule函数：
```
private PluralRules getPluralRule() {
    synchronized (sSync) {
        if (mPluralRule == null) {
            //单例模式，以Locales的第一个配置来初始化规则，而Locales中的第一个即为当前系统的语言，故和本地化有关。
            mPluralRule = PluralRules.forLocale(mConfiguration.getLocales().get(0));
        }
        return mPluralRule;
    }
}
```
PluralRules的select函数对应的底层实现，不同的Locales应该有不同的实现。

在此看看attrForQuantityCode：
```
private static int attrForQuantityCode(String quantityCode) {
    switch (quantityCode) {
        case PluralRules.KEYWORD_ZERO: return 0x01000005;
        case PluralRules.KEYWORD_ONE:  return 0x01000006;
        case PluralRules.KEYWORD_TWO:  return 0x01000007;
        case PluralRules.KEYWORD_FEW:  return 0x01000008;
        case PluralRules.KEYWORD_MANY: return 0x01000009;
        default:                       return ID_OTHER;
    }
}
```
从上面的代码可以看出，PluralRules的select函数的作用，就是将quantity映射成PluralRules定义的Keyword。 
然后attrForQuantityCode将Keyword转化成资源文件能识别的标志。

