---
title: "Failed Start Journal Service"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T09:02:46+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"

---
<!--more-->


# Failed to start journal service

排除思路

1.查看启动失败的服务

``` bash
systemctl --failed
```

2.根据启动失败的服务查看该服务的状态

``` bash
systemctl status servername
```

3.使用`journalctl`查看相关服务

```bash
journalctl _PID=xxx

journalctl _SYSTEMD_UNIT=servername.service

journalctl -xe
```

4.内核模块

> Linux系统加载哪些内核模块，和配置文件有关系。模块保存在/lib/modules/下。/etc/modprobe.d/下配置模块加载时的一些参数，也可以利用blacklist来屏蔽模块的自动加载。例如，在安装NVIDIA显卡驱动时，需要屏蔽开源的nouveau驱动，就可以将其加入blacklist。

最后查看那些内核模块出现问题或冲突  

然后修改内核配置文件以解决问题

## 参考

+ [systemd-modules-load.service启动失败问题排查](https://jlice.top/p/7ve9p/)