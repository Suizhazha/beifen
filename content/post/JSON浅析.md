---
title: "JSON浅析"
date: 2020-02-20T16:06:35+08:00
draft: false
---

### [JSON 中文文档](https://www.json.org/json-zh.html),看铁轨图!!!

### 支持的数据类型

1. string：只支持双引号，不支持单引号和无引号
2. number：支持科学记数法
3. bool：true 和 false
4. null：没有 undefined
5. object
6. array

Notes:

1. 不支持函数和变量，也不支持引用。
2. 其实 JSON 就是借鉴了 JS。

### window.JSON

- JSON.parse

将符合 JSON 语法的字符串转换成 HS 对应类型的数据，若不符合 JSON 语法，则抛出一个 Error 对象，一半用 try catch 捕获错误。

- JSON.stringify

JSON.parse 的逆运算，由于 JS 数据类型比 JSON 多，所以不一定成功，失败同样抛出一个 Error 对象。
