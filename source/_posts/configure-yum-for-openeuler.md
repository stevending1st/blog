---
title: 为 openEuler 配置 yum
sticky: 0
copyright: true
date: 2021-07-11 13:13:41
description: 为 openEuler 配置 yum
categories:
- 初学者的 openEuler 之旅
tags:
- Linux
- openEuler
- yum
---


# 确认发行版

```bash
cat /etc/openEuler-release
```

显示

```bash
openEuler release 20.03 (LTS)
```

# 查询源

- 进入华为开源镜像 https://mirrors.huaweicloud.com/home
- 选择 “镜像” > “openEuler” > 继续使用
- 选择架构（参看系统安装镜像）
- 复制命令（以 `X86_64` 为例）

```bash
wget -O /etc/yum.repos.d/openEulerOS.repo https://repo.huaweicloud.com/repository/conf/openeuler_x86_64.repo
```

# 配置 yum

进入 openEuler：

- 下载 `openEulerOS.repo` 到 `/etc/yum.repos.d/` 

```bash
wget -O /etc/yum.repos.d/openEulerOS.repo https://repo.huaweicloud.com/repository/conf/openeuler_x86_64.repo
```

- 清除原有 yum 缓存

```bash
yum clean all
```

- 生成新的缓存

```bash
yum makecache
```

# 安装 vim

```bash
yum install vim -y
```

>**参考资料：**
>- [配置OpenEuler的网络yum源](https://bbs.huaweicloud.com/forum/forum.php?mod=viewthread&tid=98091#lastpost)
>- [华为云](https://mirrors.huaweicloud.com/home)
