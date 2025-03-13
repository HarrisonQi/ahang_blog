---
title: "org.apache.ibatis.binding.BindingException: Invalid bound statement (not found)"
date: "2020-07-30"
categories: 
  - "java"
  - "java框架"
tags: 
  - "java"
  - "kotlin"
  - "mybatis"
  - "mybatis-plus"
  - "spring"
  - "springboot"
---

在使用Mybatis进行开发时， 出现了这样的报错：

    `org.apache.ibatis.binding.BindingException:      Invalid bound statement (not found)`

本篇文章就来记录下碰到上述问题的几种解决方案。

## 情况

比如我们有Mapper文件`UserMapper.java`及其对应的`UserMapper.xml`文件

这里列举出一些可能出现的情况以及对应的解决方案：

### 情况一：Mapper.xml的namespace有误

找到你的`mapper.xml`文件，找到类似这一行：

    `<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd"> <mapper namespace="com.bugcatt.mapper.UserMapper">  </mapper>`

仔细检查`namespace`的值是否对应正确的路径。

### 情况二：Mapper的函数未在Mapper.xml定义

检查你的UserMapper中的函数/方法，是否已在`Mapper.xml`中定义或名称有误。如果未定义 或者函数名不同请订正。

### 情况三：查询返回值类型未妥善处理

比如你在`UserMapper`中定义了函数的返回值是`List<User>`类型，但是你在`UserMapper.xml`中未正确配置`ResultMap`或`ResultType`。

### 情况三：mapper.xml路径配置

在你的spring-boot配置文件中查看你的xml配置：

    ` mybatis:   # 配置mapper.xml文件路径   mapper-locations: 'classpath*:/**/mapper/**Mapper.xml'   # 配置映射类包名   type-aliases-package: com.bugcatt.domain`

如果你使用的是`Mybatis-Plus`，配置为：

    ` mybatis-plus:   # 配置mapper.xml文件路径   mapper-locations: 'classpath*:/**/mapper/**Mapper.xml'   # 配置映射类包名   type-aliases-package: com.bugcatt.domain`

### 情况四：Mapper.java文件和Mapper.xml文件不同名

比如你的文件分别为`UserMapper.java`和`UserrrMapper.xml`（不同名）将它们的名称改为一致试试看。

此方法存在争议。部分同学不同名也可以运行。

### 情况五：maven未将mapper.xml打进包内

这种情况可能出现在你未将`mapper.xml`放进传统的资源目录中，导致maven编译打包时忽略了你的mapper.xml文件。解决此问题需要在maven配置文件`pom.xml`中添加：

    `<build>           <resources>                   <resource>                            <directory>src/main/java</directory>                            <includes>                                    <include>**/*.xml</include>                         </includes>         </resource>     </resources> </build>`
