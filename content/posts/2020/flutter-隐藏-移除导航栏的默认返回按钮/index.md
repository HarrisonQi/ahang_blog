---
title: "Flutter 隐藏/移除导航栏的默认返回按钮"
date: "2020-06-19"
categories: 
  - "flutter"
  - "flutter-actual-combat"
tags: 
  - "flutter"
  - "常用操作"
  - "常用组件"
---

在实际项目开发中, 我们在进行页面跳转时, 偶尔会跳到不可返回的页面(比如退出登录后). 本篇文章就来记录下 Flutter 如何隐藏/移除导航栏的默认返回按钮.

## 效果

有图有真相, 先来看下实际效果:

## 应用场景

移除导航栏的默认返回按钮适用于:

- 退出登录后禁止返回
- 跳转至一个全新的页面, 不可返回
- 禁止返回的任何页面

## 需具备的条件

- 掌握Flutter基础
- 掌握Flutter页面跳转的基本操作

本篇文章的环境:

| 环境 | 版本 |
| --- | --- |
| Flutter | 1.19.0-2.0.pre |

## 实战开始

### 准备工作

创建新文件`./lib/main.dart`(或者其他你想要的文件名):

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Remove back button',
      home: FirstPage(),
    );
  }
}

class FirstPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("First Page"),
      ),
      body: Center(
        child: RaisedButton(
          child: Text("跳转到下一页"),
          onPressed: () {
            Navigator.push(context, MaterialPageRoute(builder: (context) {
              return SecondPage();
            }));
          },
        ),
      ),
    );
  }
}

class SecondPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Second Page"),
      ),
    );
  }
}
```

🟢 运行, 可以看到demo提供了正常跳转:

![](images/Flutter-移除导航栏的默认返回按钮-01.gif)

### 方法一: 替换AppBar的leading

找到`SecondPage`, 为其AppBar传入`leading`:

```dart
appBar: AppBar(
  leading: Container(),
  title: Text("Second Page"),
),
```

<figure>

![](images/Flutter-移除导航栏的默认返回按钮-02.png)

<figcaption>

代码截图

</figcaption>

</figure>

> `leading`是AppBar的一个可选参数. 传入的widget将置于`title`前. 我们巧妙的传入了一个空的Container来达到替换返回按钮的效果.
> 
> 💡 代码解析

🟢 运行, 可以看到返回按钮不见了:

![](images/Flutter-移除导航栏的默认返回按钮-03.gif)

\[epcl\_box type="notice"\]这种方法存在两个缺陷: 第一个就是标题前方会有空白. 第二个就是按物理返回键仍能返回至上一页.\[/epcl\_box\]

虽然这种方法代码非常简洁, 但是可能无法完全满足我们的需求.

### 方法二: Navigator.pushAndRemoveUntil()

如果你尝试了方法一, 请先移除此行:

```dart
leading: Container(),
```

找到`FirstPage`, 替换:

```dart
Navigator.push(context, MaterialPageRoute(builder: (context) {
  return SecondPage();
}));
```

为:

```dart
Navigator.pushAndRemoveUntil(context,
    MaterialPageRoute(builder: (context) {
  return SecondPage();
}), (route) => route == null);
```

<figure>

![](images/Flutter-移除导航栏的默认返回按钮-04.png)

<figcaption>

代码截图

</figcaption>

</figure>

> `Navigator._push_()`和`Navigator._pushAndRemoveUntil_()`的不同之处就是, push会保留之前的页面, 而_`pushAndRemoveUntil`_将会移除之前的页面. 使Flutter无法找到之前的页面, 从而达到去除返回键的目的.
> 
> 💡 代码解析

🟢 运行项目, 可以看到导航栏返回按钮消失, 并且按物理返回键会直接退出APP:

![](images/Flutter-移除导航栏的默认返回按钮-05.gif)

\[epcl\_box type="success"\]搞定啦!\[/epcl\_box\]

## 感谢

[flutter remove back button on appbar](https://stackoverflow.com/questions/44978216/flutter-remove-back-button-on-appbar) 