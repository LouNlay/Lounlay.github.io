---
layout: post
title:  如何使用LessOrMore这个Jekyll模版
date:   2019-3-20 12:51:50 +0800
categories: 博客搭建
tag: 教程
---

* content
{:toc}


昨天搭建了属于自己的博客，在这里将过程记录下来

  

**1.新建一个Repository**

在 GitHub上 新建一个 Repository![](https://lounlay.github.io/images/newRepository.png)

Repository 的名字一定要是 username.github.io，其中 username 是账号的名称，如图所示，我的名称为 LouNlay.github.io。

  

Description 是描述信息，选填信息。

  

Public 和 Private 是所创建 Repository 的可视权限，public 是所有人可见，private 是必须授权才可见，这里要做博客需要选择 public。

  

Initalize this repository with a README 这个选项的意思是否初始化的时候创建README.md文件，这里不勾选，创建一个空的 repository 即可，点击完成。

  

官方教程：


[https://pages.github.com/](https://pages.github.com/)


  

**2.从Jekyll中选择一个自己喜欢的主题**  


[http://jekyllthemes.org/](http://jekyllthemes.org/)


将自己选择的主题下载并解压，上传到刚刚创建的 repository 中。我这里使用的工具是 git，步骤如下。

  

**2.1首先将刚刚创建的项目clone到本地**

```
git clone git@github.com:username/username.github.io.git
```

下载到本地是空的，文件夹中只有一个隐藏的.git文件夹。  

  

**2.2修改配置文件**

打开 _config.yml 文件（yml文件通过缩进来表示层级关系，比较简洁易读），修改配置信息，我下载的主题：

```
git clone https://github.com/luoyan35714/LessOrMore.git
```

  

需要修改的配置信息说明：  

```

    name: 博客名称
    email: 邮箱地址
    author: 作者名
    url: 个人网站
    # baseurl修改为项目名，如果项目是'***.github.io'，则设置为空''
    baseurl: "/LessOrMore"
    resume_site: 个人简历网站
    github: github地址
    github_username: github用户名称
    # 请到百度统计官网[https://tongji.baidu.com/](https://tongji.baidu.com/)申请自己的网站ID并在此处替换，否则将无法正常统计访问量
    baidu_analysis: 94be4b0f9fc5d94cc0d0415ea6761ae9
    # 请到revolvermaps [http://www.revolvermaps.com/?target=setupgl](http://www.revolvermaps.com/?target=setupgl)申请自己的网站ID并在此处替换，否则将无法正常统计访问量
    revolvermaps: 5ytn1ssq6za

```

修改完毕后将全部文件复制到之前下载下来的空目录中。

  

**2.3上传**

命令如下：

```
git add --all
```

提交到 github 上之后会自动构建，直接访问 https://username.github.io 就可以访问到自己的博客了。  

  

**3.使用gitalk为博客添加评论系统**

**3.1注册**

```
https://github.com/settings/applications/new
```

![](https://lounlay.github.io/images/newApplication.png)  

点击 Register application 按钮后，会自动跳转到详细信息页面。接下来需要使用的是 Client ID 和 Client Secret （其实这不是什么机密信息，在使用中都是以明文传输的）
![](https://lounlay.github.io/images/id.png)

**3.2将注册信息配置进项目中**

一般是在 _layout 文件夹下的 post.html 文件中，也要在文件中引用下列代码：

```
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/gitalk@1/dist/gitalk.css">
<script src="https://cdn.jsdelivr.net/npm/gitalk@1/dist/gitalk.min.js"></script>
```

上面的是 gitalk 的 css 样式，下面的是 gitalk 的 js 文件，下面的代码需要这俩文件的支持，不然无法正常运行。  

  

下面是我的代码，可以参考下：

```
{% if site.comments.gitalk %} //通过参数控制评论是否开启
{% endif %}
```

这段代码是我 copy 的一个博客上的，原文地址：  


[https://blog.csdn.net/Madridcrls7/article/details/80871596](https://blog.csdn.net/Madridcrls7/article/details/80871596)


  

这里使用了配置文件中的配置信息，就是上面的 site.comments.* 的内容，配置信息其实可以自定义，配置信息又是我从另外一个地方 copy 来的，原文地址：


[https://weijunzii.github.io/2018/06/29/Add-Gitalk-In-Jekyll-Theme-H2O.html](https://weijunzii.github.io/2018/06/29/Add-Gitalk-In-Jekyll-Theme-H2O.html)


注意，这里 id 参数使用了 md5() 这个方法处理，这是因为id长度不能超过50，这里的参数就是对应的文件名，为了好辨别，文件名的长度有时候会超过50，所以这里用这个方法处理一下不会出现因为文件名过长而导致的 Error:Validation Failed 错误。同时也要注意不要忘记引用 md5.min.js这个 js 文件，文件内容可以在网上轻易获取，这是我项目中的：


[https://github.com/LouNlay/Lounlay.github.io/blob/master/styles/js/md5.min.js](https://github.com/LouNlay/Lounlay.github.io/blob/master/styles/js/md5.min.js)


记得放置到对应的引用路径下。  

  

修改完毕后，将修改内容上传到 github 上，稍后刷新博客主页，然后打开具体文章，最下面就能看评论框了。

  

在搭建过程中会遇到一些问题，我在网上搜索问题的时候觉得这篇文章写得特别好，遇到问题的时候可以参考下。文章链接：


[https://zhwangart.github.io/2018/12/06/Gitalk/](https://zhwangart.github.io/2018/12/06/Gitalk/)


  

博客的搭建到这里已经完成，关于写博客的方法，排版，等我学会后再来更新（如果我能坚持的话）。
