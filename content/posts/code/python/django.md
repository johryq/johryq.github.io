---
title: "Django"
date: 2021-11-08T19:58:45+08:00
lastmod: 2024-12-03T16:37:53+08:00
draft: false
keywords: []
description: ""
tags: ['django','python','code']
categories: ['python']
author: "2332334"

---
<!--more-->

# Django

> python后端框架  
> [官网](https://www.djangoproject.com/)

## 安装

``` bash
python -m pip install django

python3

import django
django.get_version()
```

## start

### 新建项目

1.创建项目和应用

```bash
django-admin startproject projectName

cd projectName

python mange.py startapp appName
```

2.配置项目的`urls.py`

```py
from django.contrib import admin
from django.urls import path,include

urlpatterns = [
    path('',include('appname.urls')),
    path('admin/', admin.site.urls),
]
```

3.新建app的`urls.py`

```py
from django.urls import path
from . import views

urlpatterns = [
    path('',views.index,name='index'),
]
```

4.创建数据库模型

```py
from django.db import models

class proxy(models.Model):
    def __str__(self):
        return str(self.proxyIP)+':'+str(self.proxyPort)
    proxyIP = models.CharField(max_length=30)
    proxyPort = models.IntegerField()
```

5.配置项目`setting.py`添加该模型

```py
INSTALLED_APPS = [
    'get_ip.apps.GetIpConfig',
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
```

> 第一项为新增内容,即`app`中`apps.py`的第一个类

6.编写`view.py`

```py

```

7.生成数据库

```bash
cd appname
mkdir -p templates/appname
touch templates/appname/index.html

cd ../
py manage.py migrate
python manage.py makemigrations appName
python manage.py migrate
```

8.剩下

+ templates的html模板
+ vies.py中返回给模板的内容
+ urls.py新加页面或者请求

### 基本命令

``` bash
django-admin startproject projectName
# 创建项目

python mange.py startapp appName
# 创建应用

python mange.py runserver [0:8080]
# 运行项目,ip端口可选

----
# db相关

python manage.py migrate
# 创建/最后更新数据库

python manage.py makemigrations appName
# 数据迁移,结构改变,生成相关py脚本

python manage.py sqlmigrate appName 0001
# 查看迁移执行的sql语句;默认在appName/migrations/下
```
