---
title: "JS变量声明，数据类型和类型转换"
date: 2020-01-26T21:00:42+08:00
draft: false
---

## 推荐阅读：《我用了两个月的时间才理解 let》

## 变量声明

三种声明方式：

1. var a = 1

   var 过时，不好用。

2. let a = 1

   let 新的，更合理，用于变量声明。

3. const a = 1

   const 声明必须赋值，不可更改，用于常量声明。

### let 声明：

- 遵循块作用域，使用范围不超过{}。
- 不能重复声明。
- 可以赋值也可不赋值。
- 先声明后使用，否则报错。
- 全局声明的 let 变量，不会变成 window 的属性，但是 var 可以。
- for 循环配合 let 有奇效（面试题）。

### const 声明：

- 规则几乎跟 let 一样。
- 声明时就要赋值，且赋值后不能更改（只读变量，即常量）。
- 无法和 for 配合，因为值不可改。

### note：变量声明的时候，既指定了值，也指定了类型。

## JS 数据类型

- 数字 number：
  64 位浮点数存储一个 number，其中符号占 1 位，指数占 11 位（-1023~1024），有效数字占 52 位（省略开头的 1）。

  note：正 0，负 0 和 0 是不一样的。

![](https://user-gold-cdn.xitu.io/2020/1/26/16fe17d7a0e30f31?w=214&h=196&f=png&s=21429)

- 字符串 string：阉割版 UTF8

  - 单引号''
  - 双引号""
  - 反引号``(es6)

  note:

1.  引号不属于字符串的一部分，例如：
    'it's ok'只表示 it 就结束，而

```
'it/'s ok'  //转义,表示it's ok
"it's ok"
`it's ok`用反引号`来引用，万能
```

    ```
    \' 表示'
    \" 表示"
    \\ 表示/
    \n 表示换行
    \r 表示回车
    \t 表示Tab制表符
    \uFFFF 表示对应的Unicode字符
    \xFF表示前256个Unicode字符
    ```

2.  想在字符串里打会出，可以使用反引号+内容+回车+反引号.
3.  ' '字符串长度为 1，空字符串和空格字符串不同。
4.  UTF-8 是 Unicode 的一种存储规则，也叫字符编码规则。

note：数字和字符串

- 功能不同：

  1. 数字能加减乘除，字符串不行。
  2. 字符串可以表示电话号码，数字不行。

- 存储形式不同:
  1. 数字：以 64 位浮点数的形式储存。
  2. 字符串：以 UTF8 形式储存。
- 布尔 bool： if...else...
  - ture：1==1，4>3 等等。
  - false：！value，1==2 等等。
  - 5 个 falsy 值（相当于 false 但又不是 false 的值）：undefined，null，0，NaN 和''。
- 符号 symbol：用的很少。
- 空 undefined 和空 null：JS 独创，没有本质区别。

1. 若一个变量声明了，但无赋值，则默认为 undefined 默认。
2. 而一个函数如果没写 return，则返回值默认为 undefined。
3. 有人代码习惯上，非对象的空值为 undefined，对象的空值为 null。

- 对象 object：下一篇单独发布。

note：

1. 数组，函数和日期不是数据类型。
2. 数组，函数和日期属于 object。
3. 四基两空一对象。
4. undefined，null，number，string，bool，symbol 为简单类型，object 为复杂类型。
5. 数据类型大小写无所谓。

## 类型转换

- number=>string

  - String(n)
  - n+''

- string=>number

  - Number（s）
  - s - 0
  - +s
  - parseInt（s）
  - parseFloat（s）

- x=>bool
  - Boolean(1)
  - !!1
- x=>string - x.toString

  note：js 的 bug
  ![](https://user-gold-cdn.xitu.io/2020/1/26/16fe1d7b91411efe?w=553&h=233&f=png&s=44029)

## JS 的奇葩

可查看 JS 的秘密花园
