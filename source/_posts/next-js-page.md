---
title: Next.js 入门笔记 | 页面路由、页面数据获取
sticky: 0
copyright: false
date: 2022-08-25 13:24:06
categories:
- Next.js
tags:
- Next.js
---

> 最近基于 Next.js 写了几个项目，记录一下该框架的使用方法。
> Next.js 是一个基于 React 的服务端渲染框架，支持 TypeScript。

本文主要记录 Next.js 的页面路由及页面数据获取。

<!-- more -->

## 页面路由

Next.js 的页面路由根据根目录下的 `pages` 文件夹的文件生成。即一个 page（页面） 就是一个从 `.js`、`.jsx`、`.ts` 或 `.tsx` 文件默认导出（`export default`）的 React 组件，每个 page（页面）都使用其文件名作为路由（route）。

例如：
如果你创建了一个命名为 `pages/about.js` 的文件并导出一个组件，则可以通过 `/about` 路径进行访问。

### 动态路由

如果你创建了一个命名为 `pages/posts/[id].js` 的文件，那么就可以通过 `posts/1`、`posts/2` 等类似的路径进行访问。

路由参数获取：

```js
import { useRouter } from 'next/router'

const Post = () => {
  const router = useRouter()
  const { id } = router.query

  return <p>Post: {id}</p>
}

export default Post
```

`query` 对象除了有 `param` 的值，还有 `query` 请求对象的值。
以 `/pages/post/[id].tsx` 为例：

| router | query|
|---|---|
| `/post/1` | `{"id": "1"}` |
| `/post/2?name=steven` | `{"id": "2", "name": "steven"}` |


如果 `param` 和 `query` 重名，`param` 将覆盖 `query`。
以 `/pages/post/[id].tsx` 为例：

| router | query|
|---|---|
| `/post/3?id=steven` | `{"id": "3"}` |


可以有多级动态路由。
以 `/pages/post/[day]/[name].tsx` 为例：

| router | query|
|---|---|
| `/post/2021-01-01/steven` | `{"day": "2021-01-01", "name": "steven"}` |


可以用 `...` 匹配多级路由。
以 `/pages/post/[...path].tsx` 为例：

| router | query |
|---|---|
| `/post/a` | `{"path": ["a"]}` |
| `/post/b/1` | `{"path": ["b", "1"]}` |


## 页面数据获取

Next.js 页面数据获取方法有两种，一是服务端数据获取，一是客户（网页）端异步获取。客户（网页）端异步获取方法和原生 React 框架的常用方法一样，但这种方式在数据爬取的时候往往只能获取页面框架代码，不利于 SEO，所以 Next.js 针对这个问题做了服务端数据获取（服务端渲染）。服务端数据获取的方法是调用 Next.js 暴露的 API，在客户端向前端服务器请求数据后，前端服务器在 Next.js 暴露的 API 对应的生命周期发送数据请求，获取后和网页代码一并返回给客户端。

### 服务端数据获取
Next.js 暴漏了三个 API 供服务端数据获取—— `getStaticProps`、
`getStaticPaths` 和 `getServerSideProps`。

| API | 触发时间 | 用途 |
|---|---|---|
| `getStaticProps` | 构建（build）时 | 在构建时固定，且后面不更改的数据。 |
| `getStaticPaths` | 构建（build）时 | 用于动态路由页面，构建时固定，且后面不再更改，需要提供路由列表。 |
| `getServerSideProps` | 向前端服务器请求数据后 | 根据路由数据向后端数据库请求数据。 |

#### getStaticProps

```ts
import { GetStaticProps, InferGetServerSidePropsType } from 'next'

export async function getStaticProps: GetStaticProps(context) {
  return {
    props: {}, // 传递到页面组件
  }
}

export default function Component( componentProps: InferGetServerSidePropsType<typeof getServerSideProps>) {
  // getStaticProps 返回值中 props 的值会挂载到 componentProps 上
}
```

#### getStaticPaths

```ts
import { GetStaticProps, GetStaticPaths, InferGetServerSidePropsType } from "next";

export const getStaticPaths: GetStaticPaths = async () => {
  return {
    paths: [
      { params: { name: "route1" } },
      //...
      { params: { name: "routen" } },
    ],
    fallback: false,
  };
};

export const getStaticProps: GetStaticProps = async (context) => {
  console.log("context.params.name:", context.params.name); // route1 或 route2 ……
  return {
    props: {}, // 传递到页面组件
  };
};

export default function Component( componentProps: InferGetServerSidePropsType<typeof getServerSideProps>) {
  // getStaticProps 返回值中 props 的值会挂载到 componentProps 上
}

```

### getServerSideProps

```ts
import { GetServerSideProps, InferGetServerSidePropsType } from 'next' //TypeScript：使用 GetServerSideProps

export async function getServerSideProps:GetServerSideProps (context) {
  return {
    props: {}, // 将作为道具传递到页面组件
  }
}

export default function Component( componentProps: InferGetServerSidePropsType<typeof getServerSideProps>)  {
  // getServerSideProps 返回值中 props 的值会挂载到 componentProps 上
}

```

### 客户（网页）端异步获取

```ts
import {useEffect} from 'react';

export default function Component()  {
  useEffect(() => {
    // 异步请求……
  }, []);

}
```

## 表单 post 请求数据接收

这里再介绍一下表单 post 请求传递数据的方法，这种方法适用于将数据从一个页面发送给另一个页面，不经过后端处理。

当某一个页面向 `/post` 页面发送表单 post 请求时，下面可实现 `/post` 页面接收请求数据。
```ts
// pages/api/request.ts

import { GetServerSidePropsContext } from 'next';

type ReqType = GetServerSidePropsContext['req'];

// 该方法旨在接收 post 请求数据
export async function handleRequestBody(req: ReqType) {
    let body = '';

    for await (const data of req) body += data;

    return Object.fromEntries(new URLSearchParams(body));
}
```

```ts
// pages/post/index.tsx

import { GetServerSideProps, InferGetServerSidePropsType } from 'next';
import { handleRequestBody } from '../api/request';

export const getServerSideProps: GetServerSideProps = async ({
    req,
    query: { id },
}) => {
    const postReq = (await handleRequestBody(req)) || {};
    // 此处可根据接收的数据做一些处理……
    return {
        props: {}, // 返回给渲染组件
    };
};

export default function Post( ComponentProps: InferGetServerSidePropsType<typeof getServerSideProps>) {
  // getServerSideProps 返回值中 props 的值会挂载到 componentProps 上
}
```


> **参考资料**
> - [Next.js 静态生成和服务器端渲染](https://www.jianshu.com/p/9172f1d560c6)
> - [getServerSideProps](https://nextjs.org/docs/basic-features/data-fetching/get-server-side-props)
> - [getStaticPaths](https://nextjs.org/docs/basic-features/data-fetching/get-static-paths)
> - [getStaticProps](https://nextjs.org/docs/basic-features/data-fetching/get-static-props)
> - [NextJS_Basics/src/pages/getStaticPaths/[name].tsx](https://github.com/maxwilsonpereira/NextJS_Basics/blob/a807090cec703d4a892d88f650b7cc75f52eacfb/src/pages/getStaticPaths/%5Bname%5D.tsx#L37)
