---
title: "Default value of an optional parameter must be constant"
date: "2020-06-02"
categories: 
  - "flutter"
  - "flutter踩坑"
tags: 
  - "dart"
  - "flutter"
coverImage: "Default-value-of-an-optional-parameter-must-be-constant-01.png"
---

今天阿航在使用Flutter进行开发时, 希望为`final`修饰的实例变量提供默认值. 尝试过程中IDE报错:

```
Default values of an optional parameter must be constant.
```

本篇文章就来记录下碰到这种问题该如何解决!

## 错误示例

\[epcl\_box type="information"\]因为阿航出错的源码并不便于演示, 所以这里采用Stack Overflow上的简单示范, 使大家更直观的解决问题.\[/epcl\_box\]

先来看下错误源码:

```
enum MyEnum { a, b }

class ClassA {
  final MyEnum myEnum;
  ClassA({this.myEnum = MyEnum.a});
}

class ClassB {
  final ClassA classA;
  ClassB({this.classA = ClassA()}); // ClassA 报错
}
```

乍一看似乎没有什么问题, 但是实际上Dart并不允许这种写法.

## 解决方案

其实解决方案很简单, 来看下修改后的代码(注意高亮的行):

```
enum MyEnum { a, b }

class ClassA {
  final MyEnum myEnum;
  const ClassA({this.myEnum = MyEnum.a});
}

class ClassB {
  final ClassA classA;
  ClassB({this.classA = const ClassA()});
}
```

> 可以看出, 我们在`ClassA`构造函数前增加了`const`进行修饰. 并在`ClassB`设置classA的默认值时做了同样的操作.
> 
> 💡 代码解析

\[epcl\_box type="success"\]修改后再试下, 现在应该不会报错了!\[/epcl\_box\]

## 感谢

[Default values of an optional parameter must be constant](https://stackoverflow.com/questions/51907159/default-values-of-an-optional-parameter-must-be-constant) - Stack Overflow
