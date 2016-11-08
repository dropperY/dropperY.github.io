---
layout: post
title:  Xcode8中使用CoreData
date:   2016-11-11 22:20:15 +0800
tags:	 Xcode swift CoreData 
---


# Xcode8中使用CoreData

在Xcode8中想使用CoreData遇到了问题，我像以前一样新建entity之后使用`Editor`->`Create NSManagedObject SubClass`之后编译，提示如下错误：

```
 error: filename "XXX+CoreDataClass.swift" used twice:'
```


研究了一下发现，Xcode8开始会自动替我们生成数据库entity相对应的class. 你新建一个entity, 会在你`的DerivedData` > `Build` > `Intermediates` > `.Build`.产生如下三个文件

- `COREDATA_DATAMODELNAME_+CoreDataModel.swift`
- `EntityName+CoreDataClass.swift`
- `EntityName+CoreDataProperties.swift`

于是你创建的文件就与之重复


## 解决办法

目前强烈建议关闭此功能。

![agnoster]({{ site.url }}/assets/img/xcode8_coredata.png)

另外Xcode8有一个bug,就是你必须修改一下这个entity任意属性，这个控制autogen的value才会被保存，坑！

另外`build`前记得`clean`,不然那些文件不会被重新生成也不会被删除，坑+1！

有关StackOverFlow:

- If you change the Codegen dropdown, it's new value isn't saved in Model.xcdatamodel. You have to change something else to get it to save. For example change the class name; build; change the class name back; build again.

- The generated code is placed in DerivedData in the Intermediates folder, but it only happens if the folder doesn't already exist. The workaround is to do a clean then a build.

[相关链接](http://stackoverflow.com/a/39394426)



