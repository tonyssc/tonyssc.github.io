---
layout: post
title: "Github my pages -- Jekyll"
date: 2014-08-20 10:12:00
---

![jekyll](/public/images/jekyll-logo-light-transparent.png)

在上篇文章中我提到了搭建一个github pages所用到的东西，从这篇开始将逐一介绍每一个知识点。首先要声明一下：网上关于搭建github pages的文章很多，有些已经介绍的很详细了。我只是将我认为重要的环节和我在搭建过程中遇到的一些问题记录下来，关于那些基本概念和基础的操作将略过，本文的最后会列出我在建站过程中阅读的文章链接供大家参考。

<!--break-->

##Github pages是什么？
github pages可以看做是用户编写的，托管在github上的静态网页。github为用户提供了现成的pages模板，当然它也允许用户自己编写页面，然后上传。重要的是，这种上传并不是单纯的文件上传，而是会经过Jekyll程序的再处理。

##Jekyll是什么？
搭建一个github pages，最核心的就是使用一个站点的发布器，其他功能(比如评论)都是作为插件丰富我们的网站。Jekyll就起到的静态站点发布器的作用，它会根据网页源代码生成静态的文件，并且提供了模板、变量、插件等功能。因此，抛开网站中的辅助功能，只使用Jekyll就可以完成一个站点的搭建。了解以上两点，我们建站的思路就很明确了：

1. 在本地编写符合Jekyll规范的网站代码；
2. 将页面上传到github，由github生成并托管我们的网站。

###安装Jekyll

安装Jekyll最好的方式是RubyGem：

    $ gem install jekyll

###使用Jekyll

一个典型的Jekyll站点通常具有如下结构：

    .    
    |--  _config.yml
    |--  _includes
    |     |--  header.html
    |--  _layouts
    |     |--  default.html 
    |--  _posts
    |     |--  2014-08-19-hello-world.html
    |--  _site
    |--　index.html

####_config.yml

Jekyll的配置文件，详细解释参考[Jekyll config](http://jekyllrb.com/docs/configuration/ "Jekyll config")

####_includes

该文件夹存放可以与_layouts和_posts混合、匹配使用的文件，也可以称为结构碎片。比如站点的头部(head.html)，底部(footer.html)等等。

####_layouts

该文件夹存放站点的布局模板文件，比如通用模板(default.html)，首页模板(index.html)，文章模板(post.html)等等。

####_posts

该文件夹存放所有的博客文章，博客文件名必须遵循：YEAR-MONTH-DATE-TITLE.后缀名(如果网页代码采用html格式，后缀名为html。如果采用[markdown](http://daringfireball.net/projects/markdown/ markdown)格式，后缀名为md)。每一个帖子的固定链接URL可以作弹性的调整，但帖子的发布日期和转换所使用的标记语言会根据且仅根据文件名中的相应部分来识别。

####_site

该文件夹是Jekyll用以存放最终生成站点静态文件的地方(Jekyll的站点文件中，没有以"下划线 _"开头的文件夹最终都会被放到 _site)。建议将该文件夹添加到.gitignore列表。

####index.html

顾名思义，每个站点都需要一个首页。

至于如何编写模板、碎片以及首页等，可以参考我的[github pages](https://github.com/tonyssc/tonyssc.github.com/)，也可以参考[jekyll bootstrap](https://github.com/plusjade/jekyll-bootstrap/)。

###运行Jekyll

进入你的站点目录中，运行：

    $ jekyll server

或者：

    $ jekyll server -w

加入-w参数，jekyll会自动监听文件的变动，可以方便的让用户即时预览修改后的页面。然后在浏览器中输入http://localhost:4000即可访问你的站点。

当然jekyll还有很多其他的参数选项可以使用，更多用法参考[Jekyll Basic Usage](http://jekyllrb.com/docs/usage/)。

本篇文章主要介绍了Jekyll的目录结构和基本用法。在接下来的文章中会着重介绍站点中模板的组织方式和结构碎片的编写。

####参考链接

- [github Pages和Jekyll入门](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html "github Pages和Jekyll入门")
- [Github Pages](https://pages.github.com/ "Github Pages")
- [Github Pages极简教程](http://yanping.me/cn/blog/2012/03/18/github-pages-step-by-step/ "Github Pages极简教程")