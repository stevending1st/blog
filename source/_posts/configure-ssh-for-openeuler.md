---
title: 为 openEuler 配置 SSH
sticky: 0
copyright: true
date: 2021-07-11 11:08:07
description: 为 openEuler 配置 SSH
categories:
- 初学者的 openEuler 之旅
tags:
- Linux
- openEuler
- SSH
---

# 设置网卡

设置 > 网络
设置“链接方式”：`桥接网卡`
设置“界面名称”：选择本地能联网的网卡
保存

# 进入 openEuler
执行 `ip addr`

```log
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 00:00:00:00:00:00 brd ff:ff:ff:ff:ff:ff
    inet 192.168.0.1/24 brd 192.168.0.01 scope global dynamic noprefixroute enp0s3
       valid_lft 81259sec preferred_lft 81259sec
    inet6 ::1/128 scope link noprefixroute
       valid_lft forever preferred_lft forever
```

发现虚拟机的网络接口是 `192.168.0.1`

# SSH 链接虚拟机

在本地机启动命令行工具：

```Bash
ssh <userName>@<ip>
```

显示：

```log
The authenticity of host '192.168.0.1 (192.168.0.1)' can't be established.
ECDSA key fingerprint is SHA256:xV1o/ZwaUNtEcmUmjp4nzOzpApXfXD+bnJCkl499LTw.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

输入 `yse` 或 `y`
显示：

```log
Warning: Permanently added '192.168.0.1' (ECDSA) to the list of known hosts.
Authorized users only. All activities may be monitored and reported.
root@192.168.0.1's password:
```

输入用户密码
显示：

```log
Authorized users only. All activities may be monitored and reported.
Last login: xxx xxx xx xx:xx:xx xxxx


Welcome to 4.19.90-2003.4.0.0036.oe1.x86_64

System information as of time:  xxxx年 xx月 xx日 星期x xx:xx:xx xxx

System load:    0.07
Processes:      81
Memory used:    13.2%
Swap used:      0.0%
Usage On:       9%
IP address:     192.168.0.1
Users online:   2
```

完成

> **参考资料：**
>- [SSH的使用详解](https://bbs.huaweicloud.com/forum/thread-100452-1-1.html)
