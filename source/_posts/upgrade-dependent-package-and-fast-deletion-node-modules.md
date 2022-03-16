---
title: Node.js 升级依赖包和快速删除 node_modules
sticky: 0
copyright: true
date: 2021-01-22 11:22:31
categories:
- Node.js
tags:
- Node.js
- npm
- node_modules
---

很久之前的一个仓库，原本不想维护了，GitHub 经常发送安全警告，主要是 npm 依赖版本过低，这次想升级一下 npm 的依赖。记录一下方法。

<!-- more -->

## 查询版本可更新的版本
可以安装 npm-check-updates 模块：
```bash
npm install -g npm-check-updates
```
可以执行下面的对依赖进行检查（二选一）
```bash
ncu
# or
npm-check-updates
```
不建议用 `ncu -u` 将所有模块更新到最新版本，应选择性更新，减少应更新依赖而导致的错误。


## 执行更新
修改 package.json ，使不同模块到对应版本。
执行下面的 npm 命令
```bash
npm update xxx
```

xxx 是 指定的模块名，可以根据作用范围在后面加上 -D、-S 或 -g

package.json 更新后，可删除整个 node_modules 目录并重新安装依赖包。
```bash
npm install
```


## 快速删除 node_modules 的方法

### 方法一：使用 rimraf 模块

全局安装 rimraf 模块
```bash
npm install rimraf -g
```

通过 rimraf 模块命令来快速删除node_modules目录
```bash
rimraf node_modules
```

### 方法二：使用系统命令来删除目录
Windows：
在 cmd 窗口中进入到 node_modules 文件夹所在的路径：
```bash
rmdir /s/q node_modules
```

Linux：
```bash
rm -f /node_modules
```

> **参考资料**
> - [npm 依赖包的安装、更新、删除](https://www.jianshu.com/p/9b9166f7559c)
> - [快速删除node_modules文件夹](https://www.cnblogs.com/yulinlewis/p/10441181.html)
