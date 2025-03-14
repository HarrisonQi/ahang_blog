---
title: "Linux 出现 too many open files 的处理办法"
date: "2021-06-22"
categories: 
  - "linux"
  - "linux踩坑"
tags: 
  - "centos"
  - "hexo"
  - "linux"
---

今天在使用Hexo generate时出现了`oo many open files`这个问题, 在此记录下过程以及解决方案.

## 环境

CentOS

## 排查步骤

使用此命令获取当前系统打开文件数量:

```bash
lsof | wc -l
```

使用此命令获取打开文件数量上限:

```bash
ulimit -a
```

会返回类似:

```plaintext
ulimit -a
core file size          (blocks, -c) 0
data seg size           (kbytes, -d) unlimited
scheduling priority             (-e) 0
file size               (blocks, -f) unlimited
pending signals                 (-i) 7268
max locked memory       (kbytes, -l) 64
max memory size         (kbytes, -m) unlimited
open files                      (-n) 1024
pipe size            (512 bytes, -p) 8
POSIX message queues     (bytes, -q) 819200
real-time priority              (-r) 0
stack size              (kbytes, -s) 8192
cpu time               (seconds, -t) unlimited
max user processes              (-u) 7268
virtual memory          (kbytes, -v) unlimited
file locks                      (-x) unlimited
```

其中, `open files`的值就为上限. 上方的例子为 1024.

## 解决方案

### 方案一: 优化你的服务

最优方案其实是使你的服务妥善处理文件. 如果无法优化, 请参考方案二.

### 方案二: 提高 open files 数量上限

#### 临时修改

使用该命令临时修改, 立即生效, 重启后失效:

```bash
ulimit -n 2048
```

你可以按需调整数量, 比如 `ulimit -n 65535`
