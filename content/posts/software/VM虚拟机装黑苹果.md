---
title: "VM虚拟机装黑苹果"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T13:28:22+08:00
draft: false
keywords: []
description: ""
tags: []
categories: ['software']
author: "2332334"

---
<!--more-->

<!--markdown-->莫名奇妙看到黑苹果,就复习一下之前的安装过程吧!

> 虚拟机版本: vm16

> macos版: Big Sur 11.0.1 20B50

## 1.[unlocker][1]

> vm默认没有创建apple虚拟机的选项,通过该工具可以解锁apple的虚拟机选项.

1. 通过上面的Github地址下载该软件

2. 然先结束vm的所有进程及服务

3. 以`管理员方式`运行`win-install.cmd`即可

工具使用后:

![apple.png][2]

## 2.下载苹果镜像

> 推荐下载地址:[黑果小兵][3]

下载完成后是苹果的`dmg`文件需要转换为`iso`文件才可使用(cdr好像可以直接使用)

我这里使用的是`any to iso`;`UltraISO`转换的不能用!

最后我安装最新的11.0版本只打开`colver`引导工具,没给装上(没有安装选项)!

## 安装系统

这里我又下载了`10.15.7`的版本尝试,colver都没进去...

最后先把镜像刻录到u盘然后安装的,[刻录工具][4]

安装界面如下,直接空格就好

![apple2.png][5]

这里莫名出现这种情况,这时会出现下面的`button`无法选中的情况,这时需要调整虚拟机的缩放横纵比即可!

![apple3.png][6]

>安装时需要先格式化虚拟机分配的那个磁盘才可以!

最后登录界面

![apple4.png][7]

> 更多参考资料可以看  [黑果小兵][8]

  [1]:https://github.com/BDisp/unlocker

  [2]: https://www.johryq.top/usr/uploads/2020/12/1253946995.png

  [3]:https://blog.daliansky.net/

  [4]:https://www.balena.io/etcher/

  [5]: https://www.johryq.top/usr/uploads/2020/12/198477698.png

  [6]: https://www.johryq.top/usr/uploads/2020/12/4041053887.png

  [7]: https://www.johryq.top/usr/uploads/2020/12/3475331549.png

  [8]:https://blog.daliansky.net/
