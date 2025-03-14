---
title: "Spring Boot AOP 获取注解中的值"
date: "2021-05-12"
categories: 
  - "java"
  - "java框架"
tags: 
  - "java"
  - "springboot"
---

## 确定需求

首先来确定一下我们的需求:

我需要做一个功能, 可以通过注解的方式来使某些controller做一些事情(比如权限校验).

## 环境

- java 8
- Spring Boot

## 开始

首先来创建一个注解类`MyAnnotation`:

```java
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
public @interface MyAnnotation {
    /**
     * 注解值(等下要获取并处理该值)
     * @return
     */
    String value() default "";
}
```

还有处理注解的类`MyAnnotaionAspect`:

\[epcl\_box type="notice"\]注意, 需要将下方的@annotation内的值替换为你的注解路径!\[/epcl\_box\]

```java
import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.Around;
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.reflect.MethodSignature;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.stereotype.Component;

import java.lang.reflect.Method;

@Aspect
@Component
public class MyAnnotationAspect {
    protected static final Logger logger = LoggerFactory.getLogger(MyAnnotationAspect.class);

    // TODO 注意这里需要替换为你的注解路径
    @Around("@annotation(com.example.demo.MyAnnotation)")
    public Object doSomething(ProceedingJoinPoint point) throws Throwable {
        MethodSignature signature = (MethodSignature) point.getSignature();
        Method signatureMethod = signature.getMethod();

        MyAnnotation myAnnotation = signatureMethod.getAnnotation(MyAnnotation.class);

        String value = myAnnotation.value();
        
        // 这里就可以打印你的注解值了
        System.out.println(value);

        return point.proceed();
    }
}
```

写一个Controller作为例子:

```java
import com.example.demo.aop2.aop.MyAnnotation;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
public class TestController {
    
    // 这里添加我们定义的注解
    @MyAnnotation(value = "123456")
    @RequestMapping(value = "/hello", method = RequestMethod.POST)
    public @ResponseBody
    String demo() {
        return "hello";
    }
}
```

运行Spring Boot, 尝试调用该接口, 然后看看控制台是否成功打印了你传入的value: `123456`
