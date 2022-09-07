---
title: Win11 家庭版安装 Hyper-V 服务
sticky: 0
copyright: true
date: 2022-09-07 09:09:15
categories:
- 环境搭建
tags:
- 环境搭建
- Hyper-V
- Win11 家庭版
---

最近正在把旧电脑的环境逐步迁移到新电脑。目前新电脑的操作系统是 Win11 家庭版，Win11 家庭版默认未安装 Hyper-V 服务，需要手动安装并启用。操作步骤如下：

<!-- more -->

1. 新建一个文本文件，并将下面代码粘贴到文件内，并保存：
```cmd
pushd "%~dp0"
dir /b %SystemRoot%\servicing\Packages\*Hyper-V*.mum >hyper-v.txt
for /f %%i in ('findstr /i . hyper-v.txt 2^>nul') do dism /online /norestart /add-package:"%SystemRoot%\servicing\Packages\%%i"
del hyper-v.txt
Dism /online /enable-feature /featurename:Microsoft-Hyper-V-All /Limit
Access /ALL
```

2. 将步骤 1 的文本文件重命名为以 `.cmd` 为后缀的文件（如 `Hyper-V.txt`）。

3. 以管理员身份运行上述步骤制作的脚本，等待脚本运行结束，未完成前不要关机或重启。

4. 脚本运行结束后重启电脑。

5. 进入：`控制面板` -> `程序` -> `程序和功能/启用或关闭 Windows 功能`，并勾选 `Hyper-V`及其下级的 `Hyper-V 管理工具` 和 `Hyper-V 平台`，点击 `确定`，等待系统启用相关服务，按提示点击确认重启电脑。

6. 电脑重启完成即完成。

> **参考资料**
> - [Windows10 家庭版添加 Hyper-V 的方法](https://jingyan.baidu.com/article/d7130635e5678113fcf4757f.html)
