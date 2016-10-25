---
layout: post
title:  iTerm2+zsh+agnoster
date:   2016-03-27 22:20:15 +0800
---


## iTerm2+zsh+agnoster

最近突然发现oh-my-zsh的新主题agnoster,的确很fancy,

![agnoster]({{ site.url }}/assets/agnoster.png)

于是迫不及待安装，本以为修改zsh_theme即可，结果没有想象中那么顺利。

## iTerm2

下面是iTerm2官网，这个自行下载安装
[iTerm](http://www.iterm2.com/)

设置颜色主题

iTerm -> preferences -> profiles -> colors -> load presets

- Solarized Dark theme
- Solarized Light theme


## oh-my-zsh

可直接使用以下命令安装

`sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"`

安装成功后修改配置文件`.zshrc`

`ZSH_THEME="agnoster"`

此时很有可能出现乱码，原因是你没有安装相应的font.

相关链接：[oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh)

## 安装powerline

下载powerline

`git clone https://github.com/powerline/fonts.git`

安装powerline

```
cd fonts
sh install.sh
```
设置iTerm2字体

iTerm -> preferences -> profiles -> Font

iTerm -> preferences -> profiles -> Non-Ascii Font

我这选用了`14 pt Melso LG M DZ Regular for Powerline`


