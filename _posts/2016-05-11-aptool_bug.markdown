---
layout: post
title:  APKTOOL的一个bug以及相关应用
date:   2016-05-11 23:58:11 +0800
tags:	 Android Apk Apktool
---


# Apktool

apktool是目前最常用的一款apk反编译的工具。

# bug简单描述

在AndroidManifest中如果我们声明如下字段

```
 <meta-data
    android:name="Atype"
    android:value="100" />
```

然后通过代码getString读取的话会抛出一个异常，这是这个Atype会被识别为int类型

当然我们可以通过修改配置，显示声明此value为String类型

```
<meta-data
    android:name="Atype"
    android:value="\ 100" />
```

然后我们使用apktool来反编译并重新编译成apktool时，我们发现

这个`\ 100`又变回了`100`

## 解决办法

解决办法有很多，比如:

- 代码中相关的try,catch方法
- 将value定义在strings.xml,使用@String来引用

## 这个bug的其他应用

关于这个bug的时候，联想到目前市面上大家都是通过apktool来反编译修改apk，我们可以给他们埋个坑，然后在app启动时读取这个参数来简单地判断当前包是否被修改过，从而选择一些行为比如：

- 直接奔溃（^.^）
- 收集数据 

