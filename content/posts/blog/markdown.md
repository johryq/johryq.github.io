---
title: "Markdown"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-03T16:34:55+08:00
draft: false
keywords: []
description: ""
tags: ['markdown']
categories: ['blog']
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
<!--more-->

<!--markdown-->
# Markdown

## markdown简介

轻量标记语言,便于转换成html.

> markdown换行时在行末敲 `两个空格` 即可

## 语法及使用

|语法|解析|
|---|---|
| **标题** ! | `!`表示符号与内容之间必须有空格 |
| `# 标题` | 相当于html中的`<h1>`标签 |
| `## 二级标题` | html中的`<h2>` |
|---|---|
| **文字样式** | &nbsp |
| `*内容*` | *斜体* |
| `**内容**` | **加粗** |
| `***内容***` | ***斜体加粗*** |
| `~~内容~~~` | ~~删除线~~ |
|---|---|
| **列表** ! | &nbsp |
| `+ 内容` | 无序列表 (`+`前使用空格分级) |
| `1. 内容` | 有序列表 (分级同上,使用相应数字) |
|---|---|
| **图片** | &nbsp; |
| `![图片简介](图片路径)` | 简介相当于`<a>`标签中的 `alt` 属性 (路径可以是一个图片链接或者本地图片地址) |
| `[简介](网页链接)` |  链接网页,相当于`<a>`标签
| `[简介](#标题)` | 可以实现页面内跳转(vscode中的markdown预览可以实现) |
| `[简介][数字]` | 可在文章末尾使用 `[数字]:链接` 来实现a标签 |
|---|---|
| **代码** | &nbsp |
| *\`echo hello\`* | 单行代码,使用 **`** 包括代码 (键盘esc下面那个键) |
| *\`\`\`* | 首行和尾行添加左边三个 *`* 即可实现(行首可指定编程语言) |
| `> 内容` ! | 引用区块(多行在行首添加`>`即可 |

### 表格

``` txt
| 表头列一 | 列二 |
|---|---| #用以分割表头与内容
| 行二 | 行二 |
| 行三 | 行三 |
```

效果:

|表头列一|列二|
|---|---|
| 行二 | 行二 |
| 行三 | 行三 |