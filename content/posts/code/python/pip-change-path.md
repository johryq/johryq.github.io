---
title: "Pip Change Path"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T08:49:55+08:00
draft: false
keywords: []
description: ""
tags: ['pip','pythone']
categories: ['python']
author: "2332334"

---
<!--more-->

<!--markdown-->
# 修改pip下载位置

之前装python3下了很多包,看着日渐填满的C盘空间就想给 `pip` 下载的包挪个位置!

搜到的改包路径其实就是修改 `site.py` 文件的两个参数:

## 具体步骤

### 1.查找文件所在位置

``` bash
#所有依赖的位置
python -m site

#查看 site.py 位置
python -m site -help
```

## 2.找到文件之后修改以下参数内容即可

``` python

USER_BASE =  #包的位置

USER_SITE =  #pip脚本位置

```

![pip.png](./img/pip.png)

之后就ok了

## 参考地址

+ [【强迫症系列】【win】更改 Python 的 pip install 默认安装依赖路径](https://blog.csdn.net/mukvintt/article/details/80908951)

+ [PIP INSTALL 默认安装路径修改](https://www.cnblogs.com/yinliang/p/12931685.html)
