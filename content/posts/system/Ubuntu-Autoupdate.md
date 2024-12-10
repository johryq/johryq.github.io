---
title: "Ubuntu Autoupdate"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T13:26:19+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"

---
<!--more-->


# ubuntu设置自动更新

[参考地址](https://www.jianshu.com/p/52677157166d)

## 1.使用 APT-GET 命令和 APT 命令来安装 unattended-upgrades 软件包

`$ sudo apt-get install unattended-upgrades`

+ 下方两个文件可以使你自定义该机制：

```bash
/etc/apt/apt.conf.d/50unattended-upgrades

/etc/apt/apt.conf.d/20auto-upgrades
```

## 2.在 50unattended-upgrades 文件中做出必要修改

默认情况下只有安全更新需要的最必要的选项被启用。但并不限于此，你可以配置其中的许多选项以使得这个机制更加有用。

我修改了一下文件并仅加上被启用的行以方便阐述：

```bash
# vi /etc/apt/apt.conf.d/50unattended-upgrades

Unattended-Upgrade::Allowed-Origins {

"${distro_id}:${distro_codename}";

"${distro_id}:${distro_codename}-security";

"${distro_id}ESM:${distro_codename}";

};

Unattended-Upgrade::DevRelease "false";

```

有三个源被启用，细节如下：

+ `${distro_id}:${distro_codename}`：  
这是必须的，因为安全更新可能会从非安全来源拉取依赖。

+ `${distro_id}:${distro_codename}-security`：  
这用来从来源得到安全更新。

+ `${distro_id}ESM:${distro_codename}`：  
这是用来从 ESM（扩展安全维护）获得安全更新。

> 启用邮件通知： 如果你想要在每次安全更新后收到邮件通知，那么就修改以下行段（取消其注释并加上你的 email 账号）。

+ 从：

  + `//Unattended-Upgrade::Mail "root";`

+ 修改为：

  + `Unattended-Upgrade::Mail "2daygeek@gmail.com";`

> 自动移除不用的依赖： 你可能需要在每次更新后运行 sudo apt autoremove 命令来从系统中移除不用的依赖。

+ 从：

  + `//Unattended-Upgrade::Remove-Unused-Dependencies "false";`

+ 修改为：

  + `Unattended-Upgrade::Remove-Unused-Dependencies "true";`

> 启用自动重启： 你可能需要在安全更新安装至内核后重启你的系统。你可以在以下行做出修改：

+ 从：

  + `//Unattended-Upgrade::Automatic-Reboot "false";`

+ 到：取消注释并将 false 改成 true以启用自动重启。

  + `Unattended-Upgrade::Automatic-Reboot "true";`

> 启用特定时段的自动重启： 如果自动重启已启用，且你想要在特定时段进行重启，那么做出以下修改。

+ 从：

  + `//Unattended-Upgrade::Automatic-Reboot-Time "02:00";`

+ 到：取消注释并将时间改成你需要的时间。我将重启设置在早上 5 点。

  + `Unattended-Upgrade::Automatic-Reboot-Time "05:00";`

## 3.启用自动更新

> 现在我们已经配置好了必须的选项，一旦配置好，打开以下文件并确认是否这两个值都已设置好？值不应为0。（1=启用，0=禁止）。

```bash
# vi /etc/apt/apt.conf.d/20auto-upgrades

APT::Periodic::Update-Package-Lists "1";

APT::Periodic::Unattended-Upgrade "1";
```

详情：

第一行使 apt 每天自动运行 apt-get update。

第一行使 apt 每天自动安装安全更新

可选参数

```bash
APT::Periodic::Download-Upgradeable-Packages "1";  
//下载更新包 0表示停用设置
APT::Periodic::AutocleanInterval "7";  
// 7日自动删除
```

