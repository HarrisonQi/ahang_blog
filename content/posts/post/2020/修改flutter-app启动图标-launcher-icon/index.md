---
title: "修改Flutter APP启动图标/Launcher Icon"
date: "2020-12-10"
categories: 
  - "flutter"
  - "flutter-actual-combat"
tags: 
  - "flutter"
---

## 开门见山

为了简化修改Flutter启动图标的过程, `Flutter Launcher Icons`诞生了.

## 开始

访问 [Flutter Launcher Icons 库网址](https://pub.dev/packages/flutter_launcher_icons) . 访问慢的同学可以使用[国内镜像](https://pub.flutter-io.cn/packages/flutter_launcher_icons).

修改你的`pubspec.yaml`文件(版本号替换为最新的):

    ` dev_dependencies:   flutter_launcher_icons: ^0.8.1`

在资源目录中创建你的icon文件, 比如路径`assets/icon/icon.png`.

然后再次修改`pubspec.yaml`:

    ` flutter_icons:   android: "launcher_icon"   ios: true   image_path: "assets/icon/icon.png"`

在终端中分别运行以下命令:

    `flutter pub get`

    `flutter pub run flutter_launcher_icons:main`

## 其他资源

- [点击此处](https://github.com/fluttercommunity/flutter_launcher_icons/tree/master/example)查看完整示例项目
- 如果使用该库出现任何问题, 请[提issue](https://github.com/fluttercommunity/flutter_launcher_icons/issues)
