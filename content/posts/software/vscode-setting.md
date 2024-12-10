---
title: "Vscode Setting"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T09:04:28+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"

---
<!--more-->

# VS code配置文件属性

## VS code

### 1.首选项 -> Files.eol -> \n

### 2.`EditorConfig for Visual Studio Code`插件

``` editorconfig
root = true

[*]
charset = utf-8
indent_style = space
indent_size = 2
end_of_line = lf
insert_final_newline = true
trim_trailing_whitespace = true
```

## Git配置

``` bash
# clone git 时自动选择LF还是CRLF
git config --global core.autocrlf true

git config --global core.autocrlf input

git config --global core.autocrlf false
```

## dos2unix

> 处理`windows LF`结尾符转`unix CRLF`

`find . -type f -exec dos2unix {} \;` 未测试命令

## 参考

+ [vscode如何替换所有文件的回车格式为LF呢？](https://segmentfault.com/q/1010000011799577)
+ [editorconfig](https://editorconfig.org/)