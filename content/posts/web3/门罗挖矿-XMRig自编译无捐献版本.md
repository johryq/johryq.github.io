---
title: "门罗挖矿 XMRig自编译无捐献版本"
date: 2021-11-08T19:58:37+08:00
lastmod: 2024-12-03T16:26:37+08:00
draft: false
keywords: []
description: ""
tags: [XMRig]
categories: []
author: "2332334"
---
<!--more-->


# XMRig无捐献

[之前][1]尝试了一下挖门罗币,发现使用的工具 `XMRig` 开源且用的人还蛮多,但是使用默认会有1%的捐献比例!

于是找了找无捐献版本并做个记录:

## linux版本

1.安装依赖

```  bash
sudo apt-get install git build-essential cmake libuv1-dev libssl-dev libhwloc-dev -y
```

如果想要静态版本(如果多机器运行还是编译这个版本)，则在上面的依赖安装完成后,再输入：

``` bash
sudo apt-get install automake libtool autoconf -y
```

2.下载XMRig

工具官方 [GitHub 仓库][2]

``` bash
sudo apt install git

git clone git@github.com:xmrig/xmrig.git

```

3.修改源代码

``` bash
vim xmrig/src/donate.h
```

将以下内容

``` conf
constexpr const int kDefaultDonateLevel = 5;

constexpr const int kMinimumDonateLevel = 1;
```

修改为：

``` conf
constexpr const int kDefaultDonateLevel = 0;

constexpr const int kMinimumDonateLevel = 0;
```

4.编译

``` bash
mkdir xmrig/build # 新建个文件夹装编译后文件

cd xmrig/build    #进入build文件夹

cmake ..

make -j$(nproc)
```

静态编译

``` bash

mkdir xmrig/bulid

cd xmrig/scripts && ./build_deps.sh #进入xmrig目录执行build_deps.sh文件

cd ../build

cmake .. -DXMRIG_DEPS=scripts/deps

make -j$(nproc)
```

编译完成后使用ldd xmrig验证文件依赖

最后就可以直接复制build文件夹来运行里面的程序了

### win版本

本来是打算编译这个版本的,但是我电脑装的vs2019;

就算下了c++的支持我也没有编译成功,索性就编译linux的;

最后感觉还是装linux的好点,win的不知道什么时候就卡死了!

跑起来电脑卡到爆炸!

1.下载并安装 `cuda`

> cuda: N卡推出的并行计算平台,可以使用显卡算力吧!  

> 查看cuda版本的话 `控制面板 -> NVIDIA控制面板 -> 左下角 系统信息 -> 组件 -> NCVCUDA.dll 那行`  

>跑门罗的话感觉没必要吧!我没测试过还是下了!版本好像自动检查本机cuda版本!

[下载链接](https://developer.nvidia.com/cuda-downloads?target_os=Windows&target_arch=x86_64&target_version=10&target_type=exelocal)

2.下载 `xmrig` 源代码

[GitHub仓库地址](https://github.com/xmrig/xmrig)

[下载链接](https://github.com/xmrig/xmrig/archive/master.zip)

3.下载 `Visual Studio 2017`并安装`c++桌面开发`工作负载

[下载链接](https://visualstudio.microsoft.com/zh-hans/vs/older-downloads/)

4.下载并安装 `Cmake` (跨平台安装,编译工具)

[下载链接](https://cmake.org/download/)

5.编译

打开`PowerShell`执行以下命令

``` bash
mkdir build

cd build

cmake .. -G "Visual Studio 15 2017 Win64" -T v140,host=x64
```

成功执行后 `Cmkake` 会在 `xmrig` 源代码目录下build目录生成vs的`.sln`文件

打开该文件修改 `Option.sh` :

``` C
iniline int donateLevel() const {return 0;}

```

将原本 `return m_donateLevel;` 修改为 `return 0;`即可

然后编译该项目,为啥问题基本就ok了.

> 有些和参考链接不一样,不晓得有没有问题,有问题参考下面链接

## 参考链接

+ [linxu编译无捐献xmrig](https://www.jianshu.com/p/d896c41a13ec)

+ [linxu编译无捐献xmrig(方法2)](https://zhuanlan.zhihu.com/p/100083701)

+ [win无捐献xmrig(1)](https://www.jianshu.com/p/1779022d117c)

+ [win无捐献xmrig(2)](https://www.freesion.com/article/7548175944/)

+ [win查看cuda版本](https://blog.csdn.net/qq_38295511/article/details/89223169)

[1]:https://www.johryq.top/index.php/archives/12/

[2]:https://github.com/xmrig/xmrig