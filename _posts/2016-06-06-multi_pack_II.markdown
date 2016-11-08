---
layout: post
title:  Android多渠道打包
date:   2016-06-06 23:29:15 +0800
tags:	 Android Apk
---


# Android apk实现多渠道打包 ||

在之前的博客里，我们通过修改assets下的文件来实现多渠道打包，除此之外我们也可以通过修改manifest来实现多渠道打包。

例如在Application下加入如下：

```
	<meta-data android:name="channelid" android:value="100" />
```

在代码中读取

```
    ApplicationInfo appInfo = this.getPackageManager().getApplicationInfo(getPackageName(),PackageManager.GET_META_DATA);
    appInfo.metaData.getString("channelid");
```


## 修改xml

首先我们直接用`zip`解压出的特殊的二进制文件，称之为`AXML`。当然你也可以用`APKTOOL`来反编译，不过相应要花费更多的时间在解包与重打包。我们这里直接选择直接修改AXML文件。

### AXML

首先我们要了解一下这个格式，这里可以参考一下[AndroidManifest Ambiguity方案原理及代码](http://www.cnblogs.com/wanyuanchun/p/4084292.html)


这里简单说一下我们需要了解的:

- meta-data的value一般是一个`utf-16`的`string`类型
- 这个值存储在`stringchunk`的string数据块中
- string数据块已经进行过4字节对齐(即人为地填充了几个0x00)
- string的长度会影响`stringchunk`的长度


## 重打包

### 主要思路

我们可以用一个通用的足够长的string作为这个标识符,来通过替换这个string来实现修改AXML，具体可以参考博文
[另辟蹊径实现Android多渠道打包](https://yrom.net/blog/2015/05/25/the_other_way_to_package_multi_channel_apks/)

### 步骤

- 删除apk的签名
- 复制apk里的AndroidManifest.xml文件
- 删除apk中的AndroidManifest.xml
- 替换AndroidManifest.xml文件中的replaceStr
- 将替换后的AndroidManifest.xml压入apk
- 重签名
- zipalign

