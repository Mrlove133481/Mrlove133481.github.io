---
layout:     post
title:      Messager与AIDL的区别
subtitle:   
date:       2019-07-23
author:     Mrlove
categories: Android
header-img: img/post-bg-alibaba.jpg
catalog: 	 true
tags:
    - java
    - Messager
    - AIDL
---
1.Messenger的本质也是AIDL，只不过Messenger对其进行了封装，在操作的时候不用再写.aidl文件。
因为在使用Messenger的时候不用写aidl文件，所以使用Messenger是非常简单方便的，但是因为Messenger是对AIDL的封装，所以在底层进程通信上，两者的效率应该是差不多的。
2.在service端，Messenger处理client的请求是单线程的，AIDL是多线程的。
AIDL当service端收到一个请求时，就会启动一个线程，不是主线程，对其进行处理，而Messenger是将其放入handle的MessageQueue中进行处理，handle需要绑定一个thread。
3.在client端，使用AIDL获取返回值是同步的，使用Messager是异步的。
Messenger提供了一种方法进行进程间通信，就是send（Message msg）方法，没有返回值，如果需要返回值，需要将client的Messenger作为msg.replyTo参数传递过去，service处理完后，在调用的cilent的send方法将返回值返回client，这个过程是异步的。AIDL可以指定方法，指定返回值，这个过程是同步的。
