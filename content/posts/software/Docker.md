---
title: "Docker"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T09:12:16+08:00
draft: false
keywords: []
description: ""
tags: ['docker']
categories: ['software']
author: "2332334"

---
<!--more-->

# docker

## docker容器简介

虚拟化容器

docker大致由三部分组成 **仓库** **镜像** **容器**

## docker安装

> `卸载旧版本`

``` bash
# ubuntu
sudo apt-get remove docker docker-engine docker.io containerd runc

# centos
sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
```

### 自动化脚本安装(test环境,root用户)

方式一:

``` bash
curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun
```

方式二:

``` bash
curl -fsSL https://get.docker.com -o get-docker.sh \ sudo sh get-docker.sh
sudo sh get-docker.sh
```

卸载

``` bash
sudo apt-get purge docker-ce docker-ce-cli containerd.io
sudo rm -rf /var/lib/docker
sudo rm -rf /var/lib/containerd
```

### 仓库安装(推荐)

#### ubuntu

``` bash
sudo apt-get update

sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg


# x86_64/amd64
echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io
```

#### centos

``` bash
sudo yum install -y yum-utils

sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo

sudo yum install docker-ce docker-ce-cli containerd.io

sudo systemctl start docker

sudo docker run hello-world
```

### 手动安装

> 添加用户: `sudo usermod -aG docker your-user`

1.选择`https://download.docker.com/linux/`需要的版本

+ `centos/x86_74/stable/Packages/.rpm`

+ `dists/pool/stable/.deb`

ubuntu

``` bash
sudo dpkg -i /path/to/package.deb

sudo docker run hello-world
```

centos安装`Docker Engine`

``` bash
sudo yum install /path/to/package.rpm
# 安装docker完成,并创建了docker组

sudo systemctl start docker

sudo docker run hello-world
```

## docker相关命令

### 仓库

``` bash
docker search 你要找的镜像

docker pull 下载镜像到本地
```

### 镜像

``` bash
docker images
# 展示你本地的镜像信息

docker rmi
# remove 镜像
```

### 容器

> 运行容器

`docker run 参数 --name 名字 路径` #运行某容器

| 基本参数 | 解析 |
| --- | --- |
| -i | 交互模式 |
| -t | 终端 |
| -d | 后台运行 |
| -P | 将容器内部使用的网络端口映射到我们使用的主机上 |
| -p | 将端口映射到本地制定端口 |
| v | 主机路径:容器内路径 ｜
| --name |  容器名 |

``` bash
docker run -it image:[version] /bin/bash

docker run -d image:[version] /bin/bash

docker logs containerID
# 容器标准输出
```

<kbd>Ctrl</kbd> +  <kbd>p</kbd>  + <kbd>q</kbd> 退出容器而不终止

> 查看容器

``` bash
docker ps -a  #查看所有容器状态等信息

docker port #端口相关

docker top

docker inspect 底层信息，Docker容器配置和状态信息
```

> 重启容器相关

``` bash
docker start 容器ID或者容器名字 
# 启动已停止容器

docker restart ID/Name 
# 重启停止的容器

docker stop ID/Name 
#停止

docker attach ID/Name 
#进入后台运行的容器但是退出会使容器停止

docker exec ID/Name 
# 这个命令进入后台容器，退出容器终端时，不会导致容器的停止
```

> 删除容器

``` bash
docker rm -rf ID/Name 
#删除停止的容器

docker container prune 
#清理掉所有终止的容器
```

> 导入导出容器快照

``` bash
docker export 容器ID > 文件名.tar 
#导出

docker import 
#本地导入

docker import 地址 镜像 
#通过URL或目录导入

```

## 打包镜像-dockerfile

相关指令

| 命令        | 解释 |
| - | - |
| FROM        | 构建基于那个镜像 |
| ENV         | 设置环境变量 |
| ADD         | copy文件或目录到容器，如果是URL或压缩包会自动下载解压 |
| COPY        | 与上类似，但不具备后述功能 |
| MAINTAINER  | img维护者邮箱及姓名 |
| RUN         | 构建镜像执行的命令，每run一次构建一层 |
| CMD         | 容器启动命令，如多个以最后一个为准，也可为netrypoint提供参数 |
| VOLUME      | 指定容器挂载点到宿主机自动生成目录或其他容器 |
| USER        | 为run，cmd，entrypoint执行指定用户 |
| WORKDIR     | 为run，cmd，entrypoint，copy，add 设置工作目录，即切换目录 |
| HEALTHCHECH | 健康检查 |
| ARG         | 构建时指定参数 |
| EXPOSE      | 声明服务端口，仅声明 |
| ENTRYPOINT  | 运行容器时执行shell命令 |

## docker-compose



## 参考

+ [菜鸟docker教程](https://www.runoob.com/docker/docker-tutorial.html)

+ [docker官网](https://docs.docker.com/get-docker/)

+ [官方文档](https://docs.docker.com/engine/install)