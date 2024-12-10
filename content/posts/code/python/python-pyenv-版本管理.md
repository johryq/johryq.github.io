---
title: "Python_版本管理"
date: 2024-10-21T11:03:49+08:00
lastmod: 2024-10-21T11:03:49+08:00
draft: false
keywords: []
description: ""
tags: ['pyenv','python','code']
categories: ['python']
author: "2332334"
---
<!--more-->

# python 版本管理

pyenv自动安装脚本
```bash
curl https://pyenv.run | bash
```

## 一.[pyenv基本使用](https://github.com/pyenv/pyenv)

```bash
# 查看当前版本
pyenv version

# 查看所有版本
pyenv versions

# 查看所有可安装的版本
pyenv install --list

# 安装指定版本
pyenv install 3.6.5
# 安装新版本后rehash一下
pyenv rehash

# 删除指定版本
pyenv uninstall 3.5.2

# 指定全局版本
pyenv global 3.6.5

# 指定多个全局版本, 3版本优先
pyenv global 3.6.5 2.7.14

```

> 实际上当你切换版本后, 相应的pip和包仓库都是会自动切换过去的


## 二.MACOS install时CMD给出下载链接后无下载进度，无法下载

```bash
Downloading Python-2.7.18.tar.xz...
-> https://www.python.org/ftp/python/2.7.18/Python-2.7.18.tar.xz
```

用浏览器下载上面链接的文件将其复制到  `~/.pyenv/cache` 目录下再次执行intall即可

> pyenv 只能管理通过它安装的python，无法管理单独下载python安装包安装的版本

## 三 [用于管理 virtualenv 的 pyenv 插件](https://github.com/pyenv/pyenv-virtualenv)