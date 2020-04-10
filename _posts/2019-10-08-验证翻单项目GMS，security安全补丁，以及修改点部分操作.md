---
layout:     post
title:      验证翻单项目GMS，security安全补丁，以及修改点部分操作
subtitle:   
date:       2019-10-08
author:     Mrlove
categories: TINNO
header-img: img/post-bg-2015.jpg
catalog: 	 true
tags:
    - TINNO
---

首先还原翻单定制化脚本覆盖掉的内容

android@Precision-T1700-c0508:~/work/K210/vendor/tinno/k210/qmb_pk$ git checkout .

android@Precision-T1700-c0508:~/work/K210/vendor/tinno/k210/qmb_pk$ git status .

连接手机查看修改点

android@Precision-T1700-c0508:~/work/K210/vendor/tinno/k210/qmb_pk$ adb shell getprop |grep 2020

查看手机gms更新时间是否为最新时间

android@Precision-T1700-c0508:~/work/K210/vendor/tinno/k210/qmb_pk$ adb shell getprop |grep gms

查看项目中的gms时间

android@Precision-T1700-c0508:~/work/K210/vendor/tinno/k210/trunk$ ls

bootanimation  build_fingerprint.mk  buildinfo.sh  configs_env.sh  configs.mk  configs_version.mk  etc  gms.mk  kernel_config  logo  overlay  PlatformConfigs  sounds  vendor_buildinfo.sh

android@Precision-T1700-c0508:~/work/K210/vendor/tinno/k210/trunk$ cat gms.mk |grep version

ro.com.google.gmsversion=9_201902.go

查看git提交有没有最新修改

android@Precision-T1700-c0508:~/work/K210/vendor/tinno/k210/trunk$ gitk gms.mk &

[1] 6007

查看项目代码中security安全补丁时间

android@Precision-T1700-c0508:~/work/K210/vendor/tinno/k210/trunk$ cat gms.mk |grep security

[1]+  已完成               gitk gms.mk

查看手机中security安全补丁时间

android@Precision-T1700-c0508:~/work/K210/vendor/tinno/k210/trunk$ adb shell getprop |grep security
