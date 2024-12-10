---
title: "Scrapy Vscode Debug"
date: 2021-06-29T08:46:23+08:00
lastmod: 2024-12-04T08:46:23+08:00
draft: false
keywords: []
description: ""
tags: ['scrapy','code']
categories: ['python']
author: "2332334"

---
<!--more-->

# Scrapy vscode调试项目

> 2021年6月29日

## 配置vscode运行配置

<kbd>ctrl</kbd>+ <kbd>shift</kbd> + <kbd>d</kbd>
点击齿轮配置按钮,生成配置文件

``` json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Python: 当前文件",
            "type": "python",
            "request": "launch",
            "program": "${file}",
            "cwd": "${workspaceFolder}/项目名称",
            "console": "integratedTerminal",
            // "args": [
            //     "crawl",
            //     "爬虫名字"
            // ]
        }
    ]
}
```

> 之后即可 <kbd>F5</kbd> 直接运行了(然后就没然后了)

在settings.py文件新建run.py

```python
from scrapy.cmdline import execute
import sys
import os
# 获取当前脚本路径
dirpath = os.path.dirname(os.path.abspath(__file__))
#运行文件绝对路径
print(os.path.abspath(__file__))
#运行文件父路径
print(dirpath)
# 添加环境变量
sys.path.append(dirpath)
#切换工作目录
os.chdir(dirpath)
# 启动爬虫,第三个参数为爬虫name
execute(['scrapy','crawl','爬虫名字'])
```

> 然后第一个设置配置文件就没啥用了,配置第二个,即可名中spiders中的断点

## Scrapy shell


## 参考

+ [如何使用vscode调试scrapy爬虫项目](https://www.myfreax.com/debug-scrapy-crawler-project-with-vscode/)
+ [vscode 调试和运行scrapy](https://blog.csdn.net/wq_ocean_/article/details/100607310)