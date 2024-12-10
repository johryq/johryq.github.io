---
title: "Kubernetes"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T10:13:39+08:00
draft: false
keywords: []
description: ""
tags: ['docker','k8s']
categories: ['software']
author: "2332334"
---
<!--more-->

# Kubernetes/K8s

[kubernetes官方文档][1]
[minikuber官方教程](https://minikube.sigs.k8s.io/docs/start/)

## 基本组成及相关概念

1. etcd  
  保存了整个集群的状态

2. apiserver  
  提供了资源操作的唯一入口，并提供认证、授权、访问控制、API 注册和发现等机制

3. controller manager  
  负责维护集群的状态，比如故障检测、自动扩展、滚动更新等

4. scheduler  
  负责资源的调度，按照预定的调度策略将 Pod 调度到相应的机器上

5. kubelet  
  负责维护容器的生命周期，同时也负责 Volume（CVI）和网络（CNI）的管理

6. container runtime  
  负责镜像管理以及 Pod 和容器的真正运行（CRI）

7. kube-proxy  
  负责为 Service 提供 cluster 内部的服务发现和负载均衡

other

+ kube-dns 负责为整个集群提供 DNS 服务
+ Ingress Controller 为服务提供外网入口
+ Heapster 提供资源监控
+ Dashboard 提供 GUI
+ Federation 提供跨可用区的集群
+ Fluentd-elasticsearch 提供集群日志采集、存储与查询

[细分使用的对象名称](https://kubernetes.feisky.xyz/concepts/concepts#fu-zhi-kong-zhi-qi-replication-controllerrc)

+ Pod
+ 复制控制器（Replication Controller，RC）
+ 副本集（Replica Set，RS）
+ 部署(Deployment)
+ 服务（Service）
+ 任务（Job）
+ 后台支撑服务集（DaemonSet）
+ 有状态服务集（StatefulSet）
+ 集群联邦（Federation）
+ 存储卷（Volume）
+ 持久存储卷（Persistent Volume，PV）和持久存储卷声明（Persistent Volume Claim，PVC）
+ 密钥对象（Secret）
+ 用户帐户（User Account）和服务帐户（Service Account）
+ 名字空间（Namespace）
+ RBAC访问授权 Role-based Access Control(角色的访问控制)

### kubernetes yaml必须字段

+ apiVersion  kubernetes版本

+ kind        obj 类别

+ metedata    唯一标示对象，name UID or namespace

+ spec        期许状态

## 本地安装及基本使用

### 学习环境安装

minikube

1. 使用[官方安装脚本](https://minikube.sigs.k8s.io/docs/start/
)

```bash

```

### 正式环境-外网

### 正式环境-国内

> 系统: ubuntu 20.04  
> Docker  
> 国内主要问题: gcr.io(Google Cloud Container Registry)被墙

### 本地运行安装

一.安装前置条件

 1. memory and swap accounting 统计Linux内核的内存和交换区
 2. 关闭swap

---

1. 查看是否开启该参数

```bash
cat /proc/cmdline
```

2. 修改配置开启该功能

```bash
vi /etc/default/grub
# GRUB_CMDLINE_LINUX="cgroup_enable=memory swapaccount=1"
# 参数中添加如上内容
```

3. 更新GRUB

```bash
update-grub
```

>  grub启动引导程序

4. 关机swap

```bash
swapoff -a
# 临时关闭

sed -ri 's/.*swap.*/#&/' /etc/fstab
# 永久关闭
```

5. 重启系统

二.安装相关包

```bash
apt-get update && apt-get install -y apt-transport-https
curl https://mirrors.aliyun.com/kubernetes/apt/doc/apt-key.gpg | apt-key add - 
cat <<EOF >/etc/apt/sources.list.d/kubernetes.list
deb https://mirrors.aliyun.com/kubernetes/apt/ kubernetes-xenial main
EOF
apt-get update
apt-get install -y kubelet kubeadm kubectl
```

三.下载镜像

``` bash
kubeadm config images list
# 获取镜像列表
```

从阿里云获取该列表镜像

``` shell
#/bin/bash
images=(  # 下面的镜像应该去除"k8s.gcr.io/"的前缀，版本换成上面获取到的版本
    kube-apiserver:v1.24.0
    kube-controller-manager:v1.24.0
    kube-scheduler:v1.24.0
    kube-proxy:v1.24.0
    pause:3.7
    etcd:3.5.3-0
    coredns/coredns:v1.8.6
)

for imageName in ${images[@]} ; do
    docker pull registry.cn-hangzhou.aliyuncs.com/google_containers/$imageName
    docker tag registry.cn-hangzhou.aliyuncs.com/google_containers/$imageName k8s.gcr.io/$imageName
    docker rmi registry.cn-hangzhou.aliyuncs.com/google_containers/$imageName
done
```

报错 `Error response from daemon: No such image: registry.cn-hangzhou.aliyuncs.com/google_containers/coredns/coredns:1.8.6`

将 images中的 `coredns/coredns:v1.8.6` 替换为 `coredns:1.8.6` 即可

## 参考链接

+ [kubernetes官方文档][1]

+ [安装Kubernetes(k8s)保姆级教程---无坑版 centos7.9](https://www.cnblogs.com/Sunzz/p/15184167.html)

+ [kubernetes安装（国内环境） Ubuntu 16.04](https://zhuanlan.zhihu.com/p/46341911)

+ [kubernetes指南](https://kubernetes.feisky.xyz/introduction/cluster)

  [1]:https://kubernetes.io/zh-cn/
