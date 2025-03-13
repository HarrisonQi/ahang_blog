---
title: "Mybatis-Plus 查询获取数据集最大值(Max())"
date: "2020-07-24"
categories: 
  - "java"
  - "mybatis-plus"
tags: 
  - "mybatis"
  - "mybatis-plus"
  - "mysql"
  - "spring"
  - "springboot"
  - "sql"
---

在使用Mybatis-Plus框架进行查询时, 碰到了需要查询最大值的情况. 但是截止本文章撰写前, Mybatis-Plus并没有提供直接的查询数据最大值的函数. 本篇文章就来记录下如何实现.

## 前置条件

- 掌握Spring框架
- 掌握Mybatis
- 掌握Mybatis-Plus的基本使用
- 掌握SQL语句

## 实战开始

我们进行普通查询的时候, 需要用到以下语句:

    `xxxMapper.selectOne(QueryWrapper(...));`

我们只需要分别添加排序(`orderByDesc`)和取第1个(`limit 1`)就可拿到最大值:

    `xxxMapper.selectOne(QueryWrapper(...).orderByDesc("排序字段名").last("limit 1"));`

拿到最小值只需改为正序排列:

    `xxxMapper.selectOne(QueryWrapper(...).orderByAsc("排序字段名").last("limit 1"));`

搞定.

## 结语

本文的方法虽然实现了我们的目标. 但是**仅为代码美观**. 实际上这样的查询效率可能不高. 生产环境的项目慎用.
