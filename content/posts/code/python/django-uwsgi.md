---
title: "Django Uwsgi"
date: 2021-11-08T19:58:45+08:00
lastmod: 2024-12-04T08:51:45+08:00
draft: false
keywords: []
description: ""
tags: ['django','python','code']
categories: ['python']
author: "2332334"

---
<!--more-->

# Django uWSGI

> uWSGI 是一个快速的，自我驱动的，对开发者和系统管理员友好的应用容器服务器，完全由 C 编写。  
> dgango搭配nginx  
> mod_wsgi搭配apache

## 安装配置

### 安装

``` bash
python -m pip install uwsgi

# or install LTS
python -m pip install https://projects.unbit.it/downloads/uwsgi-lts.tar.gz
```

### 配置启动

``` bash
uwsgi --chdir=/path/to/your/project \
    --module=mysite.wsgi:application \
    --env DJANGO_SETTINGS_MODULE=mysite.settings \
    --master --pidfile=/tmp/project-master.pid \
    --socket=127.0.0.1:49152 \      # can also be a file
    --processes=5 \                 # number of worker processes
    --uid=1000 --gid=2000 \         # if root, uwsgi can drop privileges
    --harakiri=20 \                 # respawn processes taking more than 20 seconds
    --max-requests=5000 \           # respawn processes after serving 5000 requests
    --vacuum \                      # clear environment on exit
    --home=/path/to/virtual/env \   # optional path to a virtual environment
    --daemonize=/var/log/uwsgi/yourproject.log      # background the process
```

配置  

`uwsgi --ini uwsgi.ini`

``` ini
[uwsgi]
chdir=/path/to/your/project
module=mysite.wsgi:application
master=True
pidfile=/tmp/project-master.pid
vacuum=True
max-requests=5000
daemonize=/var/log/uwsgi/yourproject.log
env = LANG=en_US.UTF-8
```

## 参考

+ [如何用 uWSGI 托管 Django](https://docs.djangoproject.com/zh-hans/3.2/howto/deployment/wsgi/uwsgi/)