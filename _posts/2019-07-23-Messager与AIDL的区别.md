---
layout: post
title: Messager与AIDL的区别
date: 2019-07-23
author: Mrlove
categories: Android
catalog: true
tags: Java Messager AIDL
---
# Messager与AIDL的区别

1.Messenger 的本质也是 AIDL，只不过 Messenger 对其进行了封装，在操作的时候不用再写.aidl 文件。
因为在使用 Messenger 的时候不用写 aidl 文件，所以使用 Messenger 是非常简单方便的，但是因为 Messenger 是对 AIDL 的封装，所以在底层进程通信上，两者的效率应该是差不多的。 2.在 service 端，Messenger 处理 client 的请求是单线程的,AIDL 是多线程的。

AIDL 当 service 端收到一个请求时，就会启动一个线程，不是主线程，对其进行处理，而 Messenger 是将其放入 handle 的 MessageQueue 中进行处理，handle 需要绑定一个 thread。 3.在 client 端，使用 AIDL 获取返回值是同步的，使用Messager 是异步的。

Messenger 提供了一种方法进行进程间通信，就是 send（Message msg）方法，没有返回值，如果需要返回值，需要将 client 的 Messenger 作为 msg.replyTo 参数传递过去，service 处理完后，在调用的 cilent 的 send 方法将返回值返回 client，这个过程是异步的。AIDL 可以指定方法，指定返回值，这个过程是同步的。
