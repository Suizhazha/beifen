---
title: "初探Vue"
date: 2020-03-09T23:30:17+08:00
draft: false
---

#### Vue 一开始采用了 MVC 框架，V（视图）是 Vue 的重点，M 和 C 则被简化。

#### Vue 将在 2020 年发布 3.0 版本，过去的 1.0 版本是 MVVM 框架，在 2.0 版本后就不是 MVVM 框架（看似是 MVVM 框架），在 3.0 版本就完全不是 MVVM 框架了。

## Vue 完整版与运行时版的区别

1. Vue 完整版文件名为 vue.js 和 vue.min.js , 后者是压缩版，取消了注释和警告，适合在生产环境下使用。
2. Vue 运行时版文件名为 vue.runtime.js 和 vue.runtime.min.js， 后者是压缩版，取消了注释和警告，适合在生成环境下使用。

#### 个人建议选择运行时版版，配合 vue-loader 和 vue 文件。

原因：

1. 保证用户体验，用户下载的 JS 文件体积更小(小 30%)，但只支持 h 函数。
2. 保证开发体验，开发者可以直接在 vue 文件里写 HTML 标签，而不用写 h 函数。
3. 累活让 vue-loader 来做，vue-loader 把 vue 文件里的 HTML 转为 h 函数。

## template 和 render 怎么用

```
//template (完整版使用)
// 需要编译器
new Vue({
  template: '<div>{{ hi }}</div>'
})
```

```
//render (完整版与运行时版使用)
// 不需要编译器
new Vue({
  render (h) {
    return h('div', this.hi)
  }
})
```

## 使用 codesandbox.io 写 Vue 代码

1. [点击进入 codesandbox.io 主页](https://codesandbox.io)
2. 在主页选择 create a Sandbox
3. 然后选择 vue 开始撸代码

#### note: Sandbox 使用的是运行时版
