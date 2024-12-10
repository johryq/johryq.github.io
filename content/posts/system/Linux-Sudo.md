---
title: "Linux Sudo"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T11:07:45+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"

---
<!--more-->

# sudo

使普通用户执行命令拥有root权限

## Linux user add sudo authority

### 方法一:修改 `sudoers`

1.未安装 `sudo` 需要登录 root 执行:

```bash
apt install sudo #ubuntu
yum install sudo #centos
```

2.设置( root 下)

```bash
vi /etc/sudoers
```

3.添加如下内容到配置文件

```bash
用户名 ALL=(ALL) ALL
用户名 ALL=(ALL) NOPASSWD: ALL  #执行sudo时不用输入密码

# or 
sudo usermod -aG sudo [name-of-user]
```

最后强制写入退出

### 方法二:`usermod`添加进sudo 组

```bash
usermod -aG sudo 用户名
```

## sudo相关命令

```bash
# 版本及相关信息
sudo -V

# 当前用不sudo权限
sudo -l
```
