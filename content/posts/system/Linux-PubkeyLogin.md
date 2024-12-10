---
title: "Linux PubkeyLogin"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T10:56:13+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"
---
<!--more-->


# 配置密钥登录

## 新建用户

1.`adduser 用户` or `useradd 用户` > 新建用户
> (`adduser` 为 `useradd`软连接)

2.`passwd 用户` > 设置密码

3.`usermod -aG wheel 用户` > 切换用户组
>（普通用户无sudo权限）

## 设置密钥

``` base
ssh-keygen
#建立密钥对

cd .ssh
cat id_rsa.pub >> authorized_keys
#安装公钥

chmod 600 authorized_keys
chmod 700 ~/.ssh
更改文件权限

下载私钥，登录使用
```

## 配置SSH登录

```base
vi /etc/ssh/sshd_config
```

```conf
#配置文件
PasswordAuthentication no 
#不启用密码认证
PermitRootLogin no 
#禁止Root登录 
       
#允许密钥认证
RSAAuthentication yes
#centos7.4以上弃用这个第一代RSA

PubkeyAuthentication yes
# 公匙认证
```

重启SSH服务`systemctl restart sshd`

## 参考地址

+ [初始参考地址](https://www.jb51.net/article/170446.htm)  
+ [设置密钥](http://coolnull.com/3486.html)