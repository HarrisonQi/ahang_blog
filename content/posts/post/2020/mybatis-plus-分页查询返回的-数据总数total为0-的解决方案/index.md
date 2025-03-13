---
title: "MyBatis Plus 分页查询返回的 数据总数total为0 的解决方案"
date: "2020-05-15"
categories: 
  - "java"
  - "mybatis-plus"
tags: 
  - "java"
  - "mybatis-plus"
  - "后端"
coverImage: "MyBatis-Plus-分页查询返回的-数据总数total为0-的解决方案-banner.jpg"
---

今天在使用MyBatis-Plus在进行分页查询时, 返回的`IPage`对象数据的`total`属性一直是`0`. 没有数据总数, 前端的分页部分将会比较难搞, 在此记录一下排坑过程.

## 开发环境

本教程的开发环境如下:

| 名称 | 版本 |
| --- | --- |
| JDK | 1.8 |
| Spring Boot | 2.1.14.RELEASE |
| Mybatis-Plus | 3.2.0 |

## 解决方案

### 方案一: 添加配置类, 注入`PaginationInterceptor`(推荐)

创建类文件`MybatisPlusConfig`文件, 输入以下代码:

\[epcl\_tabs\] \[epcl\_tab title="Kotlin"\]

```

import com.baomidou.mybatisplus.extension.plugins.PaginationInterceptor
import org.springframework.context.annotation.Bean
import org.springframework.context.annotation.Configuration

@Configuration
class MybatisPlusConfig {
    /**
     * 分页插件
     */
    @Bean
    fun paginationInterceptor(): PaginationInterceptor {
        return PaginationInterceptor()
    }
}
```

\[/epcl\_tab\] \[epcl\_tab title="Java"\]

```

import com.baomidou.mybatisplus.extension.plugins.PaginationInterceptor;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class MybatisPlusConfig {
    /**
     * 分页插件
     */
    @Bean
    public PaginationInterceptor paginationInterceptor() {
        return new PaginationInterceptor();
    }
}
```

\[/epcl\_tab\] \[/epcl\_tabs\]

搞定.

### 方案二: 检查分页插件冲突(PageHelper)

**不推荐此方法**, 因为是典型的兼容性问题. 为了解决问题而删除另一个东西, 是相当不明智的做法. 当然, 不影响你的项目除外.

检查导入的依赖, 判断是否包含`pagehelper`:  
比如进行全局搜索:

```

pagehelper-spring-boot-starter
```

去掉此依赖即可搞定.

## 感谢

排名不分先后

- [使用Mybatis-Plus进行分页查询,返回的数据中total总是为0的问题?可以参考以下两种解决方案](https://blog.csdn.net/wlh_150568/article/details/89947838)
- [Mybatis Plus分页Page total始终为0](https://blog.csdn.net/a992795427/article/details/87793339)

## 结语

本篇实例使用了两种方式来解决问题. 推荐第一种方式, 简单、 快捷、 可靠.
