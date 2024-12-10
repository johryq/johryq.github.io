---
title: "Hexo Next Theme"
date: 2023-08-22T10:34:05+08:00
lastmod: 2024-12-04T08:25:05+08:00
draft: false
keywords: []
description: ""
tags: ['Hexo-next']
categories: ['blog']
author: "2332334"

---
<!--more-->


# Hexo-next主题使用并上传Github


## 1. hexo 安装


```bash
npm install hexo-cli -g
hexo init blog
cd blog
npm install
```

## 2. hexo 主题安装

```bash
cd your-hexo-site
# 老版本仓库已不再维护
# git clone https://github.com/iissnan/hexo-theme-next themes/next

# git clone https://github.com/theme-next/hexo-theme-next themes/next
# 这个库2-3年更新的了

npm install hexo-theme-next
# npm 安装这个在维护版本，安装完成后修改配置文件中theme配置

hexo server --debug
# 查看安装是否ok，并安装缺失的相关包
```

安装报错依据提示查看报错信息安装相关包

```bash
#npm i hexo-renderer-swig 
#npm install nunjucks

npm install -- save-dev hexo-util
```


## 3. 使用一键部署脚本配置并上传github

按如下配置
```yml
deploy:
  type: 'git'
  repo: https://github.com/<your github name>/<your github name>.github.io
  branch: gh-pages
```

```bash
git init
npm install hexo-deployer-git --save
hexo clean & hexo g & hexo d
```

> 如上即可访问 `<your github name>.github.io` 访问部署的页面
