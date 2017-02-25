---
layout: post
title: "也谈flexbox布局"
date: 2014-09-15 10:00:00
---

为什么叫也谈flexbox布局呢？首先网上已经有不少关于这方面知识的介绍，尤其是[w3cplus](http://www.w3cplus.com/)中，分了几篇文章对该知识点进行了较详细的分析，本人一开始也是参考这些文章入门的。随着将该技术用到工作中的mac和h5的项目中，会发现还有一些需要注意的地方，说严重点就是这里边还有坑。这便是“再谈一下flexbox布局”的初衷。

<!--break-->

##什么是flexbox布局
Flexbox布局俗称伸缩布局，它可以简单快速的创建一个具有弹性功能的布局。一个Flexbox布局是由一个伸缩容器（flex containers）和在这个容器里的若干伸缩项目（flex items）组成。伸缩容器（flex containers）是一个HTML标签元素，并且“display”属性显式的设置了“flex”属性值。在伸缩容器中的所有子元素都会自动变成伸缩项目（flex items）。当在一个小屏幕上显示的时候，Flexbox可以让元素在容器（伸缩容器）中进行自由扩展和收缩，从而容易调整整个布局。

Flexbox布局能够让我们很轻松的实现以下效果：

- 在不设置元素的具体宽度的情形下将元素排成横排，并在一排的空间不够的时候折行。
- 快速的将元素排成竖排。
- 将元素沿着父容器的左边、右边或中间或者两端(之前只能使用text-align:justify，还需要为低版本浏览器做很多兼容)对齐。
- 改变元素显示的顺序而不改变页面的dom结构。
- 将每个元素占有的空间设置为父元素宽度／高度的一个比例，却不用担心在父元素的尺寸设置为百分比值的时候或是窗口的尺寸变化的时候布局会坏掉。
- 实现元素的水平，垂直居中。

flexbox这些特性完美的实现了流式布局，并在原始的百分比布局基础上做了很多实用功能的扩展，可以说它天生就是为了h5而生。

##flexbox的前世今生
要想真正用好flexbox布局，有必要了解其发展史。否则在今后项目中运用它的时候会出现让你抓狂的问题(更何况h5的项目会测试N多机型和N+N种浏览器 =。=! )。下面着重介绍flexbox的发展历史，如果想了解每个版本中的其他属性，请参考各个版本中的相关链接。

###flexbox诞生

w3c在2009年发布了第一版[Flexible Box Layout Module](http://www.w3.org/TR/2009/WD-css3-flexbox-20090723/)。根据该规范，定义了两个新的display属性为：

    display: box;
    display: inline-box;

伴随着该display属性，同时定义了一系列flexbox布局需要的属性和方法。第一版规范仅仅得到了旧版webkit(chrome, safari)内核和旧版Gecko内核(firefox)的支持。支持版本如下：

    display: -webkit-box; /* OLD - iOS 6-, Safari 3.1-6 */
    display: -moz-box;    /* OLD - Firefox 19- (doesn't work very well) */

虽然这个版本是flexbox的第一版，但是它在页面布局上带来的贡献绝对不可小视。我们都知道，市面上种类繁多的移动设备rom和各种自主研发或套壳浏览器。想要做到对它们的兼容，这个版本的兼容样式是必不可少的。关于前缀，box和inline-box这两个属性只需要设置带前缀的样式即可。关于支持性，webkit内核的浏览器对旧版的flexbox支持很好，但不得不提的就是gecko内核的firefox。我特地安装了最新版的firefox浏览器(32.0.1)并做了相关测试，发现如果不设置伸缩容器的宽度，设置display: -moz-box的伸缩容器表现出来的行为和display: -moz-inline-box一样，因此如果使用-moz-box进行布局，伸缩容器就一定要**设置宽度**。

###flexbox成长

w3c在2011-2012年发布了新的flexbox布局，也可以算作flexbox历史上的第二版[Flexible Box Layout Module - 2011](http://www.w3.org/TR/2011/WD-css3-flexbox-20110322/)，[CSS Flexible Box Layout Module - 2012](http://www.w3.org/TR/2012/WD-css3-flexbox-20120322/)。

这两个版本在第一版的基础上将box替换为flexbox:

    display: flexbox;
    display: inline-flexbox;

该版本并没有得到各浏览器厂商很好地支持，可能w3c不想给flexbox布局遗留太多的兼容性语法，在第三版发布之后这个版本的语法只有IE10保留了对它的支持。

    display: -ms-flexbox; /* TWEENER - IE 10 */

所以，如果开发的项目需要支持IE浏览器，则需要将这个兼容语法保留下来，其他的浏览器就不用考虑该语法了。

###flexbox的现在和未来

w3c在2012年6月发布了第三版flexbox布局，其语法结构一直沿用至今并规范了其名字为Level 1，[CSS Flexible Box Layout Module Level 1](http://www.w3.org/TR/css-flexbox-1/)。

这个版本中，w3c再一次对flexbox的核心语法进行了修改, display属性如下：

    display: flex;
    display: inline-flex;

由于这个版本的语法已经作为新一代flexbox布局的标准，各个浏览器的厂商都在w3c的标准下对它做了很好地支持。下面列举webkit内核和gecko内核的语法。需要注意的是，在这个版本的语法中，firefox浏览器只支持默认(不带前缀)的属性：

    display: -webkit-flex;  /* NEW - Chrome */
    display: flex;          /* NEW, Spec - Opera 12.1, Firefox 20+ */
    display: -moz-flex;     /* Error doesn't work */

在我看来，第三版的flexbox布局已经能够完美的解决大多数移动端的复杂布局。至于将来会不会有更加先进的布局技术，这个艰巨的任务只能由w3c的工作小组来完成了。

##flexbox的那些坑

了解完flexbox的历史，让我们回到项目中，看看flexbox给我们带来的那些坑！

###1.浏览器属性支持

比如我们开发一个h5的项目，考虑到要兼容多个版本的浏览器(Android 2.1, Android 2.2+, ios6, ios7...)。我们既要保证低版本浏览器能够在布局上不出现问题，还要尽量为高版本的浏览器设置一些高级属性，这同样也体现了渐进式增强的特点。因此我们要做如下设置：
    
    display: -webkit-box;   /* OLD - iOS 6-, Safari 3.1-6 */
    display: -moz-box;      /* OLD - Firefox 19- (doesn't work very well) */
    display: -ms-flexbox;   /* TWEENER - IE 10 */
    display: -webkit-flex;  /* NEW - Chrome */
    display: flex;          /* NEW, Spec - Opera 12.1, Firefox 20+ */

由于移动端firefox用户量较小，而旧版本的flexbox在firefox上支持的也不是很好。因此我们可以去掉display: -moz-box，只保留display: flex对新版firefox的支持即可。

###2.水平、垂直居中

flexbox完美的解决了项目中任何布局的水平、垂直居中问题。我们只需要给伸缩容器设置如下属性：

    /* basic flexbox style */
    display: -webkit-box;   /* OLD - iOS 6-, Safari 3.1-6 */
    display: -ms-flexbox;   /* TWEENER - IE 10 */
    display: -webkit-flex;  /* NEW - Chrome */
    display: flex;          /* NEW, Spec - Opera 12.1, Firefox 20+ */
    
    /* vertical && horizontal */
    -webkit-box-pack: center;           /* OLD - horizontal for IOS 6-, Safari 3.1-6 */
    -webkit-box-align: center;          /* OLD - vertical for IOS 6-, Safari 3.1-6 */
    -ms-flex-pack: center;              /* TWEENER - horizontal for IE 10 */
    -ms-flex-align: center;             /* TWEENER - horizontal for IE 10 */
    -webkit-justify-content: center;    /* NEW - horizontal for Chrome */
    justify-content: center;            /* NEW - horizontal for Firefox */
    -webkit-align-items: center;        /* NEW - vertical for chrome */
    align-items: center;                /* NEW - vertical for Firefox */

用了这么多代码进行新老样式兼容，似乎看上去搞定了，但这些样式在低版本的webkit内核上(IOS6...)会有一个坑。就是flexbox的居中样式需要配合margin: auto来完成真正意义上的居中。所以还需要加上如下设置：

    /* 水平居中 */
    margin-left: auto;
    margin-right: auto;
    
    /* 垂直居中 */
    margin-top: auto;
    margin-bottom: auto;
    
    /* 水平、垂直居中 */
    margin: auto;

### 3.内容和容器的关系

在进行页面布局的时候，我们经常会碰到如下场景：

<img class="article_entry_img" src="http://images.cnitblog.com/blog/575790/201311/28110734-10370ecb20144baaae2f169390df01eb.png">

对页面中的某个容器进行均分操作，使用flexbox布局实现该效果的新老样式如下：

    -webkit-box-flex: 1;    /* OLD Chrome */
    -ms-flex: 1;            /* OLD IE */
    -webkit-flex: 1;        /* NEW Chrome */
    flex: 1;                /* NEW Chrome, Safari, Firefox */

进行如上设置后出现的问题就是：旧版浏览器使用-webkit-box-flex: 1，伸缩项的宽度会和其内容的多少有关。而设置-webkit-flex: 1，伸缩项的宽度是固定的，无论其中的内容有多少。它们的差异表现为下图：

<img class="article_entry_img" src="http://images.cnblogs.com/cnblogs_com/tonyssc/612569/o_28110734-10370ecb20144baaae2f169390df01eb.jpg">

到这里，我们就有必要了解一下flex属性了，通过查看w3c官方文档得知flex是另外三个属性的缩写，他们分别是：

1. flex-grow：定义伸缩项的扩展能力。它接受一个不带单位的值做为一个比例。主要用来决定伸缩容器剩余空间按比例应扩展多少空间。默认值为1。
2. flex-shrink：定义伸缩项的收缩能力。它接受一个不带单位的值做为一个比例。默认值为0。
3. flex-basis：定义伸缩项的伸缩基准值。它接受一个类似width的值。默认为auto。

用到flex缩写中即：flex: none | [ <‘flex-grow’> <‘flex-shrink’>? || <‘flex-basis’> ]。

按照这个缩写我们将把上边的代码改为:

    -webkit-box-flex: 1;        /* OLD Chrome */
    -ms-flex: 1 0 auto;         /* OLD IE */
    -webkit-flex: 1 0 auto;     /* NEW Chrome */
    flex: 1 0 auto;             /* NEW Chrome, Safari, Firefox */

现在我们将flex属性的缩写补全，另外两个值按照其默认值来设置，按说得到的结果应该和上边一样。但是恰恰相反，现在这两版语法表现出的行为完全一致，伸缩项的宽度都会根据内容多少改变。他们真实地分配原则是：先按照伸缩项的内容进行空间分配，然后将伸缩容器剩余的空间按照flex-grow的比值进行分配。也就是说，我们这样设置得到的结果不是将伸缩容器平均分为N份，而是将减去伸缩项内容剩余的宽度平均分为N份。

再继续查看w3c对于flex的定义，我们发现：
><‘flex-basis’>

>This component, which takes the same values as the width property, sets the flex-basis longhand and specifies the flex basis: the initial main size of the flex item, before free space is distributed according to the flex factors. When omitted from the flex shorthand, its specified value is 0%.

最后这句话揭露了问题的真相，当使用flex属性的缩写格式时，flex-basis的默认值为0%，即伸缩项的伸缩基准值为0。这就是为什么当我们只设置flex: 1后，无论内容如何变化，伸缩项的宽度始终保持不变。所以：flex: 1 < = > flex: 1 0 0

最后附上一个用sass编写的flexbox布局新老版本兼容代码的@mixin链接：[sass-flex-mixin](https://github.com/mastastealth/sass-flex-mixin/blob/master/flex.scss "sass-flex-mixin")

##结语
flexbox布局固然好用，但我们也需要根据项目的实际情况来做出合理的选择，有些时候是不是用宽度百分比 + box-sizing(border-box)也能实现简单的响应式布局。这样我们就能避免在不恰当的地方浪费更多地精力和css大小。

##参考链接

- [CSS Flexible Box Layout Module Level 1](http://www.w3.org/TR/css3-flexbox/ "Flexible Box Layout Module 1")
- [伸缩布局 — 打开布局天堂之门？](http://dev.oupeng.com/articles/flexbox-basics "伸缩布局 — 打开布局天堂之门？")
- [跨浏览器弹性布局进阶教程](http://dev.oupeng.com/articles/advanced-cross-browser-flexbox "跨浏览器弹性布局进阶教程")
- [一个完整的Flexbox指南](http://www.w3cplus.com/css3/a-guide-to-flexbox.html "一个完整的Flexbox指南")
- [flexbox playground and code generator](http://the-echoplex.net/flexyboxes/ "flexbox playground and code generator")
- [Flexible Box Layout](http://msdn.microsoft.com/en-us/library/ie/hh772069%28v=vs.85%29.aspx "Flexible Box Layout")