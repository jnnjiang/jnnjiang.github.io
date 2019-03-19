---
title: Java-并发
permalink: Java-并发
toc: false
date: 2019-03-19 13:50:23
tags:
categories:
---
一开始就将一个类设计成线程安全的，比在后期重新修复它更容易。

在没有正确同步的情况下，如果多个线程访问了同一个变量，程序就存在隐患，有三种方法修复它

* 不要跨进程共享变量
* 使状态变量为不可变的，或
* 在任何访问状态变量的时候使用同步

无状态对象永远是线程安全的。什么是无状态对象？？？(无状态就是没有变量)

最常见的一种竞争条件是“检查再运行”
检查再运行（check-then-act)：你观察到一些事情为真（X文件不存在），然后（then）基于你的观察去做一些事情（创建X文件），但事实上，从观察到执行操作的这段时间内，观察结果可能已经无效了（有人在此期间创建了文件X），从而引发错误（非预期的异常，重写数据或破坏文件。

检查再运行的常见用法是惰性初始化（Lazy initialization）。惰性初始化的目的是延迟对象的初始化，直到程序真正使用它，同时确保它只初始化一次。
```
public class LazyInitRace{
    private ExpensiveObject instance = null;
    public ExpensiveObject getInstance(){
        if(instance == null){
            intance = new ExpensiveObject();
        }
        return instance;
    }
}
```
这段惰性初始化的代码，可能会导致instance被实例化多次，如果多个线程并发访问该段代码的话。

竞争条件并不总是失败，还需要某些特殊的十分，但是竞争条件会引起严重的问题

####原子操作
假设有操作A和B，如果从执行A的线程的角度看，当其他线程执行B时，要么B全部执行完成，要么一点都没执行，这样A和B互为原子操作。一个原子操作是指：该操作对于所有的操作，包括它自己，都满足前面描述的状态。

为了保证线程安全，操作必须原子的执行。想“检查再运行”和“读-改-写”这样的复合操作，可以借助`锁（synchronized）`来实现原子性。还有一种方法是使用现有的`java.util.concurrent`包中的线程安全类。

为了保证状态的一致性，要在单一的原子操作中更新相互关联的状态变量。

#####锁
声明为synchronized的方法，或者被synchronized包裹的代码块，同一时间只有一个线程可以进入，保证了线程安全。（但是，由于这个关键字，有时可能会引发性能问题）

当使用锁的时候，你应该清楚块中的代码的功能，以及它的执行过程是否会很耗时。无论是做运算密集型的操作，还是在执行一个可能存在潜在阻塞的操作，如果线程长时间地占有锁，就会引起活跃度与性能风险的问题。有些耗时的计算或操作，比如网络或控制台I/O，难以快速完成，执行这些操作期间不要占有锁。











```
05-10 14:32:49.540  5268  5268 E AndroidRuntime: java.lang.NoSuchMethodError: No interface method getFrontLeftAngle()F in class Lcom/ff/VehicleManager/interfaces/IDoorBinder; or its super classes (declaration of 'com.ff.VehicleManager.interfaces.IDoorBinder' appears in /system/framework/vehicleManager.jar)

=>将vehicleManager.jar push 到系统中
nana@HP:~/ffdev/OCar/Mainline/MPC/out/target/product/df91_hu_mpc/system/framework$ adb push vehicleManager.jar /system/framework/vehicleManager.jar
```

gradle error
```
error: duplicate value for resource 'attr/icon' with config ''.	
https://blog.csdn.net/qq_24014229/article/details/79360344



java.util.concurrent.ExecutionException: com.android.tools.aapt2.Aapt2Exception: AAPT2 error: check logs for details	
https://stackoverflow.com/questions/46910532/android-studio-3-0-rc-2
```


资源重复
```
[dimen/car_navigation_button_width] /home/nana/ffdev/OCar/Mainline/MPC/vendor/leeco/packages/apps/SystemUI/res/values/dimens_car.xml	[dimen/car_navigation_button_width] /home/nana/ffdev/OCar/Mainline/MPC/vendor/leeco/packages/apps/SystemUI/res/values/dimens.xml: Error: Duplicate resources


duplicate layer name: changing com.leeco.vehicle/com.leeco.vehicle.car.VehicleActivity to com.leeco.vehicle/com.leeco.vehicle.car.VehicleActivity#2

final int callingPid = Binder.getCallingPid();
final int callingUid = Binder.getCallingUid();
```


