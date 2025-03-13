---
title: "Flutter介绍"
date: "2020-07-03"
---

## 简介

**Flutter**是一个由谷歌开发的开源移动应用软件开发工具包，用于为Android、iOS、 Windows、Mac、Linux、Google Fuchsia开发应用。

Flutter第一个版本支持Android操作系统，开发代号称作“Sky”。 它于2015年4月的Flutter开发者会议上被公布，宣称其目标为实现120FPS的渲染性能。在上海Google Developer Days的主题演讲中，Google宣布了Flutter Release Preview 2，这是Flutter 1.0之前的最后一个重要版本。2018年12月4日，Flutter 1.0在Flutter Live活动中发布，是该框架的第一个“稳定”版本。2019年12月11日，在Flutter Interactive活动上发布了Flutter 1.12，宣布Flutter是第一个为环境计算设计的UI平台。

## 框架组织

Flutter的主要组成部分包括：

- Dart平台
- Flutter引擎
- 基础库
- 定制化设计语言的组件

### Dart平台

Flutter应用是使用Dart语言编写的，并利用了该语言的许多高级功能。

在Windows、macOS和Linux上，通过半官方的_Flutter Desktop Embedding_项目，Flutter在Dart虚拟机中运行，该虚拟机具有即时编译执行引擎。在编写和调试应用时，Flutter使用即时编译功能进行“热重载”，可以将对源文件的修改注入正在运行的应用中。Flutter通过支持有状态的热重载来扩展此功能，在大多数情况下，对源代码的更改可以立即在运行的应用中反映出来，而无需重新启动或丢失任何状态。Flutter实现的此功能已广受赞誉。

Flutter应用的发布版本在Android和iOS上都进行了提前（AOT）编译，使Flutter在移动设备上可以高性能地运行。

### Flutter引擎

Flutter的引擎主要使用C++开发，通过Google的Skia图形库提供底层渲染支持，亦提供平台相关的SDK，例如Android和iOS。Flutter引擎是用于托管Flutter应用的可移植的运行环境。它实现了Flutter的核心库，包括动画和图形、文件和网络I/O、可访问性支持、插件架构以及Dart运行环境和编译工具链。大多数开发人员将通过Flutter框架与Flutter进行交互，该框架提供了一个现代、响应式的框架，以及一组丰富的平台、布局和基础组件。

### 基础库

基础库由Dart编写，提供了用Flutter构建应用所需的基本的类和函数，例如与引擎通讯的API。

#### 组件

Flutter是通过组织、创建不同的组件完成用户界面设计的。在Flutter中，一个组件代表用户界面中不可变的一部分；包括文本、多边形以及动画在内的所有图形都是用组件创建的。复杂的组件由简单的组件结合而成。

### 定制化设计风格的组件

Flutter框架包含了两套符合特定设计语言的组件。 称作Material Design的组件实现的是同名的谷歌设计语言，称作_Cupertino_的组件实现苹果公司iOS的扁平化设计（Flat Design）。

## Hello World示例

一个Flutter中的Hello World程序如下所示：

    `import 'package:flutter/material.dart';  void main() => runApp(HelloWorldApp());  class HelloWorldApp extends StatelessWidget {   @override   Widget build(BuildContext context) {     return MaterialApp(       title: 'Hello World App',       home: Scaffold(         appBar: AppBar(           title: Text('Hello World App'),         ),         body: Center(           child: Text('Hello World'),         ),       ),     );   } }`

\[epcl\_box type="information"\] 本文转自维\_基\_百\_科. 最后修订于2020年6月19日 (星期五) 09:25\[/epcl\_box\]
