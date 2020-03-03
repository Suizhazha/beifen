---
title: "初识MVC"
date: 2020-03-03T22:08:26+08:00
draft: false
---

每个模块都可以写成三个对象，分别是:

- M-Model(数据模型)负责操作所有数据。

```
const m = {
  data: {
    n: ...
  },
  create() {},
  delete() {},
  update(data) {
    ...
  },
  get() {}
}
```

- V-View(视图)负责所有 UI 界面。

```
const v = {
  html: `
  <div>
    <div>
      <span ></span>
    </div>
  </div>
`,
  render(n) {
  ...
  }
}
```

- C-Controller(控制器)负责转发请求，对请求进行处理。

```
const C={
    bindEvents(){},//绑定事件
    bindEvnetHub(){}//绑定事件中心
}
```

最后一般会把 C.init 暴露出去作为接口给其他模块调用。

### 优缺点：

1. 优点是可以实现代码的模块化管理，各个模块之间互不影响，可以恒定复杂度。
2. 缺点是当有数据改变的时候,render()时很可能是从新渲染整个模块，包括那些没有改变的元素，性能较差。

## MVC 引发的一些抽象思维

### 最小知识原则

- 一开始写代码，引入一个模块需要引入 html，css，js
- 后来引入一个模块需要引入 html，js
- 以后引入一个模块只需要引入 js 即可

#### 优缺点：

在一个页面中需要知道的知识越少越好，模块化为这一点奠定了基础。

同样这么做页面一开始其实是空白的，没有内容和样式。

#### 解决方法：

1. 添加 loading 图片
2. 添加骨架
3. 添加占位内容（加载中等等）
4. SSR 技术，但没必要

## 关于表驱动编程

表驱动方法(Table-Driven Approach)是一种使你可以在表中查找信息，而不必用很多的逻辑语句（if 或 case）来把它们找出来的方法。事实上，任何信息都可以通过表来挑选。在简单的情况下，逻辑语句往往更简单而且更直接。

简单讲是指用查表的方法获取值。 我们平时查字典就是典型的表驱动法。

### 数组中的应用：

例如可以返回每个月中天数的函数（为简单起见不考虑闰年）

- 使用 if...else...
  ```
  function iGetMonthDays(iMonth) {
    let iDays;
    if(1 == iMonth) {iDays = 31;}
    else if(2 == iMonth) {iDays = 28;}
    else if(3 == iMonth) {iDays = 31;}
    else if(4 == iMonth) {iDays = 30;}
    else if(5 == iMonth) {iDays = 31;}
    else if(6 == iMonth) {iDays = 30;}
    else if(7 == iMonth) {iDays = 31;}
    else if(8 == iMonth) {iDays = 31;}
    else if(9 == iMonth) {iDays = 30;}
    else if(10 == iMonth) {iDays = 31;}
    else if(11 == iMonth) {iDays = 30;}
    else if(12 == iMonth) {iDays = 31;}
    return iDays;
  }
  ```
- 使用表驱动(包括闰年判断)
  ```
  const monthDays = [
    [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31],
    [31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]
  ]
  function getMonthDays(month, year) {
    let isLeapYear = (year % 4 === 0) && (year % 100 !== 0 || year % 400 === 0) ? 1 : 0
    return monthDays[isLeapYear][(month - 1)];
  }
  console.log(getMonthDays(2, 2000))
  ```
- 可以看出：

  在数值不多的时候我们可以用逻辑语句(if 或 case)的方法来获取值,但随着数值的增多逻辑语句就会越来越长,此时表驱动法的优势就显现出来了。
