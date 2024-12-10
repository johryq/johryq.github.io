---
title: "Ansible"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T09:07:38+08:00
draft: false
keywords: []
description: ""
tags: ['ansible']
categories: ['software']
author: "2332334"

---
<!--more-->

# Ansible

通过ssh的python自动化运维工具

## 基本概念

+ Control nodes(控制节点)
+ Managed nodes(受管节点)
+ Inventory(受控节点列表)
  + host file
  + 默认 `/etc/ansible/hosts` ;可通过 `-i` 指定文件位置
+ Modules
+ Task
+ Playbook
  + YAML文件

### command line

| 命令 | 解析 |
| -- | -- |
| `ansible`　| Ansibe AD-Hoc 临时命令执行工具，常用于临时命令的执行 |
| ansible-config |  |
| ansible-console | Ansible基于Linux Consoble界面可与用户交互的命令执行工具 |
| ansible-doc | Ansible 模块功能查看工具 |
| ansible-galaxy | 下载/上传优秀代码或Roles模块 的官网平台，基于网络的 |
| ansible-Inventory | |
| `ansible-playbook` | Ansible 定制自动化的任务集编排工具 |
| ansible-pull | Ansible远程执行命令的工具，拉取配置而非推送配置（使用较少，海量机器时使用，对运维的架构能力要求较高） |
| ansible-vault | Ansible 文件加密工具 |

## 安装

### 前置要求

> python2.6+ || python3.5+
> pip
> Linux发行版
> 被控端如开启SELinux需要安装libselinux-python
> ansible-core 2.12和Ansible 5.0.0将需要Python 3.8或更高版本才能在控制节点上运行。从ansible-core 2.11开始，该项目将仅针对Python 3.8和更高版本进行打包。

```bash
sudo pip install paramiko PyYAML Jinja2 httplib2 six
```

### Github

源码安装

``` bash
git clone git://github.com/ansible/ansible.git --recursive

cd ./ansible

source ./hacking/env-setup
# 在当前bash环境下读取并执行FileName中的命令
```

管理命令

``` bash
# 更新
git pull --rebase
git submodule update --init --recursive
```

### YUM || APT || pip

``` bash
# install the epel-release RPM if needed on CentOS, RHEL, or Scientific Linux
# https://fedoraproject.org/wiki/EPEL 
sudo yum install epel-release -y
sudo yum install ansible


# ubuntu
sudo apt-get install software-properties-common
sudo apt-add-repository ppa:ansible/ansible
sudo apt-get update
sudo apt-get install ansible

# pip
sudo pip install ansible
```

> `ansible all -m ping --ask-pass` 测试安装是否OK

### argcomplete依赖

> ansible 2.9+
> 用以支持命令行补全

``` bash
# CentOS
sudo yum install epel-release
sudo yum install python-argcomplete

# ubuntu
sudo apt install python-argcomplete

# pip
python -m pip install argcomplete
```

#### 配置argcomplete

```bash
# 全局配置
# bash>4.2
sudo activate-global-python-argcomplete

# 单独配置(~/.profile || ~/.bash_profile)
eval $(register-python-argcomplete ansible)
eval $(register-python-argcomplete ansible-config)
eval $(register-python-argcomplete ansible-console)
eval $(register-python-argcomplete ansible-doc)
eval $(register-python-argcomplete ansible-galaxy)
eval $(register-python-argcomplete ansible-inventory)
eval $(register-python-argcomplete ansible-playbook)
eval $(register-python-argcomplete ansible-pull)
eval $(register-python-argcomplete ansible-vault)
```

## 准备工作

### 受控清单

> /etc/ansible/hosts
> 默认组 `all` & `ungrouped`

``` conf
example.com:

[name]
192.0.2.50
aserver.example.org

[range_ep1]
www[01:50].example.com

[range_ep2]
db-[a:f].example.com:5055

[another_name]
ep ep.com
```

YAML版本

``` yaml
all:
    hosts:
        example.com:
    children:
        name:
            hosts:
                192.0.2.50
                aserver.example.org
        range_ep1:
            hosts:
                www[1:50].example.com
        range_ep2:
            hosts:
                db-[a:f].example.com:5055
```

分发密钥

```bash
# 生成密钥
ssh-keygen

#分发密钥
ssh-copy-id root@ip
```

## 常用模块

ansible-doc

``` bash
ansible-doc yum
# 获取模块

ansible-doc  -l
#列出已安装模块
```

### 基础测试模块

```bash
#ping测试
ansible all -m ping
```

### command

| 参数 | 解析 |
| -- | -- |
| chdir | 执行命令前切换目录 |
| executable | 切换shell执行,使用绝对路径 |
| free_form | 执行的Linux命令,右 `-a` 代替 |
| creates | 文件存在,则执行 |
| removes | 不存在,不执行 |

> 不支持`|管道命令`,执行单条命令+参数

```bash
ansible all -m command -a 'chdir=/dev/ ls'
```

### shell

```bash
ansible all -m shell -a ''cat /etc/passwd |grep "root"'
```

### copy

> 文件分发远程主机,支持给定内容生成文件及权限设置

| 参数 | 解析 |
| -- | -- |
| src | 本地文件或路径 |
| content |替换src,直接指定文件内容 |
| dest | 远程绝对路径 |
| backup | 文件内容改变后,在覆盖前备份为文件 |
| directory_mode | 设定权限 |
| force | 是否强制覆盖,默认覆盖 |
| others | file模块的选项 |

```bash
ansible all -m copy -a 'src=~/test dest=/ mode=666'
```

### file

> 设置文件属性,新建删除文件等

| 参数 | 解析 |
| -- | -- |
| force | 是否强制创建软链接 |
| group | 组,后加 mode |
| owner | 后加 path |
| recurse | 递归设置文件属性,后加 src,只应用于`state=link` |
| dest | 被链接路径只应用于`state=link` |
| state | 状态 |
| --directory | 如果目录不存在，就创建目录 |
| --file | 即使文件不存在，也不会被创建 |
| --link | 创建软链接 |
| --hard | 创建硬链接 |
| --touch | 如果文件不存在，则会创建一个新的文件，如果文件或目录已存在，则更新其最后修改时间 |
| --absent | 删除目录、文件或者取消链接文件 |

### fetch

> 拉取远程文件至本地

| 参数 | 解析 |
| -- | -- |
| dest | 存放目录 |
| src | 远程`文件` |

``` bash
ansible all -m fetch -a 'src=/root/hello dest=/root'
```

### script

> 使本机脚本在控制机运行

``` bash
ansible all -m script -a '/root/test.sh'
```

## 文档

+ [Ansible中文权威指南](http://www.ansible.com.cn/index.html)
+ [官网](https://www.ansible.com/)
+ [官方文档](https://docs.ansible.com/)
+ [自动化运维工具——ansible详解（一）](https://www.cnblogs.com/keerya/p/7987886.html)