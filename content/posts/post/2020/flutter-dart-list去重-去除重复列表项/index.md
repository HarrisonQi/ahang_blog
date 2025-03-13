---
title: "Flutter/Dart List去重, 去除重复列表项"
date: "2020-07-20"
categories: 
  - "flutter"
  - "flutter-actual-combat"
tags: 
  - "flutter"
  - "常用操作"
---

有时我们需要过滤掉重复的列表项, 本篇文章就来介绍下Flutter/Dart 如何进行 List去重, 去除重复列表项.

## 实战开始

### 方法一: List与Set互转

基于Set集合的不可重复特性, 我们利用该特性可轻松解决:

    `void main() {   // 声明一个集合   var ids = [1, 1, 4, 4, 5, 6, 6];   // 进行去重, 存储去重后的集合   var distinctIds = ids.toSet().toList(); }`

当然, 基于该思路还有更牛逼的写法:

    `var distinctIds = [...{...ids}];`

\[epcl\_box type="success"\]这也许是最优雅的解决方案.\[/epcl\_box\]

### 方法二: List与Set互转(保留顺序)

方案一虽然优雅, 但也不是完美的. 它无法**保留顺序**. 如果我们的需求对顺序有绝对的要求时, 就需要以下方法了:

    `import 'dart:collection'; void main() {   // 声明一个集合   List arr = ["a", "a", "b", "c", "b", "d"];   // 进行去重, 存储去重后的集合   List result = LinkedHashSet.from(arr).toList(); }`

虽然不如方法一优雅, 但是其保留了顺序.

\[epcl\_box type="success"\]虽然不如方法一优雅, 但是其保留了顺序.\[/epcl\_box\]

## 感谢

[How to delete duplicates in a dart List? list.distinct()?](https://stackoverflow.com/questions/12030613/how-to-delete-duplicates-in-a-dart-list-list-distinct)
