---
title: "Python_虚拟环境"
date: 2024-10-21T10:41:26+08:00
lastmod: 2024-10-21T10:41:26+08:00
draft: false
keywords: []
description: ""
tags: ['python','venv','pyenv']
categories: ['python']
author: "2332334"

---
<!--more-->


# python 虚拟环境   

## venv

```bash
# 在当前目录创建虚拟环境
python3 -m venv .
```

> pyvenv 是针对 Python 3.3 和 3.4 创建虚拟环境的推荐工具，并在 3.5 中被直接执行 venv 的方式所取代。


## [pyenv-virtualenv](https://github.com/pyenv/pyenv-virtualenv)

```bash
# 创建2.7.10 python版本的环境-环境名为 my-virtual-env-2.7.10
pyenv virtualenv 2.7.10 my-virtual-env-2.7.10

# 创建当前正在使用python版本的环境
pyenv virtualenv my-virtual-env-current_python_version

# 查看已创建的环境
pyenv virtualenvs

# 激活环境
pyenv activate <name>
pyenv deactivate

# 删除
pyenv uninstall my-virtual-env
```

> 上述创建的版本目录都在 `$(pyenv root)/versions` 下  
> py3.3以上版本使用venv即可

## more

+ [venv](https://docs.python.org/zh-cn/3/library/venv.html)