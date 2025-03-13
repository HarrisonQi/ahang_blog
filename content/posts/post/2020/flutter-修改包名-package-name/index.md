---
title: "Flutter 修改包名 package name"
date: "2020-05-22"
categories: 
  - "flutter"
tags: 
  - "flutter"
  - "上线准备"
coverImage: "Flutter-修改包名-package-name-banner.png"
---

通常使用`flutter create`命令创建新的flutter项目时, 包名是默认的`com.example`(或类似的包名). 很明显在开发一个属于自己的项目时, 这样是不对的. 需要将包名改为自己的或者所在公司的域名反写. 本篇文章就来写下如何修改Flutter的package name (包名).

## 方法一: 创建项目时指定包名

如果你还未创建项目, 或者已有项目代码量较少, 可以通过此命令来创建项目:

```
flutter create --org 你的域名反写 项目名称
```

比如:

```
flutter create --org com.bugcatt langaw
```

当然, 如果你的项目已经成型, 不便于迁移, 那么请考虑下面的方法.

## 方法二: 代码内修改

### 修改build.gradle(android)

打开`./android/app/build.gradle`, 找到类似这样的:

```
    defaultConfig {
        // TODO: Specify your own unique Application ID (https://developer.android.com/studio/build/application-id.html).
        applicationId "com.bugcatt.flutter_app_desktop"
        minSdkVersion 16
        targetSdkVersion 28
        versionCode flutterVersionCode.toInteger()
        versionName flutterVersionName
    }
```

修改其中的`applicationId`为你自己的.

\[epcl\_box type="information"\]有些同学可能已经注意到了, defaultConfig中已经给出了一个"TODO"让我们处理!\[/epcl\_box\]

### 修改Info.plist(IOS)

打开`./ios/Runner.xcodeproj`, 搜索关键字`PRODUCT_BUNDLE_IDENTIFIER`. 修改所有的:

```
PRODUCT_BUNDLE_IDENTIFIER = 包名;
```

\[epcl\_box type="notice"\]分号什么的别忘记哦!\[/epcl\_box\]

### 修改AppInfo.xcconfig(MacOS)

如果你同样开启了MacOS的桌面应用开发, 则需要本步骤!

打开`./macos/Runner/Configs/AppInfo.xcconfig`, 可以看到有三个属性:

```
// 桌面应用名称
PRODUCT_NAME = flutter_app_desktop

// 包名
PRODUCT_BUNDLE_IDENTIFIER = com.bugcatt.flutterAppDesktop

// 版权等信息
PRODUCT_COPYRIGHT = Copyright © 2020 com.bugcatt. All rights reserved.
```

自己按需修改即可哦!

## 感谢

[Pexels](https://www.pexels.com/zh-cn/photo/220685/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) 上的 [Victor Zissou](https://www.pexels.com/zh-cn/@victor-zissou-6614?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) 拍摄的照片
