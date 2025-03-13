---
title: "解决NVM报错：“nvm is not compatible with the npm config \"prefix\" option...”"
date: "2020-08-15"
categories: 
  - "mac"
tags: 
  - "macos"
  - "node"
  - "npm"
  - "nvm"
---

今天在MacOS上尝试使用NVM切换node版本时出现了如下报错：

    ``nvm is not compatible with the npm config "prefix" option:      currently set to "/usr/local/Cellar/nvm/0.35.3/versions/node/v10.21.0" Run `npm config delete prefix`      or `nvm use --delete-prefix v10.21.0` to unset it.``

本篇文章就来记录下解决方案。

## 先决条件

- 掌握终端命令行基本用法
- 掌握node，npm基本概念

本篇文章的环境：

| 环境 | 版本 |
| --- | --- |
| MacOS | Catalina 10.15.5 |
| nvm | 0.35.3 |
| node | v14.6.0 |
| npm | 6.14.7 |

## 解决方案

解决方案非常简单。只需在终端中依次输入以下命令即可：

    `npm config delete prefix`

    `npm config set prefix $NVM_DIR/versions/node/v6.11.1`

## Credit

[nvm is not compatible with the npm config “prefix” option](https://stackoverflow.com/questions/34718528/nvm-is-not-compatible-with-the-npm-config-prefix-option)
