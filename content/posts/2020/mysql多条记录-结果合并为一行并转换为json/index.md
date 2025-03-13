---
title: "MySQL多条记录/结果合并为一行,并转换为JSON"
date: "2020-07-14"
categories: 
  - "mysql"
  - "数据库"
tags: 
  - "mysql"
  - "关联查询"
---

我们在使用MySQL进行查询时, 我们希望把同类结果合并为一行(1个字段内). 本篇文章就来记录下如何使用MySQL将多条记录/结果合并为一行.

## 效果

有图有真相, 先来看下查询的最终效果对比:

<figure>

![](images/MySQL多条记录结果合并-01.png)

<figcaption>

合并前

</figcaption>

</figure>

![](images/MySQL多条记录结果合并-03.png)

<figure>

![](images/MySQL多条记录结果合并-02.png)

<figcaption>

合并后

</figcaption>

</figure>

## 实战开始

### 创建表及填充数据

先来创建一个表. 在库中运行以下SQL命令:

    ``DROP TABLE IF EXISTS `t_name`; CREATE TABLE `t_name`  (   `name` varchar(255) NOT NULL,   PRIMARY KEY (`name`) ) ; INSERT INTO `t_name` VALUES ('阿航'),('张三'),('李四'),('王五'),('傻根');``

至此, 我们有了一个`t_name`表了. 这个表用于存储名字.

### 查询所有人的名字

通常, 我们查询所有人的名字会使用以下SQL:

    `SELECT name 名字 FROM t_name;`

查看结果:

    `mysql> SELECT name 名字 FROM t_name; +------+ | 名字 | +------+ | 傻根 | | 张三 | | 李四 | | 王五 | | 阿航 | +------+ 5 rows in set (0.10 sec)`

可见, 有几条数据就会出现几行. 我们的目标就是合并它们为一行.

### 使用GROUP\_CONCAT合并多条记录

重点来了, 我们这回要用到`GROUP_CONCAT`函数了. 顾名思义, 这两个单词直译过来就是"分组合并".

输入我们改版后的SQL:

    `SELECT GROUP_CONCAT(name SEPARATOR ',') 名字 FROM t_name;`

> 其中, `SEPARATOR`关键字后面跟的值决定了分组后, 使用什么作为分隔符. 上述例子使用了逗号(`,`).
> 
> 💡 代码解析

🟢 运行, 查看结果:

    `mysql> SELECT GROUP_CONCAT(name SEPARATOR ',') 名字 FROM t_name; +------------------------+ | 名字                   | +------------------------+ | 傻根,张三,李四,王五,阿航| +------------------------+ 1 row in set (0.07 sec)`

搞定.

\[epcl\_box type="success"\]至此, 我们成功的将结果集合并为一行了.\[/epcl\_box\]

### 进阶: 合并为JSON

我们确实把多个结果合并成一行了. 但是还不够, 我还想把它变成JSON.

#### 配合CONCAT函数使用

不说废话, 直接上代码:

    ``SELECT 	CONCAT('[', GROUP_CONCAT( CONCAT('"', `name`, '"') SEPARATOR ','), ']') 名字  FROM 	t_name;``

> 虽然看起来比较复杂, 但是仍然有迹可循.
> 
> 我们从内向外看, 最里面, 我们使用了`CONCAT`函数将`name`字段拼接上两个`"`引号.
> 
> 之后我们使用GROUP\_CONCAT分组合并函数将带引号的name合并为一行, 并且用逗号分隔.
> 
> 最后, 我们在最外层拼接上我们的`[`与`]`, 包住我们的结果. 这样就成功变成了JSON格式的字符串.
> 
> 💡 代码解析

🟢 运行, 查询结果:

    ``mysql> SELECT CONCAT('[',GROUP_CONCAT(CONCAT('"',`name`,'"') SEPARATOR ','),']') 名字 FROM t_name; +-------------------------------------+ | 名字                                | +-------------------------------------+ | ["傻根","张三","李四","王五","阿航"]  | +-------------------------------------+ 1 row in set (0.07 sec)``

\[epcl\_box type="success"\]是不是很简单? 快去使用吧!\[/epcl\_box\]
