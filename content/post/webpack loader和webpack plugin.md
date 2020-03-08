---
title: "Webpack"
date: 2020-03-08T21:55:01+08:00
draft: false
---

## webpack loader v.s webpack plugin

- 英文翻译

1.  loader 加载器
2.  plugin 插件

- 中文翻译

1.  loader 用来加载文件，例如：
    babel loader 用来加载 JS 文件,将高版本 JS 转译成低版本的 JS，style/css loader 用来加载 CSS 文件引入到 JS 中，并转为页面中的 style 标签插入到 head 标签里。
2.  plugin 用来扩展 webpack 功能，例如：
    MiniCssExtractPlugin 将 CSS 代码提取成单独的文件，HtmlWebpackPlugin 可以自动生成 HTML 。
