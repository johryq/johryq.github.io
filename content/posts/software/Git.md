---
title: "Git"
date: 2021-11-08T19:58:55+08:00
lastmod: 2025-10-12T15:32:21+08:00
draft: false
keywords: []
description: ""
tags: ['git']
categories: ['software']
author: "2332334"

---
<!--more-->

# Git

分布式版本管理

> [官网](https://git-scm.com/)

## 一.安装及基本使用

git图像客户端

+ gitk(默认)
+ sourceTree
+ TortoiseGit
+ GithubDestop
+ GitKraken
+ Gitup

```bash
brew install git

apt install git 

dnf install git
```

### 二.基本配置

设置基本信息，config 参数

+ `--systemc` 系统内所有用户
+ `--global` 当前用户
+ `--local` 当前仓库

```bash
git config --global user.name ""
git config --global user.email ""

# 查看信息
git config --global --list

# 远程仓库详细信息
git remote -v
```

### 二.1 基本使用

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

### 二.2 Git上传项目至GitHub

>上传步骤如下：

1. 初始化本地仓库
    ```bash
    git init
    ```

2. 修改配置文件
   + 生成本地ssh密匙  
   ```bash
   # ssh-keygen -t rsa -b 4096
   ssh-keygen -t ed25519 -C "你的GitHub注册邮箱"
   ```
    > windows位置：C:\Users\用户名\.ssh
    > linux: ~/.ssh
3. 将id_rsa.pub 文件中的key粘贴到GitHub->Account Settings->SSH keys->Add SSH key中

    4. 验证配置是否成功
    ```bash
    ssh -T git@github.com
    ```
1. 设置username和email，添加远程地址
    ``` bash
    git brach oragin main

    # 当需要上传时，上传到具体创建的仓库
    git remote add origin git@github.com:用户名/Git仓库名称.git
    ```

>之后就可以提交代码了

*如果第一次提交报错可以尝试*  

`git push -f origin master`

>这条命令会直接覆盖前面分支，谨慎使用  

## 三. 使用

git所有提交的记录都会生成一条 `sha1` 计算的值作为key，用该值来查询更多数据或者回退等操作

```bash
git log --pretty=oneline

# 分支合并视图
git log --graph

git reflog
```
> 回退版本后使用 `git reflog` 才能查询回退后提交的版本记录

### 三.1 回退

``` bash
# 回退到上一版本
git reset --hard HEAD^
# 回退到10个版本前
git reset --hard HEAD~10

# 修改后未提交，回退到上一次添加暂存库版本 `add` 的版本
git checkout -- file_name
git restore -- file_name
```

+ --soft 会回退到上个版本的未提交状态
+ --soft 会回退到上个版本的未提交状态
+ --mixed 会回退到上个版本已添加但未提交的状态

> `HEAD` 代表当前版本,若要去某次提交记录 `git reset --hard hase`

### 三.2 分支

```bash
# 创建并切换分支
git checkout -b dev

git branch dev
git checkout dev

# 查看分支
git branch

# 删除分支
git branch -d dev

# 切换分支
git switch dev
git checkout dev
```

#### 合并分支

```bash
# 合并分支到当前分支
git merge dev

# 取消合并
git merge --abort

# 将某次提交合并到当前分支
git cherry-pick hase
```

#### rebase 变基

```bash
# 将本地git历史整理成一条线
git rebase

git rebase --abort
```

### 三.3 储藏

将现有已修改未提交的内容暂时贮存，此时可修改其他内容，修改提交完再复原贮存的内容

```bash
# 贮存
git stash

# 查看
git stash list

# 恢复但不删除贮存
git stash apply
# 删除贮存
git stash drop

# 恢复并删除
git stash pop

# 恢复指定贮存
git stash apply stash@{0}
```

### 三.4 标签

> 标签只存储在本地，推送需单独推送

```bash
git tag tag_name

git show tag_name

git tag -a v0.1 -m "version 0.1 released" 1094adb
# 删除标签
git tag -d tag_name

# 推送
git push origin tag_name
# 推送本地所有标签
git push origin --tags

# 删除
git tag -d tag_name
# 删除远程的需先删除本地标签再执行
git push origin :refs/tags/tag_name
```

## 参考

+ [用 Git 上传项目到 GitHub](https://www.jianshu.com/p/0fce531dba31)
+ [朱双印个人日志-git之旅](https://www.zsythink.net/archives/3506)
+ [廖雪峰git教程](https://liaoxuefeng.com/books/git/introduction/index.html)