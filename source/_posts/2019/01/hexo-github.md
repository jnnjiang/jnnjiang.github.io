---
title: hexo+github搭建自己的博客
permalink: hexo+github
toc: true
date: 2019-01-14 16:14:17
tags:
categories:
---

## hexo 简介
Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。
## 环境搭建
### 安装nodejs
#### Linux
1.[下载nodejs](https://nodejs.org/en/)，最新版本10.15.0
简单说就是解压后，在bin文件夹中已经存在node以及npm，如果你进入到对应文件的中执行命令行一点问题都没有，不过不是全局的，所以将这个设置为全局就好了。
2.解压到当前目录（Download）
3.移动到指定目录
```
mv Download/node-v10.15.0/ Tools/nodejs/
```
4.查看版本
```
$ cd Tool/nodejs/bin/
$ ls
$ ./node -v
v10.15.0 // 我的版本
```
5.建立软链接，使其全局有效
```
$ ln -s /home/nana/Tools/nodejs/bin/node /usr/local/bin/node
$ ln -s /home/nana/Tools/nodejs/bin/npm /usr/local/bin/npm
```
6.查看版本
```
$ node -v
v10.15.0
```
#### Mac
1.1.[下载nodejs](https://nodejs.org/en/)，最新版本10.15.0
2.双击安装（默认会安装到/usr/local/bin/下）
3.查看版本
```
$ node -v
v10.15.
```
### 安装git
#### Linux
```
sudp apt-get install git
```
#### Mac
虽然Mac自带git，但是为了方便后续用gitk查看代码提交情况，建议，用brew重新安装带gitk的git
1.如果没有安装brew，则需要先安装brew
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
2.查看系统git的位置
```
$ which git
/usr/bin/git
```
3.重新安装git
```
$ brew update
$ brew install git
```
4.再次查看git的位置
```
$ which git
/usr/local/bin/git
```
### 安装hexo
```
npm install -g hexo-cli
```

## 建站

安装完成后，执行下列命令，hexo将会在指定文件夹中新建所需要的文件
```
$ hexo init <folder>
$ cd <folder>
$ npm install
```
新建完成后，指定文件夹的目录如下：
```
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
```
这里尤其要中注意_config.yml文件，在这个文件里，可以配置网站的大部分参数。
配置详见{% post_link hexo+config hexo配置 %}