---
title: "Kotlin 使用 TypeReference"
date: "2020-04-30"
categories: 
  - "java-kotlin踩坑"
  - "随手写"
tags: 
  - "java"
  - "kotlin"
  - "支付宝"
---

后端的语言使用的是Kotlin, 在写支付宝小程序获取手机号并解密时参照官方Java文档, Java自动转Kotlin出现异常. 在此进行记录.

这一段的`Java`代码块:

```
Map openapiResult = JSON.parseObject(response,
            new TypeReference>() {
            }, Feature.OrderedField);
```

## 解决方案

转为`kotlin`的正确写法:

```
val typeRef = object : TypeReference>() {}
val openApiResult = JSON.parseObject(response, typeRef, Feature.OrderedField)        
```
