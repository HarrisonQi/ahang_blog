---
title: "MySql根据生日计算年龄"
date: "2020-10-24"
categories: 
  - "mysql"
  - "数据库"
tags: 
  - "mysql"
  - "出生日期"
  - "生日"
---

这次的需求是需要通过出生日期（年月日）来计算年龄。一句SQL就可以搞定:

    `SELECT TIMESTAMPDIFF(YEAR, '2000-01-01', CURDATE());`

如果格式是 年-月-日 ，那就使用`CONCAT`拼接起来，这么写：

    `SELECT TIMESTAMPDIFF(YEAR, CONCAT(2000, '-', 1, '-', 1), CURDATE());`

如果你遇到了更好的解法，欢迎在下方留言哟！
