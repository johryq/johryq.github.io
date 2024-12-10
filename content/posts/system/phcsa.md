---
title: "Phcsa"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T09:00:12+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"

---
<!--more-->

# PHCSA

## 考点

### RedHat 重置密码

1. 重启`e`
2. linux行末尾输入`rd.break console=tty0`
3. ctrl+x

``` bash
chroot /sysroot
mount -o remount,rw /
passwd root         #echo passwd | passwd --stdin userName
touch /.autorelabel
reboot -f
```

### cockpit(驾驶舱)

``` bash
systemctl enable cockpit.socket --now
yum -y install cockpit cockpit-machines cockpit-dashboard
```

### 网络配置

network -> NetWorkManger

> 8 开始使用后者, 7 两个都可用,以前版本使用前者

配置文件简单参数:

```conf

```

nmtui

> NetworkManager Text User Interface

### 命令

esc + . 复制命令最后参数

### SELinux

状态

+ Enforcing 强制
+ Permissive 宽松
+ Disabled 禁用

``` bash

vi /etc/selinux/config
LINUX=permissive
#重启时生效

setenforce 0
# 立即生效进入宽松模式

getenforce
# 查看信息
```

#### 修改set配置

查找错误信息

``` bash
# 安装selinux日志详情记录的包
yum -y install setroubleshoot-server
sustemctl restart httpd

# 1. 通过这个包查看日志获取个id ;再查看详细信息
grep setrouble /var/log/messages
sealert -l 

# 2. 启动服务失败直接使用 journalctl 查看
journalctl -xe
```

#### 配置selinux

```bash
# 预设策略
getsebool -a
setsebool -P 策略参数名=on 
# -P永久打开

---
# 修改文件策略

semanage fcontext -l
# 列出策略

semanage fontext -a -t 
# 添加策略

semanage fcontext -d 
# 删除策略

---
# 端口策略
semanage port -l

semanage port -a -t 策略类型 -p 协议 端口号

semanage port -d
```

### 配置 YUm

配置文件

``` bash
vi /etc/yum.conf
vi /etc/yurn.repos.d/name.repo
```

yum源

```repo
[仓库标识1]
name = 
baseurl = 
enable = 1 | 0
gpgcheck = 1 | 0
#gpgkey = 
```

检查仓库

```bash
yum repolist
yum -y install bash-completion net-tools vim-enhanced bind-utils
yum provides "文件路径" | 命令 # 查找包及其路径
```

### tuned配置集(系统调优)

```bash
yum -y install tuned
systemctl enable tuned --now
tuned-adm recommend # 推荐方案
tuned profile virtual-guest
runed-adm active
```

### 权限用户管理

password文件

```bash
/etc/passwd
/etc/shadow
```

用户

``` bash
useradd [-u uid] [-g baseGroup] [-G group] [-d homePath] [-s 登录shell] userName
userdel -r userName
usermod [-u uid] [-g baseGroup] [-G group] -[d homePath] userName

id userName

echo passwd | passwd --stdin userName
```

组

```bash
groupadd groupName
groupdel groupName
gpasswd -a userName GroupName
gpasswd -d userName GroupName
groups
usermod -a -G groupName userName
```

用户访问控制列表

``` bash
getfacl

setfacl -m user:用户名:权限组合 路径
setfacl -m group:组名:权限组合 路径

# ex
setfacl -m u:userName:rwx path

r 4 w 2 x 1
```

特殊权限

```bash
# 即 x 权限改为 s

set-uid     4
set-gid     2
# 使用该文件的用户自动拥有该用户的权限


粘滞位 t    1
# 用户拥有w权限目录,不能删除其他人文件
```

### 计划任务 cron

> 服务 crond

配置文件

```bash
/etc/crontab
/var/spool/cron/userName
```

配置工具

```bash
crontab -e -u userName
# 编辑计划任务 -l -d

*/5 * 1-5 * * /bin/ls
# 每周1-5号,每隔5min执行一次
```

### NTP时间同步

ntp,Newwork Time Protocol
chrony

vi /etc/chrony.conf

### autofs

yum -y install nfs-utils

/etc/auto.master

### 分区|格式化|扩展分区

partprobe /dev/sda

partx -a /dev/sda

VDO卷

> Virtual Data Optimizer 虚拟数据优化器

跳过去重分析

mkfs.xfs -K
mkfs.ext4 -E nodiscard

x-systemd.requires=vdo.service | (_netdev)

### Podman(podmanager)容器管理

yum module install -y container-tools

-p 真机端口:容器端口 -v 真机目录:容器目录 --name 名字

生成服务

vi /usr/lib/systemd/system
vi /etc/systemd/system

podman generate systemd --name --files
systemctl deamon-reload

rootless 无根环境

+ 端口1024+
+ 配置目录 ~/.config/systemd/user/
+ systemctl --user

loginctl enable-linger
loginctl show-user 名字

crontab -e
@reboot /usr/bin/systemctl --user  restart container-name