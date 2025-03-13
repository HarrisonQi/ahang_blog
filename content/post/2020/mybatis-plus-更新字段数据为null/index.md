---
title: "Mybatis-Plus 更新字段数据为null"
date: "2020-07-20"
categories: 
  - "java"
  - "mybatis-plus"
tags: 
  - "mybatis-plus"
  - "null"
  - "字段"
  - "数据库"
---

在使用Mybatis-Plus开发项目时, 需要将数据库某字段值设置为null. 但是仅将实体类的值赋值为null是不够的. 还需要为实体类的属性添加以下注解:

    `@TableField(fill = FieldFill.UPDATE)`

比如你需要设置某表的字段name为null, 则需要进入实体类, 在对应的属性上添加注解:

    `@TableField(fill = FieldFill.UPDATE) private String name;`
