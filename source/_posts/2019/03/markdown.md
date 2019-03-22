---
title: Markdown教程
permalink: Markdown
toc: true
date: 2019-03-20 12:34:54
tags:
    - Markdown
categories:
    - Markdown
---

-----
# 基础篇
-----
## 标题
```
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
```
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题

<!-- more -->
## 文本样式
```
- 链接：[title](url)
- 加粗：**文本**
- 斜体：*ABC*
- 高亮：==高亮==
- 段落：段落之间空一行
- 换行符：一行结束时输入两个空格
- 列表：
    - 无序列表
    - 有序列表
- 引用： >引用内容
- 内嵌代码：`code`
- 分割线：---或***或===
- 方框： - [ ] -
```
- 链接：[title](url)
- 加粗：**文本**
- 斜体：*ABC*
- 粗斜体：***粗斜体文本***
- 高亮：==高亮==
- 段落：段落之间空一行
- 换行符：一行结束时输入两个空格
- 列表：
    - 无序列表
    - 有序列表
- 引用： >引用内容
- 内嵌代码：`code`
- 分割线：----或****或===
- 方框：- [ ] -

## 有序列表
数字不能省略但可无序，点号之后的空格不能少
```
1. 第一项
2. 第二项
3. 第三项
5. 第五项
4. 第四项
```
1. 第一项
2. 第二项
3. 第三项
5. 第五项
4. 第四项

## 无序列表
符号之后的空格不能少，-+*效果一样，但不能混合使用，因混合是嵌套列表，内容可超长
```
- 无序列表
- 无序列表
- 无序列表
- 无序列表
```
- 无序列表
- 无序列表
- 无序列表
- 无序列表
## 嵌套列表
-+*可循环使用，但符号之后的空格不能少，符号之前的空格也不能少
### 无序嵌套
```
- 第一层
    * 第二层
        + 第三层
```
- 第一层
    * 第二层
        + 第三层

### 有序无序混套
```
1. 有序
    - 无序列表
        + 无序列表
2. 有序
4. 有序
```
1. 有序
    - 无序列表
        + 无序列表
2. 有序
4. 有序

## 图片
括号内的url可以是网络路径，也可以是本地路径。本地路径可以是绝对路径，也可以是相对路径，最好取相对路径。
```
![图片描述（可省略）](url)
```

## 分割线
三个或更多-_*，必须单独一行，可含空格
```
---
___
***
```
---
___
***

