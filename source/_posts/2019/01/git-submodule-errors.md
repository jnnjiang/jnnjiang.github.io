---
title: git子项目错误汇总
permalink: git-submodule-errors
toc: false
date: 2019-01-17 09:12:56
tags: git子项目
categories: git
---
## 错误收集
### clone代码报错-fatal: reference is not a tree: 85e5c187f03d9c10889dfbddd8adf4d87af2c71f
```
$ git clone --recursive -b src https://github.com/jnnjiang/jnnjiang.github.io.git blog
Cloning into 'blog6'...
remote: Enumerating objects: 803, done.
remote: Counting objects: 100% (803/803), done.
remote: Compressing objects: 100% (351/351), done.
remote: Total 803 (delta 289), reused 763 (delta 251), pack-reused 0
Receiving objects: 100% (803/803), 4.58 MiB | 661.00 KiB/s, done.
Resolving deltas: 100% (289/289), done.
Checking connectivity... done.
Submodule 'themes/next' (https://github.com/jnnjiang/hexo-theme-next.git) registered for path 'themes/next'
Cloning into 'themes/next'...
remote: Enumerating objects: 1, done.
remote: Counting objects: 100% (1/1), done.
remote: Total 5364 (delta 0), reused 0 (delta 0), pack-reused 5363
Receiving objects: 100% (5364/5364), 5.09 MiB | 812.00 KiB/s, done.
Resolving deltas: 100% (3293/3293), done.
Checking connectivity... done.
fatal: reference is not a tree: 85e5c187f03d9c10889dfbddd8adf4d87af2c71f
Unable to checkout '85e5c187f03d9c10889dfbddd8adf4d87af2c71f' in submodule path 'themes/next'
```
<!--more-->
原因还不是很清楚，解决办法：
去之前提交项目的根目录下，执行`git status`
```
$ cd blog
$ git status
On branch src
Your branch is up-to-date with 'origin/src'.
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
  (commit or discard the untracked or modified content in submodules)

	modified:   themes/next (new commits, untracked content)

no changes added to commit (use "git add" and/or "git commit -a")
```
发现有untracked文件，执行`git diff`
```
$ git diff themes/next/
diff --git a/themes/next b/themes/next
index 85e5c18..f8281ed 160000
--- a/themes/next
+++ b/themes/next
@@ -1 +1 @@
-Subproject commit 85e5c187f03d9c10889dfbddd8adf4d87af2c71f
+Subproject commit f8281ed747fe94399fd8dbf4d66d6ac5b7faf8ff-dirty
```
发现确实有一个`85e5c187f03d9c10889dfbddd8adf4d87af2c71f`提交。而`f8281ed747fe94399fd8dbf4d66d6ac5b7faf8ff`对应的是现在github上项目的`HEAD`。
执行下面的命令，将这个改动提交上去
```
$ git add themes/next/
$ git commit -m "add submodule changes"
$ git push origin src:src
```
此时再重新clone项目就不会报错了
```
$ git clone --recursive -b src https://github.com/jnnjiang/jnnjiang.github.io.git blog7
Cloning into 'blog7'...
remote: Enumerating objects: 806, done.
remote: Counting objects: 100% (806/806), done.
remote: Compressing objects: 100% (354/354), done.
remote: Total 806 (delta 290), reused 765 (delta 251), pack-reused 0
Receiving objects: 100% (806/806), 4.58 MiB | 938.00 KiB/s, done.
Resolving deltas: 100% (290/290), done.
Checking connectivity... done.
Submodule 'themes/next' (https://github.com/jnnjiang/hexo-theme-next.git) registered for path 'themes/next'
Cloning into 'themes/next'...
remote: Enumerating objects: 1, done.
remote: Counting objects: 100% (1/1), done.
remote: Total 5364 (delta 0), reused 0 (delta 0), pack-reused 5363
Receiving objects: 100% (5364/5364), 5.09 MiB | 1.01 MiB/s, done.
Resolving deltas: 100% (3293/3293), done.
Checking connectivity... done.
Submodule path 'themes/next': checked out 'f8281ed747fe94399fd8dbf4d66d6ac5b7faf8ff'
```

### `git status`时一直提示有未跟踪的文件:(new commits, untracked content)
```
$ git status
On branch src
Your branch is up-to-date with 'origin/src'.
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
  (commit or discard the untracked or modified content in submodules)

	modified:   themes/next (new commits, untracked content)

no changes added to commit (use "git add" and/or "git commit -a")
```
进入子项目`themes/next`发现文件夹下有一个patch
```
$ cd themes/next
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	0001-change-styles-of-pre-article-and-next-article.patch

```
删除就没问题了。

针对子项目中未跟踪的文件，可以分两种情况处理：
1. 如果项目目中的文件是不需要提交的，则删除即可。
2. 如果是需要提交的的，则先在子项目提交，再在主项目提交。

然后在主项目上执行`git status`会发现，没有那个提示了：
```
$ git status
On branch src
Your branch is ahead of 'origin/src' by 2 commits.
  (use "git push" to publish your local commits)
nothing to commit, working directory clean
```

