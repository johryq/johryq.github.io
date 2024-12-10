---
title: "Node_nvm"
date: 2024-10-21T16:31:37+08:00
lastmod: 2024-10-21T16:31:37+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"
---
<!--more-->

# nvm—node版本管理

[nvm github](https://github.com/nvm-sh/nvm)

## install

```bash
# 安装脚本，最后访问上面github链接使用最新版本
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash

# 环境变量
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm

source ~/.zshrc
```

## 基本使用

```bash
# 展示版本
nvm ls
nvm ls-remote

# 下载
# 这将下载最新node
nvm run node --version

# 使用
nvm use system
nvm run system --version

# 当前cmd一次新使用

nvm exec

# 重命名
nvm alias my_alias v14.4.0
# 设置默认版本
nvm alias default node 


# 查看安装目录
nvm which 12.22

# 停用nvm，使用默认的npm
nvm deactivate

export NVM_NODEJS_ORG_MIRROR=https://nodejs.org/dist
export NVM_IOJS_ORG_MIRROR=https://iojs.org/dist

```