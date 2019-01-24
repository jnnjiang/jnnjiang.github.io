---
title: android-strings
permalink: android-strings
toc: false
date: 2019-01-24 17:53:10
tags:
categories:
---

string test:
```
 private static final String TAG = "PluralsTest";
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        Log.d(TAG,getResources().getQuantityString(R.plurals.time,0,0));
        Log.d(TAG,getResources().getQuantityString(R.plurals.time,1,1));
        Log.d(TAG,getResources().getQuantityString(R.plurals.time,5,5));

        Log.d(TAG,getResources().getString(R.string.old,"Lily",28));
        Log.d(TAG,getResources().getString(R.string.old2,"Lily",28));
        String str =getResources().getString(R.string.old_);
        String string = str.format(str, "李小姐",27);
        Log.d(TAG,"string = "+string);

        String fmt1 = getResources().getText(R.string.item_shop).toString();
        MessageFormat.format(fmt1, 0);
        Log.d(TAG,MessageFormat.format(fmt1, 0));
        Log.d(TAG,MessageFormat.format(fmt1, 1));
        Log.d(TAG,MessageFormat.format(fmt1, 8));
        Log.d(TAG,"=============");
        ChoiceFormat format = new ChoiceFormat("-1#is negative| 0#is zero or fraction | 1#is one |1.0<is 1+ |2#is two |2<is more than 2.");
        Log.d(TAG,format.format(0));
        Log.d(TAG,format.format(1));
        Log.d(TAG,format.format(1.1));
        Log.d(TAG,format.format(2));
        Log.d(TAG,format.format(3));
        Log.d(TAG,"=============");

        String fmt = "0#No items|1<{0} items";
        ChoiceFormat form = new ChoiceFormat(fmt);
        Log.d(TAG,form.format(0));
        Log.d(TAG,form.format(1));
        Log.d(TAG,form.format(2));

        String text = getString(R.string.welcome_messages, "nana", 24);
        if (android.os.Build.VERSION.SDK_INT >= android.os.Build.VERSION_CODES.N) {
            Spanned styledText = Html.fromHtml(text, FROM_HTML_MODE_LEGACY);
            Log.d(TAG,"text = "+styledText.toString());
        }


        String escapedUsername = TextUtils.htmlEncode("<fdf&");
        Log.d(TAG,"escapedUsername = "+escapedUsername);
        String text1 = getString(R.string.welcome_messages, escapedUsername, 44);
        Spanned styledText1 = Html.fromHtml(text1);
        Log.d(TAG,"text1 = "+styledText1.toString());

        //For instance, if you are formatting a string that contains characters such as "<" or "&",
         // then they must be escaped before formatting
        String text2 = getString(R.string.welcome_messages, "<fdf&", 44);
        Spanned styledText = Html.fromHtml(text2);
        Log.d(TAG,"text2 = "+styledText.toString());
    }
```

strings.xml
```
<resources xmlns:xliff="urn:oasis:names:tc:xliff:document:1.2">
    <string name="app_name" translatable="false">PluralsTest</string>
    <plurals name="time">
        <item quantity="zero"></item>
        <item quantity="one">%d hour</item>
        <item quantity="other">%d hours</item>
    </plurals>

    <plurals name="item">
        <item quantity="zero">No item</item>
        <item quantity="one">One item</item>
        <item quantity="other">%d items</item>
    </plurals>

    <string name="old">%1$s,%2$dyears old</string>
    <string name="old2">%1$s,%2$5dyears old</string>

    <string name="old_"><xliff:g id="name">%1$s</xliff:g>,<xliff:g id="age">%2$d</xliff:g>years old</string>

    <string name="item_shop">{0,choice,0#No items|1#One item|1&lt;{0} items}</string>
    <string name="welcome_messages">Hello, %1$s! You have %2$d new messages.</string>
</resources>
```
string.xml in zh-rCN
```
<resources xmlns:xliff="urn:oasis:names:tc:xliff:document:1.2">
    <string name="app_name">PluralsTest</string>
    <plurals name="time">
        <item quantity="zero"></item>
        <item quantity="one">%d 小时</item>
        <item quantity="other">%d 小时</item>
    </plurals>

    <plurals name="item">
        <item quantity="zero">没有</item>
        <item quantity="other">%d条</item>
    </plurals>

    <string name="old">%1$s今年%2$d岁了</string>
    <string name="old2">%1$s今年%2$5d岁了</string>

    <string name="old_"><xliff:g id="name">%1$s</xliff:g>今年<xliff:g id="age">%2$d</xliff:g>岁了</string>
    <string name="item_shop">{0,choice,0#没有|1#1条|1&lt;{0} 条}</string>

    <string name="welcome_messages">你好, %1$s! 你有 %2$d 条新消息.</string>
</resources>
```