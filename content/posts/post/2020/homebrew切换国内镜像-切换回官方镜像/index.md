---
title: "Homebrew切换国内镜像/切换回官方镜像"
date: "2020-08-17"
categories: 
  - "mac"
tags: 
  - "homebrew"
  - "macos"
  - "环境部署"
---

身在大陆，如果不使用国内镜像，每次下载软件都会怀疑人生。本篇文章就来记录下Homebrew如何切换国内镜像/切换回官方镜像。

## 先决条件

本篇文章环境：

| 环境 | 版本 |
| --- | --- |
| MacOS | Catalina 10.15.5 |
| Homebrew | 2.4.9 |

- 掌握Bash命令
- 已经完整安装Homebrew

## 实战开始

切换Homebrew源非常简单，只要输入几个命令就可以轻松搞定。

> 注意：如果你的MacOS系统的默认终端不是zsh，请把文中出现的所有`.zshrc`替换为你的终端的环境变量文件名！

### 切换至中科大国内镜像

#### 1\. 替换brew.git

在终端中依次输入以下命令：

    `cd "$(brew --repo)"`

    `git remote set-url origin 'https://mirrors.ustc.edu.cn/brew.git'`

#### 2\. 替换homebrew-core.git

在终端中依次输入以下命令：

    `cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"`

    `git remote set-url origin 'https://mirrors.ustc.edu.cn/homebrew-core.git'`

#### 3\. 替换homebrew-cask.git

在终端中依次输入以下命令：

    `cd "$(brew --repo)/Library/Taps/homebrew/homebrew-cask"`

    `git remote set-url origin 'https://mirrors.ustc.edu.cn/homebrew-cask.git'`

#### 4\. 更新brew，使配置生效

输入以下命令：

    `brew update`

耐心等待命令行执行，直至完成。

\[epcl\_box type="success"\]至此，我们已经成功为brew配置了国内源！享受超高速度吧！\[/epcl\_box\]

### 切换至官方镜像

如果你发现国内镜像出了问题，或者外网“顺畅”了，你就需要切换至官方镜像咯。

#### 1\. 替换brew.git

    `cd "$(brew --repo)"`

    `git remote set-url origin 'https://github.com/Homebrew/brew.git'`

#### 2\. 替换homebrew-core.git

    `cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"`

    `git remote set-url origin 'https://github.com/Homebrew/homebrew-core.git'`

#### 3\. 替换homebrew-cask.git

    `cd "$(brew --repo)/Library/Taps/homebrew/homebrew-cask"`

    `git remote set-url origin 'https://github.com/Homebrew/homebrew-cask.git'`

#### 4\. 更新brew，使配置生效

    `brew update`

别急，还没完成，就剩两步了！

#### 5\. 移除此前的环境变量

编辑`.zshrc`环境变量文件

    `vim  ~/.zshrc`

如果文件中有这一行，就删除它：

    `export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles`

#### 6\. 更新环境变量

    `source ~/.zshrc`

## Credit

[https://www.jianshu.com/p/022cd15432dc](https://www.jianshu.com/p/022cd15432dc)
