---
title: "CSS基础"
date: 2020-01-06T16:40:06+08:00
draft: false
toc: false
---

## 今天在谷里学习了 css 基础知识，结合维基百科和 mdn，写下此博客跟大家分享，如有错误之处，欢迎指正（没有奖励 😝）。

## 目录：

- css 历史
- 体系化学习
- 文档流
- 盒模型

---

### css 历史

css：中文为层叠样式表（又称串样式列表、级联样式表、串接样式表、阶层式样式表）是一种用来为结构化文档（如 HTML 文档或 XML 应用）添加样式（字体、间距和颜色等）的计算机语言，由 W3C 定义和维护。当前使用最广泛的版本是 CSS2.1，为 W3C 的推荐标准。CSS3 现在已被大部分现代浏览器支持，而下一版的 CSS4 仍在开发中。1994 年，哈肯·维姆·莱提出了 CSS 的最初建议。

层叠:

- 样式层叠：可以多次对同一选择器进行样式声明。
- 选择器层叠：可以用不同选择器对同一个元素进行样式声明。
- 文件层叠：可以用多个文件进行层叠。

note：这些特性使得 css 极度灵活，也为 css 被吐槽留下了隐患。

### 目前 CSS2.1 为使用最广泛的版本（IE 支持），CSS3 为最新版本（IE8 部分支持）。

使用 caniuse.com 检查各种浏览器支持哪些特性。

---

### 体系化学习

#### 怎样学习一门语言：

- 语法（怎样写代码）

  - 语法 1：样式语法

          选择器{
            属性名:属性值;
            /*注释*/
           }

    Notes：

    1. 所有符号都是英文符号。
    2. 区分大小写。
    3. 没有//注释
    4. 最后一个分号可省略，但建议不要省略。
    5. 任何一个地方写错了，都不会报错，浏览器会忽略。
    6. 若想知道写错，

  - 语法 2:@语法

           @charset "UTF-8";
           @import url(css路径);
           @media (min-width: 100px)and (max-width:200px){
              语法1
              }

    Notes:

    1. @charset 必须放在第一行。
    2. 前两个@语法都必须以;结尾。
    3. @media 语法以后在讲。
    4. charset 是字符集的意思，但 UTF-8 是字符编码 encoding，为历史遗留问题。

- 调试（查找代码错误）

  1.  https://jigsaw.w3.org/css-validator/将代码粘贴上去即可，不推荐
  2.  vscode 颜色报错，位置不大准。
  3.  WebStorm 看颜色，位置准确。
  4.  Chrome 开发者工具看警告。

          1. 找到标签
          2. 是否有选择器
          3. 样式是否被划掉
          4. 样式是否被警告

5.  Border 调试法：

        1. 找到怀疑元素
        2. 给该元素加一个border
        3. 若border没生效，说明选择器错了或语法错了
        4. 若border生效了，看看边界是否符合预期
        5. bug解决了删除border

    note：

    CSS 的 border 调试法相当于 JS 的 log 调试法。

- 查资料
  1.  mdn
  2.  css tricks
  3.  张鑫旭博客
- 标准制定者 w3c
  1. all css specifications
  2. css2.1 中文版

#### 如何学

- 抄文档，抄老师
- 在自己电脑上运行
- 加入自己的想法，重新运行并调试。

---

### 文档流

- 流动方向

  - inline 元素从左到右，到达最右边才会换行，字节会断开。
  - block 元素从上到下，每一个都另起一行。
  - inline-block 元素也是从左到右，字节不会断开。

- 宽度

  - inline 元素默认宽度为内部 inline 元素的和，inline 元素内不能存在 block 元素，不能用 width 指定，白写。
  - block 元素默认自动计算宽度，不是也不能写 width:100%;，会出 bug，一般 width 用 px 或者 em 指定。
  - inline-block 元素结合两者特点，宽度默认跟 inline 元素一样，但可用 width 指定。

- 高度
  - inline 元素高度由 line-height 间接决定，与 height，padding 无关。
  - block 元素高度由内部文档流元素决定，
    可以设置 height。
  - inline-block 元素跟 block 元素基本类似，可以设置 height。
- overflow
  overflow 还可设置 overflow-x 和 overflow-y。
  - visibl：默认值。内容不会被剪裁，可以呈现在元素框之外。
  - hidden：内容将被剪裁以适合填充框。 不提供滚动条。
  - scroll：内容将被剪裁以适合填充框。 浏览器显示滚动条，无论是否实际剪切了任何内容。（这可以防止滚动条在内容更改时出现或消失。）打印机仍可能打印溢出的内容。
  - auto：如果内容适合填充框内部，则看起来与可见内容相同。如果内容溢出，桌面浏览器会提供滚动条。
- 脱离文档流

      ![](https://user-gold-cdn.xitu.io/2020/1/7/16f7ed138d0d84fe?w=540&h=307&f=png&s=49695)

  或

      ![](https://user-gold-cdn.xitu.io/2020/1/7/16f7ed38d08b9283?w=533&h=349&f=png&s=52145)

  效果为：
  ![](https://user-gold-cdn.xitu.io/2020/1/7/16f7ed1f8ecf0104?w=272&h=80&f=png&s=5398)

---

### 盒模型

CSS 盒模型有两种，一种是 content-box（内容盒） 一种是 border-box（边框盒）。

content-box 的宽度 width 表示内容区宽度，不包含 padding 和 border；
而 border-box 的宽度 width 表示内容区 + padding + border 的总和。
一般优先使用后者（border-box）。

即下图：
![](https://user-gold-cdn.xitu.io/2020/1/7/16f7ee12704336c8?w=793&h=396&f=png&s=80174)

### margin 合并：

- 两个孩子之间的上下 margin 会合并：
  ![](https://user-gold-cdn.xitu.io/2020/1/7/16f7eed63dee59b9?w=812&h=354&f=png&s=70930)
  css 要求 margin 不用分两个单独写，直接合并就好。
  ![](https://user-gold-cdn.xitu.io/2020/1/7/16f7eef242913a14?w=811&h=446&f=png&s=69168)

- 第一个孩子和最后一个孩子的上下 margin，可以和他们的父母合并：
  ![](https://user-gold-cdn.xitu.io/2020/1/7/16f7fcb7e48d3d64?w=1127&h=588&f=png&s=132611)
