---
title: "IDEA Spring Boot彩色日志"
date: "2020-12-17"
categories: 
  - "collection-box"
tags: 
  - "idea"
  - "springboot"
---

这回在开发Spring Boot应用时, 控制台日志突然变成了黑白. 根本没眼看. 本篇文章就来记录下如何使IDEA日志恢复彩色.

## 解决方案

在IDEA启动命令中添加一条:

    `-Dspring.output.ansi.enabled=ALWAYS`

如图:

![](images/image-1.png)

![](images/image-2.png)
