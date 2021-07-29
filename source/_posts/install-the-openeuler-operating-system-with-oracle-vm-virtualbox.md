---
title: 通过 Oracle VM VirtualBox 安装 openEuler 操作系统
sticky: 0
copyright: true
date: 2021-07-11 10:47:33
description: 使用 VirtualBox 安装 openEuler
categories:
- 初学者的 openEuler 之旅
tags:
- Linux
- VirtualBox
- openEuler
---

# 虚拟机（Oracle VM VirtualBox）

## 安装 Oracle VM VirtualBox

下载地址 https://www.oracle.com/cn/virtualization/technologies/vm/downloads/virtualbox-downloads.html?source=:ow:o:p:nav:mmddyyVirtualBoxHero_cn&intcmp=:ow:o:p:nav:mmddyyVirtualBoxHero_cn

## 下载 openEuler 镜像

下载地址 https://openeuler.org/zh/mirror/list/
下载 `XXXX.dvd.ios`

## 创建虚拟机

- 新建
- 填写虚拟电脑名称和系统类型
  其中，类型选择 `Linux`，版本选择 `Other Linux（32-bit）`
- 内存大小
  建议 `1024` MB
- 虚拟硬盘
  选择 `现在创建虚拟硬盘(C)`
- 虚拟硬盘文件类型
  选择 `VDI（VirtualBox 磁盘映像）`
- 存储在物理硬盘上
  选择 `动态分配(D)`
- 文件位置和大小
  选择位置和大小，其中建议大小 `20`G

## 配置（设置）

- 系统 > 启动顺序
  将 `光驱` 调到最前
- 存储 > 添加光驱
- 注册
  选择下载的 openEuler 镜像
- 虚拟光盘选择
  选择下载的 openEuler 镜像
- 保存配置

## 安装界面引导

- 启动
- 选择 `Test this media & install openEuler 20.03 LTS`

## 安装界面

- 选择安装位置
- 用户设置 > 设置 Root 密码
- 安装完成
- 关机

## 重置启动项
- 设置 > 存储
  删除前面选择的光驱
- 系统 > 启动顺序
  重置 `启动顺序`，删除 `光驱` 和 `软驱`

## 启动
安装完成

>**参考资料：**
>- [安装指导](https://docs.openeuler.org/zh/docs/20.03_LTS/docs/Installation/%E5%AE%89%E8%A3%85%E6%8C%87%E5%AF%BC.html)
