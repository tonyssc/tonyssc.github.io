---
layout: post
title: "移动端开发规范-meta篇"
date: 2015-4-27 10:30:00
---

##概要

标签提供关于HTML文档的元数据。元数据不会显示在页面上，但是对于机器是可读的。它可用于浏览器（如何显示内容或重新加载页面），搜索引擎（关键词），或其他 web 服务。 —— [W3School](http://www.w3school.com.cn/)

##移动端常用meta设置

###viewport

viewport：能优化移动浏览器的显示。如果不是响应式网站，不要使用initial-scale或者禁用缩放。大部分4.7-5寸设备的viewport宽设为360px；5.5寸设备设为400px；iphone6设为375px；ipone6 plus设为414px。

    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0"/>

- width: viewport 的宽度（ 范围从 200 到 10,000，默认为 980 像素，width=device-width 宽度为设备的宽度 ）
- height: viewport 的高度（ 范围从 223 到 10,000 ）
- initial-scale: 初始的缩放比例（ 范围从>0到 10 ）
- minimum-scale: 允许用户缩放到的最小比例
- maximum-scale: 允许用户缩放到的最大比例
- user-scalable: 用户是否可以手动缩放

<!--break-->

###apple-mobile-web-app-capable

    <meta name="apple-mobile-web-app-capable" content="yes"/>

这个meta标签是ios设备中的safari私有meta标签，它表示：允许全屏模式浏览，开启对web app程序的支持。当它设置为“yes”时，就去掉了Safari的一些默认控件，比如地址栏、状态栏之类的。

###apple-touch-fullscreen

    <meta name="apple-touch-fullscreen" content="yes"/>

这个标签的意思是添加到主屏幕以后全屏打开，将这个设置为”yes”，并且加上上面的标签。用户将该页保存到桌面打开后，看起来完全就像一个本地app。

###format-detection

    <meta name="format-detection" content="telephone=no"/>
    <meta name="format-detection" content="email=no"/>

告诉设备忽略将页面中的数字识别为电话号码(telephone=no)或者忽略识别邮箱(email=no)

###apple-mobile-web-app-status-bar-style

    <meta name="apple-mobile-web-app-status-bar-style" content="black" />

手机顶部的状态栏设置：默认值为default（白色），可以定为black（黑色）和black-translucent（灰色半透明）。
注意： 若值为“black-translucent”将会占据页面位置，浮在页面上方（会覆盖页面20px高度–iphone4和itouch4的Retina屏幕为40px）。

###apple-touch-icon/apple-touch-icon-precomposed

    <!--网站添加至ios桌面时的图标-->
    <link rel="apple-touch-icon-precomposed" sizes="57x57" href="table_ico57.png">
    <link rel="apple-touch-icon-precomposed" sizes="72x72" href="table_ico72.png">
    <link rel="apple-touch-icon-precomposed" sizes="114x114" href="table_ico114.png">
    <link rel="apple-touch-icon-precomposed" sizes="144x144" href="table_ico144.png">

添加图标到屏幕里的有两种属性值apple-touch-icon和apple-touch-icon-precomposed，区别就在于是否会应用iOS中自动给图标添加的那层高光。apple-touch-icon会使用iOS自带的高光效果，apple-touch-icon-precomposed会使用设计原图图标

<img class="size-full wp-image-3113" title="icon1" src="http://www.iptu.net/wp-content/uploads/2011/07/icon1.png" alt="" style="width: 106px; height: 131px;">
<img class="size-full wp-image-3112" title="icon2" src="http://www.iptu.net/wp-content/uploads/2011/07/icon2.png" alt="" style="width: 106px; height: 131px;">

由于iPhone以及iPad都有两种分辨率的设备存在，图标的尺寸就需要做4个：144×144(iPad Retina)、72×72(iPad)、114×114(iPhone Retina)、57×57(iPhone)。
可以使用sizes属性来告诉设备该调用哪个图标。

###apple-touch-startup-image

    <!--网站通过ios桌面启动界面-->
    <link rel="apple-touch-startup-image" sizes="2048x1496" href="startup-2048x1496.png" media="screen and (min-device-width: 1025px) and (max-device-width: 2048px) and (orientation:landscape) and (-webkit-min-device-pixel-ratio: 2)">
    <link rel="apple-touch-startup-image" sizes="1536x2008" href="startup-1536x2008.png" media="screen and (min-device-width: 1025px) and (max-device-width: 2048px) and (orientation:portrait) and (-webkit-min-device-pixel-ratio: 2)">
    <link rel="apple-touch-startup-image" sizes="1024x748" href="startup-1024x748.png" media="screen and (min-device-width: 481px) and (max-device-width: 1024px) and (orientation:landscape)">
    <link rel="apple-touch-startup-image" sizes="768x1004" href="startup-768x1004.png" media="screen and (min-device-width: 481px) and (max-device-width: 1024px) and (orientation:portrait)">
    <link rel="apple-touch-startup-image" sizes="640x920" href="startup-640x920.png" media="screen and (max-device-width: 480px) and (-webkit-min-device-pixel-ratio: 2)">
    <link rel="apple-touch-startup-image" sizes="320x460" href="startup-320x460.png" media="screen and (max-device-width: 320)">
    <link rel="apple-touch-startup-image" sizes="640x548" href="startup-320x548.png" media="(device-width: 320px) and (device-height: 568px) and (-webkit-device-pixel-ratio: 2)">

该标签是用来设置启动画面的，但它不像apple-touch-icon可以指定sizes来告诉设备该使用哪个图片（也有一种说法是在iOS5中已经支持sizes识别了，但没有测试成功），所以只能通过media里的设备分辨率的判断值来识别，而iPhone Retina的分辨率值界于取值之间，所以需要通过webkit的私有属性-webkit-min-device-pixel-ratio:2来鉴别像素密度以进行识别。
启动画面的图片尺寸并非完全等于设备的尺寸，比如iPad2的尺寸是1024×768，但它的启动画面尺寸横向是1024×748，竖向尺寸是768×1004，因为需要减去系统状栏的高度20px，而使用的Retina屏幕的iPhone4以及iPad3则需要减去状态栏的高度40px。

###apple-mobile-web-app-title

    <meta name="apple-mobile-web-app-title" content="title">

发送到屏幕时默认的命名, 添加到主屏后的标题

<img src="http://sfault-image.b0.upaiyun.com/101/040/1010401142-548142ff1330a_articlex" style="width:150px; height:267px">
<img src="http://sfault-image.b0.upaiyun.com/322/724/3227240982-5481430dcf7db_articlex" style="width:150px; height:267px">

###其他
    <!-- 针对手持设备优化，主要是针对一些老的不识别viewport的浏览器，比如黑莓 -->
    <meta name="HandheldFriendly" content="true">
    <!-- 微软的老式浏览器 -->
    <meta name="MobileOptimized" content="320">
    <!-- uc强制竖屏 -->
    <meta name="screen-orientation" content="portrait">
    <!-- QQ强制竖屏 -->
    <meta name="x5-orientation" content="portrait">
    <!-- UC强制全屏 -->
    <meta name="full-screen" content="yes">
    <!-- QQ强制全屏 -->
    <meta name="x5-fullscreen" content="true">
    <!-- UC应用模式 -->
    <meta name="browsermode" content="application">
    <!-- QQ应用模式 -->
    <meta name="x5-page-mode" content="app">
    <!-- windows phone 点击无高光 -->
    <meta name="msapplication-tap-highlight" content="no">

##结语

了解这些移动端相关的meta设置能够有助于我们对页面进行开发，以及解释一些页面上常见的问题，以上内容可以作为移动端开发meta设置的模板，然后根据具体的项目进一步筛选。

##参考链接

- [常用meta整理](http://segmentfault.com/a/1190000002407912 "常用meta整理")
- [METATAGES in HTML5](http://www.html-5.com/metatags/ "METATAGES in HTML5")
- [W3C META TAGS](http://www.w3.org/TR/html5/document-metadata.html#the-meta-element "W3C META TAGS")
- [COMPLETE LIST OF HTML META TAGS](http://code.lancepollard.com/complete-list-of-html-meta-tags/ "COMPLETE LIST OF HTML META TAGS")