---
title: "Flutter 踩坑 A package may not list itself as a dependency"
date: "2020-04-10"
categories: 
  - "flutter"
  - "flutter踩坑"
tags: 
  - "app开发"
  - "flutter"
  - "踩坑"
---

在使用 Flutter 开发APP时, 运行`flutter package get`命令, 控制台报了 A package may not list itself as a dependency 的错误.

## 问题展示

运行`flutter package get`, 控制台报错如下:

```plaintext
Because my_app depends on my_app which doesn't exist (could not find package my_app at http://pub.dartlang.org), version solving failed.
pub get failed (1; could not find package my_app at http://pub.dartlang.org)
exit code 1

A package may not list itself as a dependency
```

## 原因

检查你的Flutter项目, 是否与即将导入的第三方库重名.

## 解决方案

### 方案一: 修改项目名 (推荐)

修改你的项目名称. 这种方法虽然会很麻烦, 但是毕竟人家的项目先上传的😅😅.

### 方案二: 寻找功能相似的第三方库(不推荐)

寻找功能相似的第三方库(不推荐)

## 结语

对文章若有任何问题、异议以及改进建议, 欢迎在下方进行评论. 作者将尽快回复! 获取最新文章, 欢迎阅读[官方博客](/post/2020/flutter-a-package-may-not-list-itself-as-a-dependency/).

更多更好的教程/博客/资讯, 欢迎访问我的官网: [阿航的技术小站](/)
