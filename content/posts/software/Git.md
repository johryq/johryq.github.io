---
title: "Git"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T10:11:21+08:00
draft: false
keywords: []
description: ""
tags: ['']
categories: ['software']
author: "2332334"

---
<!--more-->

# Git

> [官网](https://git-scm.com/)

## 安装

图形界面(win)

+ gitk(默认)
+ sourceTree
+ TortoiseGit
+ GithubDestop
+ GitKraken
+ Gitup

### 基本配置

设置基本信息

config 参数

+ `--systemc` 系统内所有用户
+ `--global` 当前用户
+ `--local` 当前仓库

```bash
git config --global user.name ""
git config --global user.email ""

# 查看设置信息
git config --global --list
```

## 使用

### 基本步骤

```bash
# 初始化仓库
git init

# 添加该目录所有文件
git add *

# 提交所有更改
git commint -m ""

# 提交历史
git log

# 文件对象类型
git cat-file -t hase

# 最近提交内容信息
git cat-file -p hase

# 获取完整hase
git rev-parse hase
```

## Git上传项目至GitHub

> ***Git***

本地版本控制软件  

***GitHub***

上传服务器的版本控制

>上传步骤如下：

1. 初始化本地仓库

    + 在仓库文件夹打开git bash后使用下方命令  

    ```bash

    git init

    ```

2. 修改配置文件

    + 生成本地ssh密匙  

    ```bash

    ssh-keygen -t rsa -C "你的GitHub注册邮箱"

    ```

    回车后，会在默认文件 id_rsa.pub 上生成 SSH key，位置：C:\Users\用户名.ssh  


    之后系统要求输入密码，直接回车不设密码，重复密码时再次回车，之后显示 SSH key 已经生成成功。

    + 将id_rsa.pub 文件中的key粘贴到GitHub->Account Settings->SSH keys->Add SSH key中

    + 验证配置是否成功

    ```bash

    ssh -T git@github.com

    ```

    + 设置username和email，添加远程地址

    ```bash

    git config --global user.name "your name"

    git config --global user.email "your_email"

    git remote add origin git@github.com:用户名/Git仓库名称.git

    ```

>之后就可以提交代码了

*如果第一次提交报错可以尝试*  

`git push -f origin master`

>这条命令会直接覆盖前面分支，谨慎使用  

## 参考

+ [用 Git 上传项目到 GitHub](https://www.jianshu.com/p/0fce531dba31)
+ [朱双印个人日志-git之旅](https://www.zsythink.net/archives/3506)