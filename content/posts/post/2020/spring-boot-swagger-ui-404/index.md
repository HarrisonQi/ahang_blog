---
title: "Spring Boot Swagger-UI 404"
date: "2020-08-01"
categories: 
  - "java"
  - "java框架"
tags: 
  - "java"
  - "spring"
  - "springboot"
  - "swagger"
---

这几天换了新的设备用于开发。启动项目后访问swagger地址，发现空空如也。本篇文章就来记录下Spring Boot Swagger-UI 404的可能原因及解决方案。

## 先决条件

- 掌握Java开发
- 掌握SpringBoot框架
- 掌握Swagger框架及相应配置

阿航的项目环境：

| 环境 | 版本 |
| --- | --- |
| JDK | 14 |
| SpringBoot | 2.1.13.RELEASE |
| Swagger | 2.9.2 |

## 问题原因

在网上翻了个遍，众说纷纭。记录下我找到的情况以及对应的解决方案。

### 情况一：检查Swagger是否限制环境

很明显我们在生产环境不太希望将完整的接口文档暴露出来，我们通常会通过`@Profile`进行限制，比如：

    `@EnableSwagger2 @Configuration @Profile("dev") class SwaggerConfig { ...`

上面的`@Profile`的值就是限制了我们仅在哪些环境中展示Swagger。

所以，

**检查你的环境是否在`@Profile`内部。**

### 情况二：绑定静态资源文件

在你的Swagger配置文件中（或任何注入Bean的类中）添加：

    `@Override protected void addResourceHandlers(ResourceHandlerRegistry registry) {     // 解决静态资源无法访问     registry.addResourceHandler("/**")             .addResourceLocations("classpath:/static/");     // 解决swagger无法访问     registry.addResourceHandler("/swagger-ui.html")             .addResourceLocations("classpath:/META-INF/resources/");     // 解决swagger的js文件无法访问     registry.addResourceHandler("/webjars/**")             .addResourceLocations("classpath:/META-INF/resources/webjars/"); }`

此方法存在争议，因为新版本的SpringBoot和Swagger并不需要该配置。