##代码
### 内嵌代码
将代码放入``内（主要不是单引号，是波浪线对应的键）
```
`代码`
```
`代码`
### 代码块
代码放入\``` ``` 内,在第一行后指定编程语言，也可以不指定
``` 
    ```
    代码块
    ```
```
```
代码块
```
### 高亮代码块中的关键字或方法
使用“\```+语言名称” + \“```”进行标记,
目前支持的语言有：
1c, abnf, accesslog, actionscript, ada, apache, applescript, arduino, armasm, asciidoc, aspectj, autohotkey, autoit, avrasm, awk, axapta, bash, basic, bnf, brainfuck, cal, capnproto, ceylon, clean, clojure, clojure-repl, cmake, coffeescript, coq, cos, cpp, crmsh, crystal, cs, csp, css, d, dart, delphi, diff, django, dns, dockerfile, dos, dsconfig, dts, dust, ebnf, elixir, elm, erb, erlang, erlang-repl, excel, fix, flix, fortran, fsharp, gams, gauss, gcode, gherkin, glsl, go, golo, gradle, groovy, haml, handlebars, haskell, haxe, hsp, htmlbars, http, hy, inform7, ini, irpf90, java, javascript, json, julia, kotlin, lasso, ldif, leaf, less, lisp, livecodeserver, livescript, llvm, lsl, lua, makefile, markdown, mathematica, matlab, maxima, mel, mercury, mipsasm, mizar, mojolicious, monkey, moonscript, n1ql, nginx, nimrod, nix, nsis, objectivec, ocaml, openscad, oxygene, parser3, perl, pf, php, pony, powershell, processing, profile, prolog, protobuf, puppet, purebasic, python, q, qml, r, rib, roboconf, rsl, ruby, ruleslanguage, rust, scala, scheme, scilab, scss, smali, smalltalk, sml, sqf, sql, stan, stata, step21, stylus, subunit, swift, taggerscript, tap, tcl, tex, thrift, tp, twig, typescript, vala, vbnet, vbscript, vbscript-html, verilog, vhdl, vim, x86asm, xl, xml, xquery, yaml, zephir
```
    ```Java
    public static void showDialog(Context context, View view) {
        AlertDialog alertDialogAddHomeLink = new AlertDialog.Builder(context)
                .setView(view).create();
        Window window = alertDialogAddHomeLink.getWindow();
        WindowManager.LayoutParams p = window.getAttributes();
        p.privateFlags = WindowManager.LayoutParams.PRIVATE_FLAG_SHOW_FOR_ALL_USERS;
        window.clearFlags(WindowManager.LayoutParams.FLAG_ALT_FOCUSABLE_IM);
        window.setAttributes(p);
        alertDialogAddHomeLink.show();
    ```
```
```Java
    public static void showDialog(Context context, View view) {
        AlertDialog alertDialogAddHomeLink = new AlertDialog.Builder(context)
                .setView(view).create();
        Window window = alertDialogAddHomeLink.getWindow();
        WindowManager.LayoutParams p = window.getAttributes();
        p.privateFlags = WindowManager.LayoutParams.PRIVATE_FLAG_SHOW_FOR_ALL_USERS;
        window.clearFlags(WindowManager.LayoutParams.FLAG_ALT_FOCUSABLE_IM);
        window.setAttributes(p);
        alertDialogAddHomeLink.show();
```


## 引用
### 简单引用
```
>要引用的内容
```
>要引用的内容

### 引用嵌套
```
>第一层内容
第一层内容
>>第二层内容
第二层内容
```
>第一层内容
第一层内容
>>第二层内容
第二层内容


## 注释
```
<!--注释--->
```
## 转义字符
转义字符为\，转义的有：
```
\\ 反斜杠

\` 反引号

\* 星号

\_ 下划线

\{\} 大括号

\[\] 中括号

\(\) 小括号

\# 井号

\+ 加号

\- 减号

\. 英文句号

\! 感叹号
```
\\ 反斜杠

\` 反引号

\* 星号

\_ 下划线

\{\} 大括号

\[\] 中括号

\(\) 小括号

\# 井号

\+ 加号

\- 减号

\. 英文句号

\! 感叹号

## 表格
行首和行尾的竖线可以省略
### 形式一：默认形式
文字默认居左
```
|表头|表头|表头|
|---|---|---|
|内容内容|内容|内容|
|内容|内容|内容|
|内容|内容|内容|
```
|表头|表头|表头|
|---|---|---|
|内容内容|内容|内容|
|内容|内容|内容|
|内容|内容|内容|
### 形式二：内容居右
```
|表头|表头|表头|
|---:|---|---|
|内容内容|内容|内容|
|内容|内容|内容|
|内容|内容|内容|
```

|表头|表头|表头|
|---:|---|---|
|内容内容|内容|内容|
|内容|内容|内容|
|内容|内容|内容|

### 形式三：内容居中
```
|表头|表头|表头|
|:---:|---|---|
|内容内容|内容|内容|
|内容|内容|内容|
|内容|内容|内容|
```
|表头|表头|表头|
|:---:|---|---|
|内容内容|内容|内容|
|内容|内容|内容|
|内容|内容|内容|

## 字体、字号、颜色
```
<font face="黑体">我是黑体字</font>
<font face="微软雅黑">我是微软雅黑</font>
<font face="STCAIYUN">我是华文彩云</font>
<font color=#0099ff size=12 face="黑体">黑体</font>
<font color=#00ffff size=3>null</font>
<font color=gray size=5>gray</font>
```
<font face="黑体">我是黑体字</font>
<font face="微软雅黑">我是微软雅黑</font>
<font face="STCAIYUN">我是华文彩云</font>
<font color=#0099ff size=12 face="黑体">黑体</font>
<font color=#00ffff size=3>null</font>
<font color=gray size=5>gray</font>

-----
# 进阶篇
-----

## 生成目录
使用[toc]生成目录，但是有些编辑器不支持，比如简书

注：想在那个位置生成目录，就写在哪个位置，一般在文正的开头。
## 脚注
使用 [^keyword] 表示注脚。

这里是脚注[^n]
[^n]: 这里是脚注的内容

注：关于注脚好像每个编辑器表示方式会有所不同

## 待办列表
使用带有 [ ] 或 [x] （未完成或已完成）项的列表语法撰写一个待办事宜列表例如：
```
- [ ] 起床
- [ ] 吃早点
- [x] 已完成任务
```
- [ ] 起床
- [ ] 吃早点
- [x] 已完成任务

## 流程图
### 例1
```
    ```flow
    st=>start: Start
    e=>end: End
    op=>operation: My Operation
    cond=>condition: Yes or No?

    st->op->cond
    cond(yes)->e
    cond(no)->op
    ```
```
```flow
st=>start: Start
e=>end: End
op=>operation: My Operation
cond=>condition: Yes or No?

st->op->cond
cond(yes)->e
cond(no)->op
```
### 例2
```
    ```flow 
    st=>start: 开始 
    e=>end: 登录 
    io1=>inputoutput: 输入用户名密码 
    sub1=>subroutine: 数据库查询子类 
    cond=>condition: 是否有此用户 
    cond2=>condition: 密码是否正确 
    op=>operation: 读入用户信息

    st->io1->sub1->cond 
    cond(yes,right)->cond2 
    cond(no)->io1(right) 
    cond2(yes,right)->op->e 
    cond2(no)->io1 
    ```
```

```flow 
st=>start: 开始 
e=>end: 登录 
io1=>inputoutput: 输入用户名密码 
sub1=>subroutine: 数据库查询子类 
cond=>condition: 是否有此用户 
cond2=>condition: 密码是否正确 
op=>operation: 读入用户信息

st->io1->sub1->cond 
cond(yes,right)->cond2 
cond(no)->io1(right) 
cond2(yes,right)->op->e 
cond2(no)->io1 
```
- 流程图代码分两块，上面一块是创建你的流程（创建元素），然后隔一行，创建流程的走向(连接元素)

- 创建流程（元素）：tag=>type: content:>url
    - tag 是流程图中的标签，在第二段连接元素时会用到。名称可以任意，一般为流程的英文缩写和数字的组合。
    - type 用来确定标签的类型，=>后面表示类型。由于标签的名称可以任意指定，所以要依赖type来确定标签的类型
    - 标签有6种类型：start end operation subroutine condition inputoutput
    - content 是流程图文本框中的描述内容，: 后面表示内容，中英文均可。特别注意，冒号与文本之间一定要有个空格
    - url是一个连接，与框框中的文本相绑定，:>后面就是对应的 url 链接，点击文本时可以通过链接跳转到 url 指定页面
- 指向流程(连接元素)：标识（类别）->下一个标识
    - 使用 -> 来连接两个元素
    - 对于condition类型，有yes和no两个分支，如示例中的cond(yes)和cond(no)
    - 每个元素可以制定分支走向，默认向下，也可以用right指向右边，如示例中cond2(yes,right)。
Created with Raphaël 2.1.4开始输入用户名密码数据库查询子类是否有此用户密码是否正确读入用户信息登录yesnoyesno

流程图元素

- 开始 
st=>start: 开始
- 操作 
op1=>operation: 操作、执行说明
- 条件 
cond=>condition: 确认？
- 子程序 
sub1=>subroutine: 子程序操作说明
- 用户输入或输出 
io1=>inputoutput: 输入密码
- 结束 
e=>end: 结束
## 时序图
时序图（Sequence Diagram）用于描述对象之间发送消息的时间顺序或显示多个对象之间的动态协作。时序图中的每条消息对应一个类操作或一个事件。如下所示：
```
    ``` sequence
    客户端->打印机: 打印请求(id)
    打印机->数据库:请求数据(id)
    Note right of 数据库: 执行SQL获取数据
    数据库-->打印机:返回数据信息
    Note right of 打印机:使用数据打印
    打印机-->>客户端:返回打印结果
    客户端->客户端:等待提取结果
    ```
```
``` sequence
客户端->打印机: 打印请求(id)
打印机->数据库:请求数据(id)
Note right of 数据库: 执行SQL获取数据
数据库-->打印机:返回数据信息
Note right of 打印机:使用数据打印
打印机-->>客户端:返回打印结果
客户端->客户端:等待提取结果
```
注：Note right/left of 角色 用于定义消息显示的位置
###时序图元素
时序图主要有一下几个元素：角色，对象，生命线，激活器和消息
1. **角色（Actor）**
任何主体都可以是角色，角色对外发布消息。示例中，客户端，打印机，数据库都是角色。

2. **对象(Object)**
对象代表时序图中的对象在交互中所扮演的角色，位于时序图顶部和对象代表类角色。有的时候可能有多个打印机 ，那么这些打印机都是同一角色的不同对象

3. **生命线(Lifeline)**
生命线代表时序图中的对象在一段时期内的存在。时序图中每个对象和底部中心都有一条垂直的线，这就是对象的生命线，对象间 的消息存在于两条虚线间。

4. **激活期(Activation)**
激活期代表时序图中的对象执行一项操作的时期，在时序图中每条生命线上的窄的矩形代表活动期。它可以被理解成C语言语义中一对花括号“{}”中的内容。csdn的Markdown中并没有这一举行，只能以右侧或左侧的注解来表示“` python

5. **消息(Message)**
消息是定义交互和协作中交换信息的类，用于对实体间的通信内容建模，信息用于在实体间传递信息。允许实体请求其他的服务，类角色通过发送和接受信息进行通信。

## 公式
### 行内公式
$ 表示行内公式
```
$E=mc^2$
```
行内公式$E=mc^2$
### 整行公式
\$\$表示整行公式
```
$$\sum_{i=1}^na_i=0$$
```
$$\sum_{i=1}^na_i=0$$
