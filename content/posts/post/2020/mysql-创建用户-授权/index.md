---
title: "MySQL 创建用户 & 授权"
date: "2020-05-11"
categories: 
  - "mysql"
  - "数据库"
tags: 
  - "mysql"
coverImage: "banner-3.png"
---

MySQL 等主流 数据库 的最高权限一般是root用户. 有时我们需要提供数据库的账号和密码以使用某些服务. 但实际上每个服务只会使用1个左右的数据库. 直接将root账号和密码随意分配是一件很危险的事情. 所以我们需要单独的 创建用户, 并 授权 需要的数据库给它.

## 用户管理

### 创建用户

创建用户harrison, 并指定IP为192.118.1.1; 设置密码为123

```
CREATE USER 'harrison' @'192.118.1.1' IDENTIFIED BY '123';
```

创建用户harrison, 任意IP即可登录; 设置密码为123

```
CREATE USER 'harrison' @'%' IDENTIFIED BY '123';
```

### 删除用户

删除用户名为harrison, 且IP为192.118.1.1的用户

```
DROP USER 'harrison' @'192.118.1.1';
```

### 修改用户名及IP

修改用户名为harrison, 不限制登录IP的用户 -> 用户名harry, 限制登录IP为192.168.1.1

```
RENAME USER 'harrison' @'%' TO 'harry' @'192.168.1.1';
```

### 修改用户密码

修改用户名为harrison, 不限制登录IP的用户的密码为456

```
SET PASSWORD FOR 'harrison' @'%' = PASSWORD ( '456' );
```

## 用户授权

### 查看用户拥有权限

查看用户harrison拥有的权限:

```
SHOW GRANTS FOR 'harrison' @'%';
```

### 赋予权限

为harrison提供db1数据库的table1表SELECT(查询)、INSERT(新增)、UPDATE(修改)权限

```
GRANT 
    SELECT,
    INSERT,
    UPDATE ON db1.table1 TO "harrison" @'%';
```

为harrison提供db1数据库的全部增删改查权限

```
GRANT ALL PRIVILEGES ON db1.* TO "harrison" @'%';
```

### 撤回权限

撤回harrison对db1数据库的table1表的全部权限

```
REVOKE ALL ON db1.table1 
FROM
    'harrison' @"%";
```

撤回harrison对db1数据库的全部权限

```
REVOKE ALL ON db1.* 
FROM
    'harrison' @"%";
```

## 感谢

- [MySQL官方网站](https://www.mysql.com/)
- [MySQL创建用户和授权](https://www.cnblogs.com/wangyueping/p/11258028.html)
- [Pexels](https://www.pexels.com/zh-cn/photo/830854/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) 上的 [Manuel Geissinger](https://www.pexels.com/zh-cn/@artunchained?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) 拍摄的照片
- (排名不分先后)

## 结语

若你对本篇文章有任何问题, 欢迎在下方评论区讨论, 或加入[阿航的技术小站交流群](https://jq.qq.com/?_wv=1027&k=egT9rjgu)
