---
title: "yum下载太慢? 使用国内源加速!"
date: "2020-04-30"
categories: 
  - "linux"
  - "linux优化"
tags: 
  - "centos"
  - "linux"
  - "yum"
  - "国内加速"
coverImage: "banner-2.png"
---

## 引言

使用 yum 下载, 看到 Linux 控制台的2Kb/s是不是心态都崩了? 国内大墙在保护我们的同时, 也把我们程序员给害惨了...来看看如何加速吧

## 备份源

万一源失效了呢, 有备无患:

```
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
```

## 选择镜像

### 使用阿里云镜像

#### CentOS 5

```
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-5.repo
```

#### CentOS 6

```
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-6.repo
```

#### CentOS 7

```
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
```

### 使用网易镜像

#### CentOS 5

```
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.163.com/.help/CentOS5-Base-163.repo
```

#### CentOS 6

```
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.163.com/.help/CentOS6-Base-163.repo
```

#### CentOS 7

```
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.163.com/.help/CentOS7-Base-163.repo
```

## 清理并构建缓存

首先运行:

```
yum clean all
```

完成后运行:

```
yum makecache
```

## 大功告成!

享受飞快的速度吧!

## 感谢

- [](https://www.cnblogs.com/imweihao/p/7357484.html)[《国内yum源的安装(163，阿里云，epel)](https://www.cnblogs.com/imweihao/p/7357484.html)》- [imweihao](https://home.cnblogs.com/u/imweihao/)

- [Wallhaven](https://wallhaven.cc/)上[Yahren的图片](https://wallhaven.cc/w/95xy88)
