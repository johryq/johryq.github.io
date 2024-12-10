---
title: "Linux 资源管理"
date: 2021-11-08T19:58:55+08:00
lastmod: 2024-12-04T11:03:58+08:00
draft: false
keywords: []
description: ""
tags: []
categories: []
author: "2332334"

---
<!--more-->

<!--markdown-->### Console

主要命令 `top` 的参数解析:

| 参数 | 解释 |

|---|---|

| top | 显示进程信息,默认交谈式指令列(interactive command) |

| -d [时间,秒] | 显示更新速度,交谈式按 `s` 更改 |

| ~~-q~~ | ~~无延迟显示(测试无法使用,应该为默认模式)~~ |

| -i | 不显示闲置(idle)和无用(zombie)进程 |

| -u [用户名] | 只显示该用户相关信息 |

| -p [UID] | 显示该进程相关信息 |

| -c | 显示完整命令(路径与名称) |

| -S | 累积模式 |

| -s | 安全模式(取消交谈式指令) |

| -n [次数n] | 更新 `n` 此后停止 |

| -b | 批次档模式,与 `n` 配合输出到文件中,Example: `top -bn 1 >>top.log` |

---

![top.png][1]

图中参数解释：

| 行数 | 包含信息 |

|---|---|

| 第一行 | 系统整体统计信息 |

| &nbsp; | 当前时间 |

| &nbsp; | 运行时间 `up` |

| &nbsp; | 登录用户数 |

| &nbsp; | 系统负载,任务队列平均长度 (三个值分别为 1min; 5min; 15min 到现在的平均值) |

| 第二行 | `Tasks`(任务),进程信息 |

| &nbsp; | `total`,进程总数 |

| &nbsp; | `running`,运行中进程数 |

| &nbsp; | `sleeping`,休眠 |

| &nbsp; | `stopped`,停止 |

| &nbsp; | `zombie`,僵尸进程 |

| 第三行 | CPU信息(百分比) |

| &nbsp; | `us`,用户空间占CPU百分比 |

| &nbsp; | `sy`,内核 |

| &nbsp; | `ni`,用户进程内改变优先级的进程 |

| &nbsp; | `id`,空闲 |

| &nbsp; | `wa`,等待输入输出(缓存) |

| &nbsp; | `hi`,硬中断(Hardware IRQ) |

| &nbsp; | `si`,软中断(Software Interrupts) |

| 第三行 | `mem`,物理内存 |

| 第四行 | `swap`,交换区 |

---

top中交互式指令:

| 按键 | 解析 |

|---|---|

| <kbd>1</kbd> | 监控每个逻辑CPU状况 |

| <kbd>b</kbd> | 视图加亮 |

| <kbd>shift</kbd> + <kbd>></kbd> / <kbd><</kbd> | 按CPU占用排序 |

| <kbd>f</kbd> | 编辑top显示视图字段 |

---

### Gui or web

#### Centos

这个桌面的我不太清楚,但是知道可以使用 `cockpit`,具体安装方法如下:

```

sudo yum install cockpit

systemctl start cockpit.socket

systemctl enable --now cockpit.socket

```

如开启了防火墙,执行以下:

```

firewall-cmd --add-service=cockpit --permanent

firewall-cmd --reload

```

之后就可以通过本机IP的`9090`端口进行访问了

#### Ubuntu

桌面自带有资源管理器,没有请执行以下命令安装:

```

sudo apt-get install gnome-system-monitor

gnome-system-monitor

```

软件截图

![top-u-resource.png][6]

---

### 参考地址

+ [菜鸟教程-top命令][2]

+ [linux TOP命令详解 top -b -n 12000 >1.log][3]

+ [Linux中top命令参数详解][4]

+ [如何在 CentOS 8 中安装 Cockpit Web 控制台][5]

  [1]: https://www.johryq.top/usr/uploads/2020/11/66954069.png

  [2]:https://www.runoob.com/linux/linux-comm-top.html

  [3]:https://blog.csdn.net/mp624183768/article/details/76175751

  [4]:https://blog.csdn.net/yjclsx/article/details/81508455

  [5]:https://www.linuxidc.com/Linux/2019-10/161221.htm

  [6]: https://www.johryq.top/usr/uploads/2020/11/2546993157.png
