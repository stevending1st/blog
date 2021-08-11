---
title: Windows 环境下在 VSCode 中使用 Git Bash 终端
sticky: 0
copyright: false
date: 2021-08-11 20:50:42
categories:
- 生产环境
tags:
- Git Bash
- 生产环境
- VSCode
---

目前，想要在 Windows 环境下使用 Bash shell，似乎 Git Bash 是最佳选择，也是唯一选择。但是之前的配置教程大多伴随 VSCode 升级而失效，这里将踩坑的经验记录一下。

<!-- more -->

## 安装 Git Bash 和 VSCode

想要安装 Git Bash 只需安装 [Git](https://git-scm.com/download/win) 即可，安装过程略。

## 寻找 Git Bash 的 bin 目录地址

在本地找到 Git 安装的目录，根目录下有一个 `bin` 文件夹，`bin` 文件夹下有一个 `bash.exe` 文件，该 `bash.exe` 文件的绝对路径即为所寻找的目录地址。

> **注意：** 在 Git 安装的根目录下有一个 `git-bash.exe` 文件，如果下面配置采用该文件的绝对路径，则启动终端时会另外启动一个 Git Bash 窗口。

## 为 VSCode 配置 Git Bash 终端

进入 VSCode > “管理” > “设置”（setting）：

搜索 `terminal.integrated.profiles.windows`，点击 `在 setting.json 中编辑`（这里以 Git Bash 的 bin 路径为 `C:\Program Files\Git\bin\bash.exe` 为例）：

```diff setting.json
        "terminal.integrated.profiles.windows": {
            "PowerShell": {
                "source": "PowerShell",
                "icon": "terminal-powershell"
            },
+           "Git-Bash": {
+                "path": "C:\\Program Files\\Git\\bin\\bash.exe"
+            },
         },
```

保存文件，重启即生效。

## 将 Git Bash 设为 VSCode 的默认终端（可选）

在上述文件 `setting.json` 文件增加 `"terminal.integrated.defaultProfile.windows": "Git-Bash"`：

```diff 
        "terminal.integrated.profiles.windows": {
            "PowerShell": {
                "source": "PowerShell",
                "icon": "terminal-powershell"
            },
            "Git-Bash": {
                "path": "C:\\Program Files\\Git\\bin\\bash.exe"
            },
        },
+       "terminal.integrated.defaultProfile.windows": "Git-Bash",
```

保存文件，重启即生效。
