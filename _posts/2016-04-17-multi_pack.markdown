---
layout: post
title:  Android多渠道打包
date:   2016-04-17 22:20:15 +0800
tags:	 Android Apk
---


# Android apk实现多渠道打包

因为google play在国内的特殊情况，导致国内应用市场繁多。于是不可避免的出现了针对不同应用市场生成不同的包的需求，如果每次都重新编译生成一个apk的话速度很慢，这里我们简单介绍一个方法。


## 添加配置文件
通过配置文件来确定当前渠道，然后通过读取该文件的参赛来动态识别当前渠道。

比如我们可以在`assets`下放一个`config.txt`的文件,内容如下：

```
channelid=1
```

至于如何读取该文件，并且更强渠道号的相关操作这里不做涉及

最后我们假设我们的apk为`demo.apk`


## 重打包

### 步骤

- 删除apk的签名
- 删除apk中的config.txt
- 添加新的config.txt到apk中
- 重签名
- zipalign

### 删除签名

```
zip -d temp.apk "META-INF/*"  
```

### 删除config

```
zip -d temp.apk assets/config.txt
```

### 添加新的config

```
mkdir assets
echo "channelid=2" >> assets/config.txt
zip -g temp.apk assets/config.txt
rm -rf assets
```

### 重签名

重签名命令如下

```
JAVA_HOME/bin/jarsigner -keystore your.keystore -storepass yourStorepass -keypass yourKeypass  -signedjar temp_signed.apk temp.apk yourAlias -verbose 
```

## 好处

- 无需重新编译，快速
- 同时可以扩展，添加任意图片，音频等文件，不局限于文本


