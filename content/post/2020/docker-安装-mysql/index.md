---
title: "Docker 安装 MySQL"
date: "2020-04-13"
categories: 
  - "docker"
  - "运维"
tags: 
  - "docker"
  - "mysql"
  - "容器"
coverImage: "2020-04-17_163315-1-e1587112972240.png"
---

本文为 docker 安装 mysql 容器的完整详细教程.

> 若图片展示异常, 请访问我的[官方博客](/post/2020/docker-安装-mysql/)

## 准备工作

### 开发环境

本博客的环境一览:

| 环境 | 版本号 |
| --- | --- |
| docker | 1.13.1 |

> 注意您的环境和文中的差异, 避免出现不兼容的情况哦!

### 需具备的条件

要顺利阅读本文, 假定您已经掌握了以下知识:

1. docker环境已正常安装
2. 掌握基本的终端命令

## 实战开始

### 查询所有的mysql镜像

```
docker search mysql
```

### 选择并拉取你想要的镜像(这里拿官方的mysql8进行举例)

```
docker pull mysql:8.0
```

### 查询已下载的MySQL镜像

```
docker images |grep mysql
```

### 使用镜像创建容器

```
docker run -p 3306:3306 --name mymysql -v $PWD/conf:/etc/mysql/conf.d -v $PWD/logs:/logs -v $PWD/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 -d mysql:8.0
```

解析:

- **`-p 3306:3306`**：将容器的 3306 端口映射到主机的 3306 端口。
- **`-v $PWD/conf:/etc/mysql/conf.d`**：将主机当前目录下的 `conf/my.cnf` 挂载到容器的`/etc/mysql/my.cnf`。
- **`-v $PWD/logs:/logs`**：将主机当前目录下的 logs 目录挂载到容器的 `/logs`。
- **`-v $PWD/data:/var/lib/mysql`**：将主机当前目录下的`data`目录挂载到容器的 `/var/lib/mysql`
- **`-e MYSQL_ROOT_PASSWORD=123456`：**初始化 root 用户的密码。

### 查看容器运行情况

```
docker ps
```

### 优雅关闭

```
docker stop [容器id]
```

### 启动已停止的容器

```
docker start [容器id]
```

### 重启容器

```
docker restart [容器id]
```

## 大功告成

通过以上的一些步骤, 我们完成了Dokcer安装Mysql的目标, 是不是很简单?

对文章若有任何问题、异议以及改进建议, 欢迎在下方进行评论. 作者将尽快回复! 获取最新文章, 欢迎阅读[官方博客](/post/2020/docker-安装-mysql/).

更多更好的教程/博客/资讯, 欢迎访问我的官网: [阿航的技术小站](/)
