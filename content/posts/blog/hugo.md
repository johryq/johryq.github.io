---
title: "Hugo"
lastmod: 2024-10-12T11:20:37+08:00
lastmod: 2024-10-12T11:20:37+08:00
draft: false
keywords: []
description: ""
categories: []
author: "2332334"
tags: ['go','hugo']
categories: ['blog']
---



# [Hugo](https://gohugo.io/)

> go 写的静态网站生成器；类似的node hexo，vue vuePress等

<!--more-->

## 一.基本使用

```bash
# 初始化项目
hugo new site [dir_name]

# 下载主题
git submodule add [theme_url] [theme_dir]

# 新建文章
hugo new content/posts/my-first-post.md

# 运行
hugo server

# 渲染包含草稿内容
hugo server -D

# 部署
hugo
```

## 二.配置文件`hugo.toml`

paperMod 主题[配置参考](https://adityatelange.github.io/hugo-PaperMod/archives/)

## 三.主题

> 在自己目录相同位置，创建相同文件即可覆盖主题内容  
> 在下载主题后有额外信息的情况下