---
title: "Spring Boot 子项目无法找到父项目问题解决"
date: "2022-06-20"
categories: 
  - "collection-box"
---

## 场景

这天在研究SpringBoot父子项目时, 发现子项目无法进行 `Maven Install`.

我的项目结构:

    ```-父项目 ----公共项目 ----项目A ----项目B```

其中, 项目A和项目B要引入公共项目作为依赖

## 解决方案

查看所依赖项目(上文中的'公共项目')的`pom.xml`是否引入了这个plugin:

```xml
<plugin>
    <groupid>org.springframework.boot</groupid>
    <artifactid>spring-boot-maven-plugin</artifactid>
</plugin>
```

删除后即可成功
