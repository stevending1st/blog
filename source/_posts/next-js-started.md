---
title: Next.js 入门笔记 | 创建 Next.js 项目
sticky: 0
copyright: true
date: 2021-08-24 12:00:50
categories:
- Next.js
tags:
- Next.js
- create-next-app
---

> 最近基于 Next.js 写了几个项目，记录一下该框架的使用方法。
> Next.js 是一个基于 React 的服务端渲染框架，支持 TypeScript。

<!-- more -->

创建 Next.js 项目有两种方式——使用 `create-next-app` 工具创建项目，手动安装。如果是新建项目，推荐使用 `create-next-app` 工具创建项目；如果是旧项目引入 Next.js，推荐手动安装。

## 使用 `create-next-app` 工具创建项目

在创建项目的文件夹执行下面命令：

```bash
npx create-next-app
# or
yarn create next-app
```

如果需要创建 TypeScript 项目可执行：

```bash
npx create-next-app --typescript
# or
yarn create next-app --typescript
```

## 手动安装

在项目中执行：

```bash
npm install next react react-dom
# or
yarn add next react react-dom
```

如果项目中已安装 `React` 和 `ReactDom`，则无需安装。


配置 `package.json` 的 `scripts` 字段：

```json
"scripts": {
  "dev": "next dev",
  "build": "next build",
  "start": "next start",
  "lint": "next lint"
}
```

> **参考资料**
> - [Next.js 快速开始](https://www.nextjs.cn/docs/getting-started)