ubuntu更改计算机的名字
```
Ubuntu 更改计算机的名字：
打开/etc/hostname文件直接更改

更改之后，每次执行sudo 时会报如下警告（假设计算机的名字为abc）：
sudo: unable to resolve host abc


虽然sudo 还是可以正常执行, 但是警告讯息每次都出来,而这只是机器在反解上的问题, 所以就直接从/etc/hosts 设定, 让abc(hostname) 可以解回127.0.0.1 的IP 即可.

在127.0.0.1 localhost 后面加上主机名称(hostname) 即可, /etc/hosts 内容修改成如下: 
127.0.0.1      localhost abc  #要保证这个名字与 /etc/hostname中的主机名一致才有效
# 或改成下面这两行 
#127.0.0.1    localhost 
#127.0.0.1    abc
这样设完后, 使用sudo 就不会再有那个提示信息了。
```

刷包
```
sudo su 切换到管理员权限
./flash_all.sh  执行flash文件
```

开发流程
```

新建目录：
# repo init -u minervar:qcom/mojave/platform/manifest.git -b master -m le/ARGUS_EVT0.1_DEV_MAIN.xml --repo-url=minervar:tools/repo.git --no-repo-verify
# repo sync -d



----------------------------------原码编译------------------------------
   @ repo sync -d
   @ source build/envsetup.sh
   @ lunch (8996)
     #如果framework api 升级   make update-api
     @ make -j4
     @ make otapackage

----------------------------------提交代码------------------------------
     repo start bug_00 .
     git status


     git add

     git status

     git commit -s

LetvXXX: 说明

Ticket: APOLLO-1（jira上的tickiet号）

然后     repo upload
```

CSDN密码：
```
csdn密码：Vx&GhqFx8dpi
```

给AOSP源码建立索引报错及解决办法
```

Try increasing heap size with java option '-Xmx<size>'.
=>
出现这个错误是由于电脑内存不足，在命令行分别执行以下三条语句，然后继续编译
export JACK_SERVER_VM_ARGUMENTS="-Dfile.encoding=UTF-8 -XX:+TieredCompilation -Xmx8g" 
./prebuilts/sdk/tools/jack-admin kill-server 
./prebuilts/sdk/tools/jack-admin start-server 
```

开发环境配置
```
开发环境配置：


android o编译需要先一处autogen目录文件：
rm -rf vendor/ff/ff_autogen


编译时需要安装的依赖：
sudo apt-get install git-core git gnupg flex bison gperf build-essential zip curl libc6-dev libncurses5-dev:i386 x11proto-core-dev libx11-dev:i386 libreadline6-dev:i386 libgl1-mesa-glx:i386 libgl1-mesa-dev g++-multilib openjdk-8-jdk tofrodos python-markdown libxml2-utils xsltproc zlib1g-dev:i386 dos2unix libgtk2.0-0:i386 libxxf86vm1:i386 libsm6:i386 lib32stdc++6 p7zip-rar


sudo apt-get install libssl-dev protobuf-compiler python-protobuf

sudo apt-get install -y python-pip

sudo pip install xlrd

sudo pip install protobuf





配置gerrit，时遇到的错误：
解决：no matching key exchange method found. Their offer: diffie-hellman-group1-sha1


解决办法：
解决：修改~/.ssh/config，加入
Host *
    KexAlgorithms +diffie-hellman-group1-sha1




编译android 7.0 出现Try increasing heap size with java option '-Xmx<size>'错误解决方案

出现这个错误是由于电脑内存不足，在命令行分别执行以下三条语句，然后继续编译
export JACK_SERVER_VM_ARGUMENTS="-Dfile.encoding=UTF-8 -XX:+TieredCompilation -Xmx8g" 
./prebuilts/sdk/tools/jack-admin kill-server 
./prebuilts/sdk/tools/jack-admin start-server 
```