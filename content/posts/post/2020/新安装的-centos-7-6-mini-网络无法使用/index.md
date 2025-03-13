---
title: "新安装的 Centos 7.6 mini 网络无法使用"
date: "2020-04-27"
categories: 
  - "linux踩坑"
  - "随手写"
tags: 
  - "centos"
  - "linux"
---

阿航在给公司部署本地服务器的时候碰到了这个问题, 新安装的 Centos 7.6 mini 网络无法使用. 所以在此记录踩坑历程.

## 解决方案

### 方法一: 选择完整安装(推荐)

这个年代, 硬件设备的价格并不高. 所以服务器的配置不会太低. 所以尽量安装完整版. 选择最小安装会遇到源源不断的坑, 浪费生命😑😑

如果条件不允许, 请看方法二↓.

### 方法二: 配置网络

1\. 找到 /etc/sysconfig/network-scripts

```
cd /etc/sysconfig/network-scripts
```

2\. 编辑ifcfg-enXXX

```
vi ifcfg-enp1s0
```

3\. 按 i 进入编辑模式, 修改:

```
ONBOOT=yes
```

4\. 按ESC键, 输入`:wq`保存

5\. 重启网络服务

## 参考资料

- [CentOS官网](https://www.centos.org/)
