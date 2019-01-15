---
title: Mac系统安装gitk
date: 2019-01-12 11:55:46
tags: 
    - 常用工具
categories:
    - Mac
---
# gitk for mac
1.如果没有安装brew，则需要先安装brew
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
2.由于系统自带的git中没有gitk，所以需要重新安装
    1)查看系统git的位置
    ```
    $ which git
    /usr/bin/git
    ```
    2)重新安装git
    ```
    $ brew update
    $ brew install git
    ```
    3)再次查看git的位置
    ```
    $ which git
    /usr/local/bin/git
    ```
    安装成功
3.在git项目中，执行`gitk`命令，就可以看到图形化界面了。
