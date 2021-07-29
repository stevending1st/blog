---
title: 实现 new 关键字
sticky: 0
copyright: true
date: 2021-07-29 16:41:08
categories:
- JavaScript 底层原理
tags:
- javaScript
- new
- Object
- 对象
---

> 之前的笔记，整理一下有关 `new` 的原理。

<!-- more -->

# 执行 `new` 时发生了什么

1. 创建一个空的 JavaScript 对象（即 `{}`）；
2. 将新对象的 `__proto__` 属性指向构造函数的原型对象（`prototype`）；
3. 将步骤 1 新创建的对象作为 `this` 的上下文，并传入参数 ；
4. 如果该函数没有返回对象，则返回 `this`。

关于上面的第 4 点请看示例一、二：

示例一：

```js
function test() {
  const a = 5;
  return [1,2,3]; //返回对象，将 [1,2,3] 替换成其他对象的数据也将返回对象
}
new test();  // [1, 2, 3]
```

示例二：

```js
function test() {
  const a = 5;
  return 1; //返回非对象，将 1 替换成其他非对象的数据也是同一结果
}
new test();  // FireFox: Object{}; Chrom: test{}
```

# 实现 `new`

```js
function newFn(classFn, ...args) {
  // 创建一个空的 JavaScript 对象
  const obj = {};
  // 将新对象的 __proto__ 属性指向构造函数的原型对象
  Object.setPrototypeOf(obj,classFn.prototype);
  // 将步骤1新创建的对象作为 this 的上下文，并传入参数
  let arg = [...args]; // 将参数对象转为数组
  let result = classFn.apply(obj, arg);
  // 如果该函数没有返回对象，则返回 this
  return typeof result === "object" ? result : obj;
}
```

测试：

```js
// 用例一：
function test() {
  const a = 5;
  return [1,2,3]; //返回对象，将 [1,2,3] 替换成其他对象的数据也将返回对象
}
const obj =  newFn(test); 
console.log(obj); // [1, 2, 3]

// 用例二：
function test() {
  const a = 5;
  return 1; //返回非对象，将 1 替换成其他非对象的数据也是同一结果
}
const obj =  newFn(test);
console.log(obj);  // Object{}

// 用例三：
function test(arg1) {
  this.a = arg1;
}
test.prototype.say = function(){
  console.log(this.a)
}
const obj =  newFn(test, 5);
console.log(obj); //Object {a: 5}
obj.say();  // 5
```

>**参考文献：**
>- [new 到底都做了什么事情](https://juejin.cn/post/6950673570196357156)
>- [JavaScript 中 new 的用处及其实现](https://www.cnblogs.com/yangrenmu/p/10628244.html)
>- MDN 相关内容
