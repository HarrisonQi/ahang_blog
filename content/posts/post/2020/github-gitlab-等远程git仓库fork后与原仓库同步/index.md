---
title: "Github/Gitlab 等远程Git仓库fork后与原仓库同步"
date: "2020-06-04"
categories: 
  - "git"
  - "github"
tags: 
  - "fork"
  - "git"
  - "github"
  - "pr"
  - "开源"
coverImage: "GithubGitlab-等远程Git仓库fork后与原仓库同步-banner_Jc.jpg"
---

看到这篇文章, 说明你也是个勤奋的贡献者🤝🤝. 同学们在贡献代码 PR 前, 都需要将原仓库`fork`下来. 但有时原仓库的代码比我们fork后的代码新, 并且github目前似乎并未提供自动fork的机制. 本篇文章就来记录下Github/Gitlab 等远程Git仓库fork后与原仓库同步的方法.

## 适用场景

github等远程仓库的原仓库代码有大量变更, 需要将自己fork下来的仓库和原仓库同步.

## 需具备的条件

本篇教程假定:

- 你已经掌握基础的CMD/Bash/Shell终端命令.
- 你已经掌握了基本的Git命令以及Github操作.
- 你已经有了待同步的、fork下来的代码仓库.

\[epcl\_box type="notice"\]本篇教程将会尽可能减少废话, 只放干货. 所以请你仔细阅读并严谨遵循教程步骤!\[/epcl\_box\]

## 解决方案

### 查看当前远程仓库配置

打开终端, `cd`至仓库目录内.

输入以下命令以查看当前的远程仓库:

```
git remote -v
```

正常情况下, 会返回类似于:

```
git remote -v
origin  https://github.com/你的用户名/你的仓库名.git (fetch)
origin  https://github.com/你的用户名/你的仓库名.git (push)
```

\[epcl\_box type="notice"\]如果你未返回数据, 请检查你的本地仓库是否关联了远程仓库. 若格式和上面不一致, 请检查你的仓库状态.\[/epcl\_box\]

### 绑定上游远程仓库

紧接着输入以下命令行, 绑定上游仓库:

```
git remote add upstream "https://github.com/上游用户名/上游仓库名.git"
```

再次查看当前仓库:

```
git remote -v
```

正常情况下, 会返回类似于:

```
git remote -v
origin  https://github.com/你的用户名/你的仓库名.git (fetch)
origin  https://github.com/你的用户名/你的仓库名.git (push)
upstream        https://github.com/上游用户名/上游仓库名.git (fetch)
upstream        https://github.com/上游用户名/上游仓库名.git (push)
```

### 拉取上游仓库代码

输入以下命令, 拉取上游仓库代码:

```
git pull upstream master
```

\[epcl\_box type="success"\]至此, 你的本地仓库已经与原仓库同步完成啦!\[/epcl\_box\]

### 收尾工作

此后, 你可以通过正常的提交推送, 使自己的fork仓库变为最新的代码. 完成后, 又可以愉快的进行PR了!
