---
title: "Kubernetes"
date: 2024-12-03T10:06:32+08:00
lastmod: 2024-12-03T10:06:32+08:00
draft: false
keywords: []
description: ""
tags: [k8s,kubernetes,DICD]
categories: ['software']
author: "2332334"
---

# kubernetes

> 基于minikuber 练习  
> 跟随教程  [https://github.com/guangzhengli/k8s-tutorials?tab=readme-ov-file#kubernetes-tutorials](https://github.com/guangzhengli/k8s-tutorials?tab=readme-ov-file#kubernetes-tutorials)
<!--more-->

```bash
# 暴露端口
kubectl port-forward [pod_name] [local_port]:[pod_port]

# 描述
kubectl describe pod [pod_name]


kubectl get endpoints


kubectl exec -it nginx --  /bin/sh
```


## pods

```bash
# show all pods
kubectl pods get

kubectl delete pod [pod_name]

kubectl describe pod [pod_name]

kubectl get pod -o wide

```

## deplayment

```bash
# version change
kubectl rollout history deployment [deployment_name]

kubectl rollout undo deployment/[deployment_name] --to-revision=2

```

## service

```bash
kubectl get service

```