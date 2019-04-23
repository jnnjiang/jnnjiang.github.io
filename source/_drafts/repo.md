---
title: repo
permalink: repo
comments: true
toc: true
date: 2019-04-23 18:32:47
updated: 2019-04-23 18:32:47
tags:
categories:
---


每次sync代码之后，都会执行`repo start branchname --all`给所有项目创建分支，但是等到在执行`repo sync`sync代码之后，就会发现项目的branch变成了如下状态
```
* (HEAD detached at 43d8941)
  base0423
```
百思不得其解，最后在网上找到了答案，原来是我用的`sync`命令的问题。
为了是项目可以快速sync，避免sync一个tags文件，SCM建议用`repo sync --no-tags -cdj4`。只知道这样就不会sync tags了，速度会快很多，但是确不知道后面的参数`-cdj4`给我的工作造成了很大的困扰，因为每次sync之后，项目branch的状态就会变成了`* (HEAD detached at 43d8941)`这种状态，即使项目的本地代码和远端代码没有任何差别。下面是对后面参数的解释
```
-c选项，–current-branch：只sync，只下载当前分支，不加上会下载很多没用的分支的。。默认情况下，sync会同步所有的远程分支，当远程分支比较多的时候，下载的代码量就大。使用该参数，可以缩减下载时间，节省本地磁盘空间。

-j选项，指定同时开启几个线程来下载代码，这个不要多，就使用4就行。使用的多不见得快。

-d选项，detach是分离，剥离的意思，一般在git中用git status查看有时候能看到。 
HEAD detached at 6beb886d10ec，这个是啥意思呢？这个指头指针剥离自一个revision， 
也就是当前分支剥离自一个revision，也就是一个没用名字的分支，也就是当前分支是一个匿名分支。 
```
就是因为用了`-d`选项才导致了这一问题，哎，没有对命令深入了解就用，真的是很坑啊，特意记录下提醒自己，以后在给命令加参数的时候，一定要先了解每一个参数的内容。

参考：[Android下的配置管理之道之repo的使用](https://blog.csdn.net/mmh19891113/article/details/78476580)