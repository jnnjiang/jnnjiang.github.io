---
title: liunx-user
permalink: liunx-user
toc: false
date: 2019-01-25 17:58:14
tags:
categories:
---
linux下修改文件用户组
chgrp： change group的简写，修改文件所属的用户组。
chgrp users test.log
修改后查看 ls -l
-rwxrwx--- 1 work users 0 Jun 8 15:46 test.log
如果要修改该目录下所有文件和目录，使用-R参数。
chgrp -R users test
要被改变的group名，必须在 /etc/group 文件中。 /etc/group文件记录系统中所有的组名称。

linux下修改文件所有者
chown ：change owner的简写， 修改文件的所有者。
chown [-R] 账号名称 文件或目录
-R 递归，将子目录下文件全部修改。
将文件所有者修改bin
chown bin test.log
修改的用户必须在/etc/passwd文件中 /etc/passwd记录用户信息。
chown还可以修改组名称
chown root:root test.log
将所有者和组名称都修改为root。