---
title: "Jenkins"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T10:12:49+08:00
draft: false
keywords: []
description: ""
tags: []
categories: ['software']
author: "2332334"

---
<!--more-->

# jenkins

> jave写的项目持续集成(CI)工具
> 自动化构建,测试,交付,部署

## 安装

基本硬件要求:

1. 256mb RAM
2. 1G存储空间,docker运行,建议最小10g

软件要求:

> 需要`java`才能运行

OpenJDK

``` bash
sudo apt update

# 搜索你需要的openjdk版本安装
sudo apt search openjdk

sudo apt install openjdk-11-jdk

java -version
```

### ubuntu

``` bash
# LTS版
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > \
    /etc/apt/sources.list.d/jenkins.list'
sudo apt-get update
sudo apt-get install jenkins


# DNF LTS
sudo wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
sudo dnf upgrade
sudo dnf install jenkins java-devel
```

> 其他可直接`apt install kenkins`安装

启动 jenkins

``` bash
sudo systemctl start jenkins
```

输出内容

``` shell
Loaded: loaded (/etc/rc.d/init.d/jenkins; generated)
Active: active (running) since Tue 2018-11-13 16:19:01 +03; 4min 57s ago
```

> 注意防火墙

### centos

``` bash
# LTS
sudo wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
sudo yum upgrade
sudo yum install jenkins java-1.8.0-openjdk-devel
sudo systemctl daemon-reload

# 启动
sudo systemctl start jenkins
```

### Docker安装

> 推荐 jenkins/jenkins 镜像,LTS版没有docker CLI且功能不完全

```bash
# 拉取镜像
docker pull jenkins/jenkins

# 运行镜像
docker run \
  --name jenkins-docker \
  --rm \
  --detach \
  --privileged \
  --network jenkins \
  --network-alias docker \
  --env DOCKER_TLS_CERTDIR=/certs \
  --volume jenkins-docker-certs:/certs/client \
  --volume jenkins-data:/var/jenkins_home \
  --publish 2376:2376 \
  docker:dind \
  --storage-driver overlay2
```

### 安装配置

1. 访问`http://localhost:8080`
2. 从Jenkins控制台日志输出中，复制自动生成的字母数字密码（在两组星号之间）

``` bash
# 打印密码
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

## 参考

+ [jenkins中文网](http://www.jenkins.org.cn/821.html)
+ [jenkins官网文档](https://www.jenkins.io/doc/)