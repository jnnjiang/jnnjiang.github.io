---
title: git子项目
permalink: git-submodule
toc: false
date: 2019-01-17 09:59:09
tags:
categories:
---
## 添加子项目
```
$ git submodule add https://github.com/jnnjiang/hexo-theme-next.git //后面的url是子项目地址
```

## 删除子项目

- 删除.gitsubmodule里相关部分
- 删除.git/config 文件里相关字段
- 删除子项目目录。
```
$ git rm --cached <本地路径>
```
## clone包含子项目的项目
### 方式:1：
```
$ git clone 项目地址
$ git submodule init
$ git submodule update
```
### 方式2：
```
$ git clone --recursive 项目地址
```
注：增加--recursive参数，会递归帮我们clone所有的子项目。

## 修改子项目

## 同步子项目的代码
