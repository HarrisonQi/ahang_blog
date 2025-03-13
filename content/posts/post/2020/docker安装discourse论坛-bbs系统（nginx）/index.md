---
title: "Docker安装Discourse论坛/BBS系统（Nginx）"
date: "2020-08-19"
categories: 
  - "docker"
  - "nginx"
tags: 
  - "bbs"
  - "centos"
  - "discourse"
  - "docker"
  - "linux"
  - "nginx"
---

最近要做[Flame中文站](https://flame-cn.com)的论坛模块，考虑到技术人社区的重要性，选用了Discourse论坛系统。安装过程相当坎坷，本篇文章就来记录下Docker安装Discourse论坛/BBS系统的全过程。

## 先决条件

- 你的服务器/主机已经妥善安装Docker
- 你的服务器/主机已经妥善安装Git
- 掌握Git基础
- 掌握Docker基础
- 掌握Bash基础

本篇文章的环境：

| 环境 | 版本 |
| --- | --- |
| 主机 | 阿里云ECS |
| 操作系统 | CentOS 7 |

## 开始

\[epcl\_box type="notice"\]即使有阿航的教程会较少大部分坑，在国内部署Discourse是仍然是较痛苦的一件事情。可以查询的资料微乎其微，如果你不喜欢折腾，请选用其他的论坛框架！\[/epcl\_box\]

### 配置

你的服务器的**必须大于**以下配置，否则你会无限踩坑：

- 双核CPU
- 1 GB 运行内存
- 64位 Linux内核系统
- 已经安装Docker

### 下载Discourse

创建一个目录，用于存放Discourse。比如：

    `mkdir /usr/local/discourse`

获得管理员权限：

    `sudo -s`

克隆discourse(命令后半段的路径和上方创建的保持一致)：

    `git clone 'https://github.com/discourse/discourse_docker.git' /usr/local/discourse`

耐心等待完成。

完成后，进入该目录：

    `cd /usr/local/discourse`

### 修改配置

克隆示例配置文件：

    `cp samples/standalone.yml containers/app.yml`

打开文本编辑器，修改复制后的配置文件：

    `vim containers/app.yml`

#### 配置国内镜像

如果你身在大陆，则需要进行镜像加速。找到配置文件中的`templates`块，添加国内镜像`templates/web.china.template.yml`：

    ` templates:   - "templates/postgres.template.yml"   - "templates/redis.template.yml"   - "templates/sshd.template.yml"   - "templates/web.template.yml"   - "templates/web.china.template.yml"`

#### 其他配置

注销或删除掉expose下面的80和443端口：

    ` expose:   - "80:80"   # http   - "443:443" # https`

这里**列出需要修改的几项**（非完整配置文件）：

    `env:   LANG: en_US.UTF-8    # 设置域名   DISCOURSE_HOSTNAME: 'discourse.example.com'    # 设置管理员邮箱   DISCOURSE_DEVELOPER_EMAILS: 'me@example.com,you@example.com'    # 设置网站邮箱配置   DISCOURSE_SMTP_ADDRESS: smtp.example.com   DISCOURSE_SMTP_PORT: 587   DISCOURSE_SMTP_USER_NAME: user@example.com   DISCOURSE_SMTP_PASSWORD: pa$$word`

如果你使用的是阿里云服务器，还需要在邮箱配置下添加：

    `  # 如果你使用的是阿里云服务器，需要添加以下三行   DISCOURSE_SMTP_AUTHENTICATION: login   DISCOURSE_SMTP_OPENSSL_VERIFY_MODE: none   DISCOURSE_SMTP_ENABLE_START_TLS: true`

此外在配置文件最后的 `run:` 那一块中找到：

    `run:   - exec: echo "Beginning of custom commands"    ## If you want to set the 'From' email address for your first registration, uncomment and change:   #- exec: rails r "SiteSetting.notification_email='info@unconfigured.discourse.org'"   ## After getting the first signup email, re-comment the line. It only needs to run once.` 

删除掉  
`#- exec: rails r "SiteSetting.notification_email='info@unconfigured.discourse.org'"`  
这一行开头的 `#` 井号，再把 `info@unconfigured.discourse.org` 改成你的发件邮箱地址。  
编辑文件的时候不要删除每一行前的空格符，保持语句块上下是对齐的，不要删除没说明的引号。

### 启动Discourse

\[epcl\_box type="error"\]在开始此步骤前，你需要**暂时停止占用`80`端口的服务**（比如Nginx、Apache等）。截止本文撰写前，官方并没有提供自定义启动端口的任何配置。\[/epcl\_box\]

输入命令：

    `./launcher rebuild app`

等待很久很久很久后运行完成。

### Nginx配置

为你的nginx添加配置，你需要将以下模板修改为你自己的：

    `server {     listen 80; listen [::]:80;     server_name forum.example.com;  # <-- change this      return 301 https://$host$request_uri; }  server {     listen 443 ssl http2;  listen [::]:443 ssl http2;     server_name forum.example.com;  # <-- change this      ssl on;     ssl_certificate      /var/discourse/shared/standalone/ssl/ssl.crt;     ssl_certificate_key  /var/discourse/shared/standalone/ssl/ssl.key;     ssl_dhparam          /var/discourse/shared/standalone/ssl/dhparams.pem;     ssl_session_tickets off;     ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-DSS-AES128-GCM-SHA256:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-DSS-AES128-SHA256:DHE-RSA-AES256-SHA256:DHE-DSS-AES256-SHA:DHE-RSA-AES256-SHA:ECDHE-RSA-DES-CBC3-SHA:ECDHE-ECDSA-DES-CBC3-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128-SHA256:AES256-SHA256:AES128-SHA:AES256-SHA:AES:CAMELLIA:DES-CBC3-SHA:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!aECDH:!EDH-DSS-DES-CBC3-SHA:!EDH-RSA-DES-CBC3-SHA:!KRB5-DES-CBC3-SHA;      http2_idle_timeout 5m; # up from 3m default      location / {         proxy_pass http://unix:/var/discourse/shared/standalone/nginx.http.sock:;         proxy_set_header Host $http_host;         proxy_http_version 1.1;         proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;         proxy_set_header X-Forwarded-Proto https;     } }`

## 完成

看起来本篇文章步骤少，实际上耗费了阿航将近一周的零散时间。

## Credit

- [30 分钟内在云上部署 Discourse](https://meta.discoursecn.org/t/topic/26)
- [在大陆地区的云上部署 Discourse](https://meta.discoursecn.org/t/topic/28)
- [记录一下部署Discourse论坛的过程](https://www.orgleaf.com/3098.html)
