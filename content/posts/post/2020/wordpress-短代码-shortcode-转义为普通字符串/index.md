---
title: "WordPress 短代码 shortcode 转义为普通字符串"
date: "2020-06-23"
categories: 
  - "wordpress"
tags: 
  - "wordpress"
  - "博客排版"
  - "字符转义"
---

在使用WordPress进行创作时, 阿航碰到了需要将短代码转为普通字符展示在文章内. 本篇文章就来记录下如何将WordPress的短代码转义为普通字符串.

## 效果

将短代码转为普通字符串, 展示在屏幕上的 3 个方案的 2 种效果:

* * *

\[\[epcl\_box type="information"\]这是一条被短代码包住的信息!\[/epcl\_box\]\]

* * *

```
[epcl_box type="information"]这是一条被短代码包住的信息![/epcl_box]
```

* * *

## 场景

阿航的网站上有这样的提示短代码:

\[epcl\_box type="information"\]这是一条被短代码包住的信息!\[/epcl\_box\]

在转义前, 我们是这样输入的:

```
[epcl_box type="information"]这是一条被短代码包住的信息![/epcl_box]
```

很明显, 这样输入会被WordPress自动转为短代码.

## 需具备的条件

- 你掌握WordPress的基础使用

本篇文章的环境:

<table class=""><tbody><tr><td>Wordpress</td><td>5.3.3</td></tr></tbody></table>

## 解决方案

### 方案一: 被"<code>"包裹

此方案非常简单, 只要我们使用`<code></code>`标签将短代码括住, 代码将被自动转义, HTML写法 (区块编辑器直接找"代码"区块, 输入即可) :

```
<code>
    [epcl_box type="information"]这是一条被短代码包住的信息![/epcl_box]
```

效果:

* * *

```
[epcl_box type="information"]这是一条被短代码包住的信息![/epcl_box]
```

* * *

\[epcl\_box type="success"\]顺利搞定!\[/epcl\_box\]

### 方案二: 被"\[\]"包裹

此方案也相当简单, 我们在短代码外包裹一层"`[]`". 写法改为:

```
[[epcl_box type="information"][/epcl_box]]
```

效果:

* * *

\[\[epcl\_box type="information"\]这是一条被短代码包住的信息!\[/epcl\_box\]\]

* * *

\[epcl\_box type="success"\]搞定! 本方法相当方便!\[/epcl\_box\]

### 方案三: 使用转义字符串

此方法需要我们的重点就是把`[`和`]`转为转义字符串. 一张表格查看对应关系:

| 转义前 | 转义后 |
| --- | --- |
| \[ | `&#91;` |
| \] | `&#93;` |
| \[shortcode\] | `&#91;shortcode&#93;` |

那么, 我们上述例子的最终写法应为:

```
&#91;epcl_box type="information"&#93;这是一条被短代码包住的信息!&#91;/epcl_box&#93;
```

效果:

\[epcl\_box type="information"\]这是一条被短代码包住的信息!\[/epcl\_box\]

### 方案优劣势对比

| 方案 | 优势 | 劣势 |
| --- | --- | --- |
| 方案一:  
使用`<code>` | 1\. 最简单的方法. WordPress原生支持, 不需要任何其他复杂的操作.  
2\. 可读性最好. 便于后续编辑. | 不够灵活, 只能存在于`<code>`块内部. |
| 方案二:  
使用`[]` | 1\. 同样简单的方法, 只需在外层添加`[]`.  
2\. 可读性较好, 便于后续编辑.  
3\. 自由度较高, 可放置于任意地点. | 需要在编辑器内部添加多余的括号. |
| 方案三:  
使用转义 | 1\. 最"程序员"的方法, 直接使用十进制字符进行转义.  
2\. 不破坏原先的代码. 可移植性好.  
3\. 自由度较高, 想怎么写就怎么写. | 1\. 可读性极差. 甚至在编辑时需要整个转义为看得懂的字符才能继续编辑,  
2\. 有使用门槛, 需要对照字符转义表. 非程序员可能会踩坑. |

如果你对字符转义不熟, 或者不想折腾, 推荐**方案一**以及**方案二**.

## 感谢

[How to Escape Shortcodes in When Posting Code Snippets in WordPress](https://havecamerawilltravel.com/photographer/escape-shortcodes-wordpress/)
