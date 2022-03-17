---
title: 表单元素作为搜索栏
sticky: 0
copyright: true
date: 2022-03-17 13:16:12
categories:
- HTML
tags:
- HTML
- 表单
- 搜索
---

基于表单元素的特点，可以用其作为搜索栏，而不使用 JavaScript。

<!-- more -->

在 `<form>` 中，如果有 `<button type="submit">提交</ button>`，点击可以提交到 `<form>` 指定的路径。利用这个特点，可以将其做成搜索组件。

以 `/search` 为搜索页为例：
```html
<form action="/post">
  <input name="type" value="name" type="hidden" />
  <!--默认带有参数 type=name-->
  <input name="content">
  <button type="submit">搜索</button>
</form>
```
输入 `steven`，点击“搜索”后，页面跳转到 `/search?type=name&content=steven`

> ****
> - [form](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/form)
> - [`<button>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/button#attr-formaction)
