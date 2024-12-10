---
title: "typecho-change-theme2"
date: 2024-12-04T08:24:21+08:00
lastmod: 2024-12-04T08:24:21+08:00
draft: false
keywords: []
description: ""
tags: ['typecho theme','tstrap']
categories: ['blog']
author: "2332334"

---
<!--more-->

<!--markdown-->
# 修改Tstrap主题

难顶,今天一点睡觉迷迷糊糊睡到4点睡不着了,只好起来继续做笔记:

正在使用的该款主题使用的 `bootstrap`,他的默认 `table` 标签没有边框!  

然后昨天写的那几篇就很难看,想着给加个边框!

修改如下:

在 *footer.php* 中添加 js 实现的

``` JavaScript

<script>

    $(document).ready(function() {

      var that = $(".jumbotron").find("table");

      for (var i = 0; i < that.length; i++) {

        that.eq(i).addClass("table table-bordered");

      }

    });

  </script>

```

后面应该会一直使用[这个主题](https://github.com/GongZhengke/Tstrap)并进行自定义,更新[GitHub地址](https://github.com/johryq/Tstrap)

改完花了1-2h,有点菜啊!继续做笔记!

## 参考链接

+ [JQ,js给所有table元素标签添加样式类，并且外面再套一个div](https://blog.csdn.net/cplvfx/article/details/107234527)
