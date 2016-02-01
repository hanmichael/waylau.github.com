---
layout: post
title: TCP 协议的三次握手、四次分手
date: 2009-12-20 00:22
author: admin
comments: true
categories: [Web]
tags: [Web,TCP]
---
详细描述了 TCP 协议的连接和关闭的整个过程。解释了为什么 TCP 协议是面向连接的、可靠的数据传输协议。
   
 <!-- more -->

### TCP

在互联网上之间的通信交流，一般是基于 TCP  (Transmission Control Protocol，传输控制协议) 或者 UDP (User Datagram Protocol，用户数据报协议) 。两者的一个重要区别是，TCP 是面向连接提供端到端可靠的数据流(flow of data)。

“面向连接”就是在正式通信前必须要与对方建立起连接。比如你给别人打电话，必须等线路接通了、对方拿起话筒才能相互通话。

### 三次握手

TCP 是基于连接的协议，也就是说，在正式收发数据前，必须和对方建立可靠的连接。一个 TCP 连接必须要经过三次“握手”才能建立起来，简单的讲就是：


1. 为了建立连接时，客户端 A 发送 SYN 包（SYN=j）到服务器 B，并进入 SYN_SEND状态，等待服务器 B 确认。 【A 向 B 请求连接：“我想给你发数据，可以吗？”】
2. 服务器 B 收到 SYN 包，必须确认客户端 A 的 SYN（ACK=j+1），同时自己也发送一个 SYN 包（SYN=k），即 SYN+ACK 包，此时服务器B进入SYN_RECV 状态。 【B 回应 A：“好的，你来吧”】
3. 客户端 A 收到服务器 B 的 SYN＋ACK 包，向服务器 B 发送确认包 ACK（ACK=k+1），此包发送完毕，客户端 A 和服务器 B 进入 ESTABLISHED 状态，完成三次握手。 【A 回应 B：“好的，我来也，你接着吧！”】

三次“握手”的目的是使数据包的发送和接收同步，经过三次“对话”之后，主机 A 才向主机 B 正式发送数据。

![](http://b303.photo.store.qq.com/psb?/c152afc5-e83c-42b3-9779-3008bbfd9eb8/pO3vXjI0xFO4bpuAELBz5BXr*BOdhBViaDfpcPS8LSs!/b/Ye86nbRrCQAAYonNobRLCQAA&ek=1&kp=1&pt=0&su=0154437137&sce=0-12-12&rf=2-9)

### 四次分手

由于 TCP 连接是全双工的，因此每个方向都必须单独进行关闭。这个原则是当一方完成它的数据发送任务后就能发送一个 FIN 来终止这个方向的连接。收到一个 FIN 只意味着这一方向上没有数据流动，一个 TCP 连接在收到一个 FIN 后仍能发送数据。首先进行关闭的一方将执行主动关闭，而另一方执行被动关闭。 

1. 客户端 A 发送一个 FIN 给服务器 B，用来关闭客户端 A 到服务器 B 的数据传送。【A 对 B 说：“我传完了”】 
2. 服务器 B 收到这个 FIN，它发回一个 ACK，确认序号为收到的序号加1（报文段5）。和 SYN 一样，一个 FIN 将占用一个序号。 【B 回应 A：“好的”】
3. 服务器 B 关闭与客户端 A 的连接，发送一个 FIN 给客户端 A。 【B 对 A 说：“我也传完了”】
4. 客户端 A 发回 ACK 报文确认，并将确认序号设置为收到序号加1。 【A回应B：“好的，我走了”】

TCP 采用四次分手关闭连接如图2所示。

![](http://b303.photo.store.qq.com/psb?/c152afc5-e83c-42b3-9779-3008bbfd9eb8/WbGDB9ewAnjDDJ6ImIKv89OhBtNHRTmeiPYiWNgrRuc!/b/YWu2m7QXCQAAYrlrqbQFCQAA&ek=1&kp=1&pt=0&su=05415601&sce=0-12-12&rf=2-9)

### 为什么建立连接协议是三次握手，而关闭连接却是四次握手呢？ 

这是因为服务端的 LISTEN 状态下的 SOCKET 当收到 SYN 报文的建连请求后，它可以把 ACK 和 SYN（ACK起应答作用，而SYN起同步作用）放在一个报文里来发送。但关闭连接时，当收到对方的 FIN 报文通知时，它仅仅表示对方没有数据发送给你了；但未必你所有的数据都全部发送给对方了，所以你可以未必会马上会关闭SOCKET,也即你可能还需要发送一些数据给对方之后，再发送 FIN 报文给对方来表示你同意现在可以关闭连接了，所以它这里的 ACK 报文和 FIN 报文多数情况下都是分开发送的。 【收到2个“好的”才算完成。大家好才是真的好】

### 为什么 TIME_WAIT 状态还需要等 2MSL 后才能返回到 CLOSED 状态？ 

这是因为虽然双方都同意关闭连接了，而且握手的4个报文也都协调和发送完毕，按理可以直接回到 CLOSED 状态（就好比从 SYN_SEND 状态到 ESTABLISH 状态那样）；但是因为我们必须要假想网络是不可靠的，你无法保证你最后发送的ACK报文会一定被对方收到，因此对方处于 LAST_ACK 状态下的 SOCKET 可能会因为超时未收到 ACK 报文，而重发 FIN 报文，所以这个 TIME_WAIT 状态的作用就是用来重发可能丢失的 ACK 报文

### 控制信息字段

* SYN： 同步序列编号(Synchronize Sequence Numbers) 
* ACK： 确认字段
* FIN： 发送方已经传完数据
* PSH： 推送功能
* RST： 重置连接
* URG： 紧急指针

### 常用状态描述

![](http://b301.photo.store.qq.com/psb?/c152afc5-e83c-42b3-9779-3008bbfd9eb8/xwsxGfO03s2YRHor2zOAIJI78WwRV*10du5eUNWYw4s!/b/YXO9drPtIAAAYvGxdrMTIQAA&ek=1&kp=1&pt=0&su=020610481&sce=0-12-12&rf=2-9)
