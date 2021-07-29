---
title: 怎样在一个 div 中水平居中另一个 div
sticky: 0
copyright: false
date: 2017-11-09 10:17:04
categories:
- stackoverflow 高赞翻译
tags:
- stackoverflow
- 前端
- FE
- 布局
- 水平居中
- display
- center
---

>**译者注：** 居中问题是前端布局常见问题，受关注度较高，这次翻译的两份答案分别获赞 3000+、1000+。还有部分答案获赞量三位数，就不一一翻译了。
>**原文地址：** https://stackoverflow.com/questions/114543/how-to-horizontally-center-a-div-in-another-div

<!-- more -->

# 问题描述：

（如果可行的话，）我们怎样在一个 `<div>` 中水平居中另一个 `<div>`?

```html
<div id="outer">  
  <div id="inner">Foo foo</div>
</div>
```
(Ask by **Mosh Feu**)

# 高赞回答：

你可以给内部的 `<div>` 添加下面的 CSS 样式：

```css
#inner {
  width: 50%;
  margin: 0 auto;
}
```

当然，并不是必须设置 `width: 50%;`，任何小于子 `<div>` 的宽度都可以。`margin: 0 auto;` 才是关键。
如果你要兼容IE8及以上的浏览器，下面的方式可以更好的替代：

```css
#inner {
  display: table;
  margin: 0 auto;
}
```

它能使内部元素水平居中，而不需要设置 `width` 属性。

(Answered by **bharadhwaj**)

---

如果你不想给子 `<div>` 一个固定的宽，可以使用下面的方式：

```css
#outer {
  width: 100%;
  text-align: center;
}

#inner {
  display: inline-block;
}
```

这使得内部 `<div>` 成为可以以文本对齐为中心的内联元素。

(Answered by **Alfred**)
