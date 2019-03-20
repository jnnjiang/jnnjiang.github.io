---
title: Hexo 多个终端同步开发的问题
permalink: hexo-multi-peers
toc: false
date: 2019-01-16 17:44:52
tags:
categories:
---

## 一端
如果想在多个终端上开发博客，并且还要保持代码同步，可以按照一下步骤操作
1.在已经搭建好Hexo环境的本地项目上创建分支`src`，需要先在跟目录下执行`git init`，把本地代码变成一个git项目。默认是在`master`分支，执行
```
git checkout -b src
```
将项目切换到src分支，因为我们在执行`hexo d`的时候，默认是将public文件夹下的内容提交到git项目的master分支上。
<!-- more -->
2.将项目提交到github上
```
git add .
git commit -m "first commit"
git push origin src:src
```
3.登录github，就会在项目下看到我们刚才的提交记录。至此，项目的源码就得到保存了。

## 另一端
4.在另一端同步代码
```
git clone -b src 项目地址
```
5.安装必要的依赖
```
npm install hexo 
```
6.然后就可以编辑同步博客内容了
```
hexo g
hexo d
```
7.提交源码
```
git add .
git commit -m "first commit"
git push origin src:src
```
## 其他端
操作方式同`另一端`

## Tips
1.如果电脑上之前配置了git账户，那么执行`hexo d`时，默认会使用已经配置的git的账户。关于`.deploy`中git账户的配置，可以参见{% post_link hexo+github hexo+github搭建自己的博客 %}中`配置.deploy中git账户`一节。


项目     | 价格
-------- | ---
Computer | $1600
Phone    | $12
Pipe     | $1