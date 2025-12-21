---
title: "Mac 安装第三方软件"
date: 2025-12-02T15:05:45+08:00
lastmod: 2025-12-02T15:05:45+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"
# cover:
#     image: "" # image path/url
#     alt: "<alt text>" # alt text
#     caption: "<text>" # display caption under cover
#     relative: false # when using page bundles set this to true
#     hidden: true # only hide on current single page
# editPost:
#     URL: "https://github.com/<path_to_repo>/content"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
---

# MAC OS 安装第三方软件

下载安装包打开后提示包已损坏，移至回收站，此时使用以下命令

<!--more-->

设置 -> 安全 -> 允许安装所有来源软件

```bash
# 1. 设置安全没有 任何来源
sudo spctl --master-disable

# 2. 修改文件属性
sudo xattr -rd com.apple.quarantine /Applications/appName.app
```
