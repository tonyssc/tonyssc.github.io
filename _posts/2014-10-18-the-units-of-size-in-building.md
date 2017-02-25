---
layout: post
title: "深入理解CSS中的尺寸单位"
date: 2014-10-19 9:30:00
---

最近在移动端的页面开发过程中使用了较多的相对尺寸单位，发现配合移动端页面的响应式特点效果比较好。本来只想介绍这些新的尺寸单位，后来想想还是让那些基础的尺寸单位也露露脸，搭个顺风车。

##常见的尺寸单位：

- % -- 百分比
- in -- 寸
- cm -- 厘米
- mm -- 毫米
- pt(point) -- 大约1/72寸
- pc(pica) -- 大约6pt, 1/6寸
- px -- 屏幕的一个像素点
- em -- 相对单位
- ex -- font-size的x-height值，为小写字母x的高度，通常相当于font-size的一半

<!--break-->

介绍了这么多只是希望大家对尺寸单位有个整体的了解，其实日常开发中我们熟悉的尺寸单位无非是以下这三种：px / % / em

px就不多说了，制作一个固定尺寸的页面就靠它了。包括字体的大小，行高，容器的宽高等等...

%和em都表示一个相对单位，都是基于某个值来计算当前元素的尺寸的，让我们先看几个例子：

    .percent { font-size: 150%; } // 字体大小为父元素的150%
    .em { font-size: 1.5em; } // 字体大小为父元素的1.5倍

上边这个例子中150%和1.5em得到的结果是一致的。那么新的问题就出现了，我们都知道，当行高为文字大小的1.5倍的时候，用户阅读起来会更舒服，因此我们经常设置line-height: 1.5，那么line-height: 1.5和line-height: 150%或者line-height: 1.5em有什么区别呢？

    body { font-size: 14px; }
    .px-line-height { line-height: 15px; }
    .em-line-height { line-height: 1.5em; }
    .percent-line-height { line-height: 150%; }
    .nounits-line-height { line-height: 1.5; }
    pre { font-size: 30px; }
    
    <div class="px-line-height">
        <pre>
        测试
        情况为line-height:15px时
        </pre>
    </div>
    <div class="em-line-height">
        <pre>
        测试
        情况为line-height:1.5em时
        </pre>
    </div>
    <div class="percent-line-height">
        <pre>
        测试
        情况为line-height:150%时
        </pre>
    </div>
    <div class="nounits-line-height">
        <pre>
        测试
        情况为line-height:1.5时
        </pre>
    </div>

结果如下图：

<img src="/public/images/line-height.png" style="width:458px;height:561px;">

从图中我们得到的结论就是：

百分比和em在计算line-height时会根据父元素的font-size计算，然后将结果赋给line-height属性，而没有单位的倍数会根据子元素的font-size动态计算line-height属性值。

##CSS3中的尺寸单位

- ch -- 字符0的宽度
- rem -- 根据根元素(html)font-size计算的值, 相对单位
- vw -- viewport width, 根据视口宽度计算的值, 1vw相当于视口宽度的1%
- vh -- viewport height, 根据视口高度计算的值, 1vh相当于视口高度的1%
- vmin -- vw和vh中较小的那个值
- vmax -- vw和vh中较大的那个值

这里我们着重介绍rem和vw、vh这几个单位, 这三个单位都适合用在移动端开发中，因为移动端的页面要求要兼容多个尺寸的移动设备，而相对单位又是响应式的必备工具。

###rem

使用过em或%单位布局的同学都应该知道，它们会根据父元素进行相应的尺寸计算，计算深度会一级一级的叠加，如果不能很清楚的理清每层的相对数值，最后会出现不小的偏差，而且变得很难维护。rem则是在em的基础上进行的扩展，r=root。从字面上就可以理解rem是针对根元素(html)进行尺寸的计算，在开发中只需要设置html元素的字体大小，在后续的开发中都可以根据这个相对值进行尺寸的设定，例如：

    html { font-size: 0.625rem; } // 浏览器默认的字体大小是16px，0.625 * 16 = 10

这里只是一个参考值，将基数定为10便于后续的尺寸计算。比如：h1标签的字体需要20px，则可以设置：

    h1 { font-size: 2rem; } // 10 * 2 = 20

###vw vh vmin vmax

先让我们看看w3c是如何描述它们的：

####vw
>Equal to 1% of the width of the initial containing block

####vh
>Equal to 1% of the height of the initial containing block.

####vmin
>Equal to the smaller of ‘vw’ or ‘vh’.

####vmax
>Equal to the larger of ‘vw’ or ‘vh’.

首先我们要知道，vw和vh中所说的viewport指的是window.innerWidth和window.innerHeight。即不包括浏览器顶部任务标题栏及底部状态栏的可视区域。

接下来看看这几个属性可以用在什么地方：

场景一：弹层和弹层蒙版

我们都实现过弹层的功能，大多数弹层会在加载的时候为页面遮盖一层蒙版。我们只需要将蒙版定位到屏幕左上角，然后给它设置width: 100vw和height: 100vh即可。其实这个可以理解为只要是和屏幕尺寸相关的动态值都可以使用vw和vh，也包括宽高自适应的弹层。

场景二：元素尺寸限制

一个缩略图，点击后查看原图。当原图尺寸太大的时候，就会超出父容器的限制。在这种情况下，可以使用

    img { max-height: xxx vh; } // 通过最大高度限制图片的高宽

关于rem和vw浏览器兼容情况可以参考[caniuse](http://caniuse.com/), 更多场景及问题详见参考链接中的[视区相关单位vw, vh..简介以及可实际应用场景](http://www.zhangxinxu.com/wordpress/2012/09/new-viewport-relative-units-vw-vh-vm-vmin/ "视区相关单位vw, vh..简介以及可实际应用场景")。

##结语

移动互联的时代已经到来了，作为一个前端攻城师，我们更应该跟上时代的步伐。有了高级浏览器的支持，我们便可以肆无忌惮的尝试更多更方便的属性和方法。最后，希望大家都能够找到精确度量自己的那个“单位”。

##参考链接

- [The New CSS3 Relative Font Sizing Units](http://www.sitepoint.com/new-css3-relative-font-size/ "The New CSS3 Relative Font Sizing Units")
- [CSS Values and Units Module Level 3](http://www.w3.org/TR/2013/CR-css3-values-20130730/#font-relative-lengths "CSS Values and Units Module Level 3")
- [Can i use vw](http://caniuse.com/#search=vw "Can i use vw")
- [视区相关单位vw, vh..简介以及可实际应用场景](http://www.zhangxinxu.com/wordpress/2012/09/new-viewport-relative-units-vw-vh-vm-vmin/ "视区相关单位vw, vh..简介以及可实际应用场景")