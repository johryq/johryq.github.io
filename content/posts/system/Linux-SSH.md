---
title: "Linux SSH"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T13:23:25+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"

---
<!--more-->

<!--markdown-->

# 一些 SSH 知识

## 基本介绍

[阮一峰的 ssh 介绍](http://www.ruanyifeng.com/blog/2011/12/ssh_remote_login.html)

---

`ssh -v user@ip`

查看详细连接过程

<!--more-->

## 操作

### 配置秘钥登录

```bash
# 生成秘钥
 ssh-keygen
 cd ~/.ssh

# 安装公钥
cat id_rsa.pub >> authorized_keys

# 给予权限
chmod 600 authorized_keys
chmod 700 ~/.ssh

# 配置sshd_config文件
PubkeyAuthentication yes
RSAAuthentication yes

PermitRootLogin no
AuthorizedKeysFile      .ssh/authorized_keys

# 秘钥登录完成后禁用密码登录
PasswordAuthentication no
ChallengeResponseAuthentication no
```

> `ssh-keygen -R domaon.com` 将指定的主机公钥指纹移出`known_hosts`文件

### 分发密钥实现免密登录

1.单个分发

```bssh
# 生成密钥
ssh-keygen

# 分发密钥
ssh-copy-id root@ip

# 配置本机免密钥登录
vim ~/.ssh/config
Host sshtest
    HostName ssh.test.com
    User user
    Port 2200
    IdentityFile ~/.ssh/id_rsa_test

ssh sshtest
```

2.批量分发脚本实现

> root用户的话注意ssh配置

host.txt

``` txt
192.168.1.1 user password
192.168.1.2 user password
```

```bash
#!/bin/bash

# expect分发密钥
pushKey(){
addr=$1
user=$2
pw=$3
/usr/bin/expect <<-EOF
set timeout 10
spawn ssh-copy-id $user@$addr
expect {
    "yes/no" { send "yes\n"; exp_continue }
    "password:" { send "$pw\n" }
}
expect eof
EOF
}           

# 本地是否有密钥
haveKey(){
if [ ! -f ~/.ssh/id_rsa ];then
 ssh-keygen -t rsa -P "" -f ~/.ssh/id_rsa
else
 echo "id_rsa has created ..."
fi
}


main(){
apt install -y expect
host=/tmp/host.txt

haveKey
while read line
  do
    # echo $line
    user=`echo $line | cut -d " " -f 2`
    ip=`echo $line | cut -d " " -f 1`
    passwd=`echo $line | cut -d " " -f 3`
    pushKey $ip $user $passwd
  done <  $host
}

main
```

## 问题

- 连接提示 `Could not load host key: /etc/ssh/ssh_host_ed25519_key`

```bash
ssh-keygen -A

service ssh restart
```

---

## 参考地址

- [解决" Could not load host key: /etc/ssh/ssh_host_ed25519_key"问题](https://www.jianshu.com/p/f2b1370d87ac)
- [Linux expect 介绍和用法](https://www.cnblogs.com/saneri/p/10819348.html)
- [ssh密钥批量分发](https://www.cnblogs.com/yizhangheka/p/11038960.html)
- [阮一峰SSH 教程](https://wangdoc.com/ssh/)
