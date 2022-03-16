---
title: Lodash 按需引入
sticky: 0
copyright: true
date: 2022-03-16 17:22:40
categories:
- JavaScript 库
tags:
- JavaScript 库
---

Lodash 是一个著名 JavaScript 库，为了减少包体积，往往需要按需引入。

<!-- more -->

Lodash 已经将每个函数单独打包，所以只需要单独安装每个函数包。
可以参见 https://www.npmjs.com/~jdalton 。

注意：如果是 TypeScript，需要单独安装类型包。

以 `_.chunk(array, [size=1])` 为例：
```bash
npm i --save lodash.chunk
```

如果需要 TypeScript 支持：
```bash
npm install --save @types/lodash.chunk
```
