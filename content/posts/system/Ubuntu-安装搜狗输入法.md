---
title: "Ubuntu 安装搜狗输入法"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T13:25:36+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"

---
<!--more-->

<!--markdown-->系统版本: 18.04



Linux默认输入法配置是 ****ibus**** ;

但是搜狗输入法 Linux 版是基于 ****fcitx**** 写的;



所以我们首先需要安装fcitx:

```

sudo apt install fcitx 

```



然后修改默认输入法配置!



1. 首先选择菜单栏的输入法图标

![sogou_1.png][1]

2. 根据这个修改配置的引导--点击 **确认** 即可(这张图是已经修改完的配置,可能和第一次打开看到的不一样)

![sogou_2.png][2]

3. 选择 **yes** 

![sogou_3.png][4]

4. 选择 ** fcitx** 点击 **确认** 即可

![sogou_4.png][3]

5. 下载并安装搜狗输入法Linux版

[搜狗输入法Linux版官网](https://pinyin.sogou.com/linux/)



点击下载的包安装或者 `sudo dpkg -i sogoupinyin_版本号_amd64.deb`



6. 最后重启系统即可看到输入法

```

shutdown -r now

```



#### 参考链接



+ [Ubuntu 18.04 安装搜狗输入法折腾记](https://www.jianshu.com/p/01ffac435ea8)

+ [搜狗官方文档](https://pinyin.sogou.com/linux/help.php)

  [1]: https://www.johryq.top/usr/uploads/2020/11/1698522111.png

  [2]: https://www.johryq.top/usr/uploads/2020/11/1613950862.png

  [3]: https://www.johryq.top/usr/uploads/2020/11/2543580736.png

  [4]: https://www.johryq.top/usr/uploads/2020/11/2943639164.png