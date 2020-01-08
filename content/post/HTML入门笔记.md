---
title: "HTML入门笔记"
date: 2020-01-01T21:59:13+08:00
draft: false
---

## 大家好，上星期在饥人谷学习了 HTML 的历史概述，语法和一些常用标签。前几天因为收拾东西回家，此笔记一直没有写完。今天整理完成后分享给大家，如有错误之处，欢迎指正！（没有奖励 😝）

---

### 首先是关于 HTML 的历史:

HTML（英文：HyperText Markup Language，中文：超文本标记语言）由英国计算机科学家 Timothy John Berners-Lee 创立，同时他也是万维网的发明者。而万维网（WWW）包括了 URL，HTML 以及 HTTP，本篇只简单介绍下 HTML。

---

### HTML 起手式

    !+tab键即可出现下图代码；

![](https://user-gold-cdn.xitu.io/2020/1/3/16f6b8a34d79cf43?w=509&h=252&f=png&s=33005)
其中`<!DOCTYPE html>`
为文档类型

`<html lang="en">`
html 标签，可改 zh-cn

而 head 标签内为看不到的元素。

`<meta charset="UTF-8" />`
字符编码

`<meta name="viewport" content="width=device-width, initial-scale=1.0" />`
为防止页面缩放，用于兼容手机。

`<meta http-equiv="X-UA-Compatible" content="ie=edge" />`
可要求 Ie 升级到最新内核（11）

`<title>Document</title>`
为标题

---

### 章节标签

- 标题 h1~h6
- 章节 section
- 文章 article
- 段落 p
- 头部 header
- 脚部 footer
- 主要 main
- 旁支 aside
- 划分 div

---

### 全局属性

- class：类(class 找元素非常不方便)，推荐：
  ![](https://user-gold-cdn.xitu.io/2020/1/3/16f6b9e46c1ea677?w=678&h=484&f=png&s=61754)

- contenteditable，可以让所有元素可编辑。`<div class="middle bordered" contenteditable>`

  note:
  要想使 style 标签可见：放置 body 内，加`style{display:block;}`
  配合 contenteditable 可被编辑样式,这是个调试技巧，可以先显示再编辑。

- hidden：隐藏，比`display：block`优先级高

- id：不到万不得已，不用要 id，因为不会报错。（唯一性会误导别人）
  简写为#xxx，js 可直接调用 id 元素，有些忌讳，新手不要用。
- style：html 的属性，不是 css 的样式，还可通过 js 设置，js 会覆盖 html 的 style（js 优先级最高，html>css）。
- tabindex：控制 tab 的顺序。（0 是最后访问，-1 是别访问）
  ![](https://user-gold-cdn.xitu.io/2020/1/3/16f6ba06008daa35?w=1032&h=102&f=png&s=33221)
- title：可在开发者模式，有代码提示。
  例：标题文字太多，想省略号隐藏。

![](https://user-gold-cdn.xitu.io/2020/1/3/16f6ba0a5c66797b?w=594&h=282&f=png&s=49546)效果为：
![](https://user-gold-cdn.xitu.io/2020/1/3/16f6ba101808df6b?w=726&h=90&f=png&s=8817)

若要显示完整内容：

![](https://user-gold-cdn.xitu.io/2020/1/3/16f6ba13b53b9899?w=736&h=174&f=png&s=43838)

---

### 默认样式（因为 css 还没出生）

查看：开发者工具，element->style->user agent stylesheet

#### css reset(清除默认样式，加自己的样式)

方方老师常用 reset![](https://user-gold-cdn.xitu.io/2020/1/3/16f6ba7cb8b2de8c?w=618&h=188&f=png&s=63122)
也可借鉴大厂源码：
开发者工具内找 h1h2h3h4…，连击 3 下复制，table 后删除。

推荐加上如下图所示代码不加会非常丑![](https://user-gold-cdn.xitu.io/2020/1/3/16f6ba41439aa9dd?w=292&h=155&f=png&s=15201)
输入 table+tab 键可快速打出下图代码：
![](https://user-gold-cdn.xitu.io/2020/1/3/16f6bb9db09ceb82?w=205&h=95&f=png&s=6087)

---

### 内容标签：

- ol：有顺序的列表，内只有 li（list item）
- ul：无顺序的列表，dl+tab 可生成所有结构
- dl：描述列表
  - dt：描述对象
  - dd：描述数据内容

* pre：保留所有空格，回车，tab（因为 tab，回车和多个空格会缩成一个空格）
* code:默认字体等宽，
  pre 配合 code 使用，效果更佳。

* hr：分割线
* br：换行

* a：超链接

  - href：网址链接
  - target：新窗口打开（国内常用）

* em：强调内容语气，默认斜体
* strong：强调内容本身，默认加粗

* quote：内联引用
* blockquote：块引用

---

## 第一次使用博客记录下学习笔记，感觉很乱，标签介绍也很简单，以后会边学习边仔细整理。
