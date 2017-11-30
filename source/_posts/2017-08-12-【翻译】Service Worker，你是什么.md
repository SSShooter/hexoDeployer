---
title: 【翻译】Service Worker，你是什么？
date: 2017-08-12 21:00:09
tags:
categories: 翻译
---
> **原文** [Service Worker, what are you ?](https://kosamari.com/notes/Service-Worker-what-are-you)

*我：“Service Worker，你是什么？”*
*Service Worker：“我是一个可编程网络代理。”*
*我：“吓？”*
<!-- more -->
## Service Worker听起来很酷炫，但是我并不了解他
2015年七月，我在德州奥斯丁出席了一个JavaScript大会。台上的是Jake Archibald，我当时只知道他是一个讲了一些bathroom matter的有趣英国人。但是后来我才知道，他可是定制Service Worker规范的大人物。[演讲地址](https://www.youtube.com/watch?v=RQQNNP8tFro)
台上他围绕着他对用户体验的感悟，介绍了一个叫做Service Worker的新东西，它可以让你的网站用起来和原生手机医用一样（这是我的理解）。
这听起来很赞，我很希望可以把这个技术用在我的项目上，虽然刚接触它理解起来不容易...这不是一个库，不是一个新的HTML元素，又不是Javascript语法。阅读关于介绍Service Worker的文章总是被一些名词迷惑——例如“代理”和“缓存”。通过边理解边画图的方法，我终于对此有所理解，**Service Worker是一个外星人，你可以邀请他住在你的浏览器里**。听起来很奇怪？请听我解释。
## 在网络浏览器宇宙里，Service Worker是一个外星人

{% asset_img 1.png %}

试想一下你的浏览器是计算机星系里的一个星球（像是地球）。这个星球里，人们用HTML, CSS, 和JavaScript等语言构成“网页社会”。如果你是网站开发者，从不同类型的元素到垃圾回收机制你都懂了，那你可能是这个星球的社会学家了。

{% asset_img 2.png %}

这个星球发明了一种链接外部世界的方法，那就是**超文本传输协议**。这是从其他星系（服务器）请求资源的方法。有了这个方法我们的星球（浏览器）才能收集各种猫gif和发推。也是这个方法让这个星球变得有趣，并保持数百万住户。

{% asset_img 3.png %}

把超文本传输协议（HTTP）说得很神奇，但实际上你要用HTTP连接其他星系需要为此铺设名为因特网的管道。尺寸和长度要看你给了网络供应商多少钱，以及你所在地区的基础设施。如果这条管道又窄又长，那获取资源的速度就相对慢些了。

{% asset_img 4.png %}

问题来了，供应商不一定能保持我们星球的网络畅通，当浏览器不能连接这个管道，我们的星球就要回到过去了，回到那个恐龙横行的时代。
## 别慌！Service Worker 帮到你！
Service Worker存在于管道和星球之间。你发送的请求交给了Service Worker，请求他帮忙，而不是直接传到其他星系。这（对我来说）感觉就像是UFO里面的外星人。

{% asset_img 5.png %}

### 关于我们的新朋友Service Worker，你应该了解以下3件事
1. Service Worker 是你召唤的。除非你请求他，否则他不会出现。一旦你请求Service Worker的帮助，直到他觉得任务已经完成之前，他会一直存在。所以Service Worker没有.terminate()。
2. Service Worker 是存在于网页之外的。当你关闭一个浏览器窗口，通常一切进入不活动的状态。你不能下载视频或者浏览网页，但是！即使浏览器关闭了，Service Worker也可以在被需要时唤醒，然后在不被需要时消失，简直是奇迹！你（作为一个开发者）不用掌控Service Woker的生命周期。（这是我觉得他像外星人的原因）
3. 之前提及到的，Service Worker 存在于页面之外，这意味着他不能接触到网页元素。你不能在Service Worker 访问window变量和document变量，也不能修改里面的DOM元素。
## 所以Service Worker 可以帮我们做什么？
**1. 与缓存互动**
你可以请求Service Worker作为中间人检查事件收发，请求Service Worker在缓存里保存完整的资源。当缓存的项目被请求，Service Worker可以在缓存中请求这些数据而不用通过HTTP。这些资源被缓存了，浏览器就可以在网络不通的情况下展示内容。

{% asset_img 6.png %}

**2. 推送提醒**
得益于“Service Worker可以在浏览器窗口关闭时保持活动状态”这一奇迹，你可以实现类似推送提醒的功能。

{% asset_img 7.png %}

**3. 运行后台同步**
可以在浏览器窗口关闭时保持活动状态也意味着Service Worker可以在后台运作（如用户切换到其他标签时）。假如当浏览器离线时，你要发送一些文件，Service Worker 可以帮你在网络接通时上传。

{% asset_img 8.png %}

如果你对Service Worker 是什么感到迷惑的话，希望这篇文章可以帮到你，想要开始写代码了？我推荐你看看Jake Archibald的[offline-cookbook](https://jakearchibald.com/2014/offline-cookbook/)。

----
**某译者的胡说八道**
到底bathroom matter是什么鬼啦（（