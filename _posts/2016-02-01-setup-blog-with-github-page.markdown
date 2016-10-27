---
layout: post
title:  基于github以及Jekyll搭建自己的博客
date:   2016-02-01 18:20:05 +0800
---


其实网上有很多相关的教程，都比较详细

这里简单介绍一下自己github pages搭建博客的流程与遇到的坑


## 创建github repository 


GitHub Pages分两种，一种是你的GitHub用户名建立，另一种是依附项目的pages。这里我们使用第一种，
新建一个名为`username.github.io`的工程。

![create-github-page-repo]({{ site.url }}/assets/img/create-github-page-repo.png)

注意:必须新建一个新的工程，别的工程改名为`username.github.io`也是没有用的T.T。
创建完可以访问一下`username.github.io`确认能否正常访问.

如果无法访问，可以看一下repo的settings,正常情况应该像下面这样

![github-page-repo-settings]({{ site.url }}/assets/img/github-page-repo-settings.png)


## 安装Jekyll


因为本人使用的mbp, 这里主要介绍Mac OS X下面的安装过程。其他操作系统可以参考官方文档。

相关链接：[Jeklly官网](<http://jekyllrb.com/docs/installation/>)

Mac下，我们可以直接通过Gem安装Jekyll

```
gem install jekyll
```

一般情况下你肯定无法直接安装成功T.T

1. 确认安装过了Xcode的command line tools
2. 确认gem的源，基于某些原因，我们选择使用taobao的镜像

```
sudo gem sources --remove http://rubygems.org/
sudo gem sources -a http://ruby.taobao.org/
```

此时安装过程仍有可能`Failed to build gem native extension`, 这个错误的原因多种多样, 需要根据具体的错误信息
才能解决。
不过我建议使用rvm来安装，可以较快解决这个问题，rvm可以使用下面的命令安装：

```
 curl -L https://get.rvm.io | bash -s stable --ruby
```

如果一切顺利，本地的jeklly环境就搭建完成了。

## 使用Jekyll创建博客


首先clone一开始新建的repo

```
git clone https://github.com/username/username.github.io.git myBlog
```

创建工程

```
cd myBlog
jekyll new .
```

启动jekyll

```
jekyll serve
```

此时打开浏览器输入`http://localhost:4000`见能访问你的博客了








