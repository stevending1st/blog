---
title: Element UI 的 el-scrollbar（滚动条）组件
sticky: 0
copyright: true
date: 2021-03-06 01:07:15
categories:
- Element UI
tags:
- Element UI
- el-scrollbar
- Element2
---

Element UI 抽出了滚动条组件——`<el-scrollbar></el-scrollbar>`，但是没有相关文档。官方在 https://github.com/ElemeFE/element/issues/2238 有过相关回复。这里对该组件的接口总结一下。

<!-- more -->

组件结构如下：
```
        ┌──────────┐
    ┌───┼──────────┼──┬────┬─┐
    │   │          │  │    │ │
    │   │          │  │    ├─┼────►track
    │   │          │  │ ┌┐ │ │
    │   │          │  │ ││ │ │
    │   │          │  │ │┼─┼─┼────►thumb
    │   │          │  │ ││ │ │
    │   │          │  │ └┘ │ │
    │   │          │  │    │ │
    └───┼───┬──────┼──┴────┴─┘
        │   └──────┼─────────────►warp
        │          ├─────────────►view
        └──────────┘
```
warp 是可视区域，view 是内容区域，warp 之外的部分将被隐藏。
滚动条的滑块 thumb 在 track 区域滑动。

接口如下：

```js
props: {
  :native: Boolean,  // 是否使用本地，设为true则不会启用element-ui自定义的滚动条
  wrapClass: string,  // 可视区域（warp）自定义样式类
  wrapStyle: string,  // 可视区域（warp）自定义样式
  viewClass: string,  // 内容区域自定义样式类
  viewStyle: string,  // 内容区域自定义样式
  noresize: Boolean, // 如果 container 尺寸不会发生变化，最好设置它可以优化性能
  tag: {  // 生成的标签类型，默认使用 `div`标签包裹
    type: String,
    default: 'div'
  }
}
```

改变 `.el-scrollbar__wrap` 这个类的样式一定要仅改变指定想改变的滚动条，避免影响到其他组件中 `el-dropdown` 有滚动条的样式。

```CSS
// 在 common.css 中添加
.el-scrollbar__wrap{
  overflow-x: hidden;
}
```

使用案例（如果有不需要的接口可以不使用）：
在使用时要设置外层容器高度。并且要设置el-scrollbar 的高度为100% 。
```html
<template>
  <div style="height: 600px;">
    <el-scrollbar style="height: 100%;" :native="false" wrapStyle="" wrapClass="" viewClass="" viewStyle="" :noresize="false" tag="main">
      <div>
        <p v-for="(item, index) in 200" :key="index">第 {{index}} 条数据。</p>
      </div>
    </el-scrollbar>
  </div>
</template>
<!--或者-->
<template>
  <div>
    <el-scrollbar style="height: 600px;" :native="false" wrapStyle="" wrapClass="" viewClass="" viewStyle="" :noresize="false" tag="main">
      <div>
        <p v-for="(item, index) in 200" :key="index">第 {{index}} 条数据。</p>
      </div>
    </el-scrollbar>
  </div>
</template>
```


> **参考资料**
> - [element ScrollBar滚动组件源码深入分析](https://juejin.cn/post/6844903764873199630)
> - [Element-ui之ElScrollBar组件滚动条的使用](https://blog.csdn.net/zhouweihua138/article/details/80077311)
> - [Element-UI 框架 el-scrollbar 组件](https://juejin.cn/post/6844903793377673230)
> - [elementUI中的隐藏组件el-scrollbar](https://www.cnblogs.com/catherLee/p/9554802.html)
> - [遮遮掩掩的滚动条 -> el-scrollbar](https://segmentfault.com/a/1190000022890903)
