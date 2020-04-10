---
layout:     post
title:      手机写号时，无法写入android key
subtitle:   
date:       2019-11-12
author:     Mrlove
categories: TINNO
header-img: img/post-bg-digital-native.jpg
catalog: 	 true
tags:
    - TINNO
    - 写号
---
- 手机在编译版本以后要检查ro.keybox.id.value的属性值，没有这个属性值手机会写入Android Key失败　　
<div align="center">
	<img src="/img/2019-11-12/2019-11-12-1.1.PNG">  
</div>  
- 如果没有这个属性值就要添加这个属性值，可以在订单仓库下面的PlatformConfigs.mk文件添加
<div align="center">
	<img src="/img/2019-11-12/2019-11-12-1.2.png">  
</div>
- 当然也可以选择在configs.mk中添加


    PRODUCT_PROPERTY_OVERRIDES += ro.config.ringtone1=$(RING_TONE) 
    PRODUCT_PROPERTY_OVERRIDES += ro.config.default_message=$(MSG_TONE)
    PRODUCT_PROPERTY_OVERRIDES += ro.config.default_message0=$(MSG_TONE)  
    PRODUCT_PROPERTY_OVERRIDES += ro.config.default_message1=$(MSG_TONE) 
    PRODUCT_PROPERTY_OVERRIDES += ro.keybox.id.value=Mobicel_ULTRA
