---
title: "CentOS 7 安装 PHP 7.2"
date: "2020-04-30"
categories: 
  - "linux"
  - "linux踩坑"
tags: 
  - "centos"
  - "php"
coverImage: "banner-3.png"
---

CentOS 7 自带的PHP版本比较低, 所以本篇来为大家记录CentOS 7 安装 PHP 7.2 的过程

## 查看当前安装的PHP版本

```
php -v
```

如果不是你想要的版本, 请继续向下看.

## 完全清除旧PHP

输入下面的命令, 来查看已安装的PHP相关包:

```
rpm -qa|grep php
```

正常情况下, 会看到若干行.

使用传统的`yum remove php`无法清理干净, 所以为了节省时间我们有两种方式:

### 方法一: 优雅删除

因为PHP直接有着相互依赖的关系, 在使用`rpm -e XXXX`时会提醒你依赖的包, 这时我们先要删除依赖.

当然, 这么做比较浪费时间, 但也是最安全的做法.

### 方法二: 强制批量删除

使用`rpm -e XXXX --nodeps`进行强制删除, 比如:

```
rpm -e php-symfony-http-foundation-2.8.12-2.el7.noarch  --nodeps; \
rpm -e php-symfony-http-foundation-2.8.12-2.el7.noarch  --nodeps; \
rpm -e php-composer-spdx-licenses-1.5.3-1.el7.noarch  --nodeps; 
```

> 这个例子就会强制删除这三个包, 方便快捷.

## 检测是否清理干净

先来看看有没有相关的包:

```
rpm -qa|grep php
```

如果没有返回, 那么视为成功;

再来看看PHP是否消失:

```
php -v
```

同样的, 如果没有返回, 那么视为成功.

## 安装PHP7.2

输入以下命令进行安装:

如果下面的yum安装过慢, 可以查看这篇文章进行加速: [《yum下载太慢? 使用国内源加速!》](https://blog.bugcatt.com/archives/981)

```
yum -y install php72w php72w-cli php72w-fpm php72w-common php72w-devel
```

> 以上的命令包含常用的PHP库, 你需要按需额外导入~

## 启动服务

首先允许服务:

```
systemctl enable php-fpm.service
```

启动服务:

```
systemctl start php-fpm.service
```

## 大功告成

输入以下命令, 检查是否成功吧!

```
php -v
```

## 感谢

- Linux公社的文章[《CentOS 7下Yum安装PHP7.2步骤》](https://www.linuxidc.com/Linux/2019-07/159197.htm).
- [Pexels](https://www.pexels.com/zh-cn/photo/366791/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) 上的 [David Bartus](https://www.pexels.com/zh-cn/@david-bartus-43782?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) 拍摄的照片

(排名不分先后)
