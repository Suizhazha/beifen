---
title: "系统学习HTTP"
date: 2020-01-24T21:28:20+08:00
draft: false
---

### 体系化学习

1. 基础概念（必会的）
2. 如何调试（用的是 node.js，可以用 log/debugger）
3. 查资料（node.js 文档）
4. 标准制定者（HTTP 规格文档：RFC 2612 等）
5. CRM 学习法（copy，run，modify）

## HTTP 基础概念

- 请求

```
请求动词 路径/查询参数 协议名/版本
//以上是请求行
Host：域名或者IP
Accept： 接收内容
Content-type：请求体的格式
//以上为请求头

//请求头和请求体中间要加一个回车
请求体（上传的内容）

```

例如：

![](https://user-gold-cdn.xitu.io/2020/1/22/16fcdb66f6ea2883?w=338&h=381&f=png&s=50536)

Notes：

1. 请求格式主要分为：请求行，请求头，请求体。
2. 请求动词有：GET（获取）/POST（上传）/PUT/PATCH/DELETE 等。
3. 请求体在 GET 请求中一般为空。
4. 具体文档[RFC 2612 第五章](https://www.w3.org/Protocols/rfc2616/rfc2616-sec5.html)
5. 大小写随意。

- 响应

```
协议名/版本 状态码（默认200） 状态字符串
//以上为状态行
Content-Type：响应体格式（其他一般不用管）
//以上为响应头

//响应头和响应体体中间要加一个回车
响应体（即下载内容）
```

例如：

![](https://user-gold-cdn.xitu.io/2020/1/22/16fcdbba5db72f39?w=334&h=148&f=png&s=20138)

Notes：

1. 响应格式分为状态行，响应头，响应体。
2. 常见的状态码是考点。
3. 文档在[RFC 2612 第六章](https://www.w3.org/Protocols/rfc2616/rfc2616-sec5.html)
