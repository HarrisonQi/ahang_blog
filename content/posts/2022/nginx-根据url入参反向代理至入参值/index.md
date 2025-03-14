---
title: "Nginx 根据URL入参反向代理至入参值"
date: "2022-03-15"
categories: 
  - "collection-box"
---

## 场景

小程序需要下载某平台的资源. 但是白名单域名机制会拦截.

## 解决方案

在nginx中添加配置:

```nginx
resolver 8.8.8.8;

location ~/video {
    if ($query_string ~* ^(.*)url=(.*)$) {
        set $mediaUrl $2;
        proxy_pass $mediaUrl;
    }
}
```
