---
title: "一步解决 Failed to connect to raw.githubusercontent.com port 443: Connection refused"
date: "2020-08-09"
categories: 
  - "mac"
  - "windows"
tags: 
  - "dns"
  - "github"
  - "macos"
---

今天在尝试安装`Homebrew`时碰到这个问题，本篇文章就来记录下如何一步解决 Failed to connect to raw.githubusercontent.com port 443: Connection refused。

## 解决方案

### 方案一：修改DNS

修改你的电脑DNS为Google的`8.8.8.8`。

👉 [点击这里](https://www.bugcatt.com/archives/2486)查看Mac修改DNS教程

### 方案二：修改代理（需科学上网）

此方法仅限于已经可以科学上网的同学。

在终端中输入以下命令行（`7890` 和 `789` 需要换成你自己的端口）：

    `export https_proxy=http://127.0.0.1:7890 http_proxy=http://127.0.0.1:7890 all_proxy=socks5://127.0.0.1:789`

再次尝试连接，应该可以了！

> 此方法有一个小小的缺陷，那就是运行完上面的命令行会导致终端的命令都处于外网状态。当然，解决方案就是**终止当前Session会话**或者**直接关闭终端窗口**。
> 
> **小缺点**及解决方案

## 感谢

[Failed to connect to raw.githubusercontent.com:443](https://zhuanlan.zhihu.com/p/115450863)
