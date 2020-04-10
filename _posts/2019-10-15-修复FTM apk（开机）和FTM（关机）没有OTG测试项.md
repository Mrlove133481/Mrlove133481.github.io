---
layout:     post
title:      修复FTM apk（开机）和FTM（关机）没有OTG测试项
subtitle:   
date:       2019-10-15
author:     Mrlove
categories: TINNO
header-img: img/post-bg-2015.jpg
catalog: 	 true
tags:
    - TINNO
    
---

（ 其他没有的手机测试项也可以参照此方法修改 ）

开机模式下：按*#*#8#*#*查看是否有OTG选项

关机模式下：按音量下键和电源键查看
①修复开机模式：打开vendor/tinno/k210/qmb_pk/etc/apeftm，将ftm-config.xml中如图所示OTG值改为1，将ftm-config.xml push到apeftm.mk中所示位置，就可以本地验证是否修改成功
![GitHub](https://raw.githubusercontent.com/DoubleWay/DoubleWay.github.io/master/img/2019-10-15/2019-10-15-1.1.png)
<div align="center">
	<img src="/img/2019-10-15/2019-10-15-1.1.png">  
</div>  
②修复关机模式：打开vendor/tinno/k210/qmb_pk/etc，将PCBA.conf中如图所示OTG值改为1,将PCBA.coonf push 到etc.mk中所示位置，就可以本地验证是否修改成功
<div align="center">
	<img src="/img/2019-10-15/2019-10-15-1.3.png">  
</div> 
