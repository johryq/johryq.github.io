---
title: "Yanderify Try"
date: 2021-11-08T08:59:08+08:00
lastmod: 2024-12-04T08:59:08+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"

---
<!--more-->

<!--markdown-->最近看视频看到挺多用这个有趣功能的也想着尝试以下



搞了几小时找到了两种实现(应该一个最新版,一个老版的):



#### 新版本

1. 下载 [该项目](https://github.com/dunnousername/yanderifier/releases) 最新版本

2. 下载 [checkpoint](https://github.com/dunnousername/yanderifier/releases/download/model/checkpoint.tar)

3. 下载 [ffmpeg-win32-v3.2.4](https://github.com/imageio/imageio-binaries/raw/master/ffmpeg/ffmpeg-win32-v3.2.4.exe)

4. 将 ***ffmpeg-win32-v3.2.4*** 复制到 *** C:\\Users\(用户名)\\AppData\Local\\imageio\\ffmpeg\\ *** 下

6. 安装 [python](https://www.python.org/downloads/)

5. 运行解压后的 ***yanderify.zip*** 里面的 ***yanderify.exe*** 即可使用



#### 百度云版本

1. 该版本在百度云上找到了(没有会员下载了许久)

2. 安装python

3. ***C:\\Users\\(用户名)\\*** 该目录下创建 **.torch** 文件夹 再在里面创建 **models** 文件夹

(完整目录为: ***C:\\Users\\(用户名)\\.torch\\models***)

4. 将下载的名为插件文件夹的东西放到上面创建的目录中

5. 进入yanderify运行Start Yanderify即可使用



---



程序界面：

![程序界面][1]



**Select Video** 选择源视频文件

**Select Image** 选择你要唱歌的图片(该图片最好是宽高像素相同大小的。最最好是与源文件视频像素一致的;你可以通过右键文件的属性，详细信息查看帧宽度和帧高度来确定。)

**Select Output** 选择你要输出的文件名。

**GO** 等待进度条前进，即可生成你想要的文件。



---

参考目录

+ [yanderifier项目](https://github.com/dunnousername/yanderifier)

+ [原版安装](https://www.bilibili.com/read/cv7475087)

+ [百度云版](https://space.bilibili.com/21705749)





  [1]: https://pic2.zhimg.com/80/v2-78b39042fb80f58b72cd5c3abbe84995_720w.jpg