---
title: hexo+github搭建自己的博客
permalink: hexo+github
toc: true
date: 2019-01-14 16:14:17
tags:
    - Hexo建站
categories:
    - Hexo
---

## hexo 简介
Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。
<!-- more -->
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
安装git：
```
sudo apt-get install git
```
安装gitk:
```
sudo apt-get install gitk
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

## 预览
```
hexo g
hexo s
```
## 关联github
1.在github上创建项目，项目名为`{username}.github.io`

## 部署
1. 打开 Hexo 博客主配置文件 _config.yml，找到 deploy 属性，作如下配置：
```
deploy:
    type: git
    repository: https://github.com/jnnjiang/jnnjiang.github.io.git
    branch: master
```

2. 在`.deploy_git/`下配置github账号：
```
git config user.name "xxxx"
git config user.email "xxxx"
```

如果没有`.deploy_git/`文件也不用担心，执行下`hexo d`就会生成，执行的过程中会报错，不用担心，按照步骤2配置账号信息即可。
3. 执行如下命令：
```
hexo g
hexo d
```
按照提示输入github账号的用户名和密码即可。

4.如果不想每次都输入用户名和密码，可以通过配置`./git/config`实现：
```
git config credential.helper store
```
然后部署时输入一次用户名和密码即可，此时会在user下面生成`.git-credentials`文件。
以后在部署就不用输入用户名和密码了。


## 配置.deploy中git账户
使用`hexo d`将代码推送到github时，如果之前配置过git账户，但是提交是想用新的git账户，而在没有执行`hexo d`之前，`.deploy`文件夹是不会生成的，这种情况下改怎么办呢？
1.执行`hexo d`推送一次代码。需要输入用户名和密码的时候，输入新账户的
2.登录github，将项目的默认分支设置成其他分支，然后删除master分支（blog默认是推送到master分支的，否则无法正常工作）
3.进入本地`.deploy/` 文件夹，配置新的git账户新
```
git config user.name "xxx"
git config user.email "xxx"
git config credential.hepler store
```
4.将`.deploy/.git/config`文件保存到项目外
5.删除`.deploy/.git`文件夹
6.重新创建仓库
```
cd .deploy
git init
```
7.将第4步中保存的config文件复制到`.deploy/.git/`下。
8.执行`hexo d`重新推送代码，这时候会发现远端存在一个干净的分支，用户名也变成新的了
9.切换默认分支。
