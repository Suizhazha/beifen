---
title: "AJAX原理"
date: 2020-02-20T16:06:02+08:00
draft: false
---

AJAX：Asynchronous JavaScript and XML 异步的 JavaScript 与 XML 技术），即使用 JS 发送请求和接收响应。

### AJAX 原理

- 步骤：
  1. 创建 HttpRequest 对象(XMLHttpRequest())
  2. 调用对象的 open 方法（查看 mdn,只用 method 和 url，后面的参数都不用）
  3. 监听对象的 onload 和 onerror 事件
     - 专业前端会改用 onreadystatechange
     - 在事件处理函数里操作相应文件内容
  4. 调用对象的 send 方法(发送请求)

例如：

加载 HTML

```
    getHTML.onclick = () => {
    const request = new XMLHttpRequest()
    request.open('GET', '/1.html')//read state = 1
    request.onreadystatechange = () => {

        //2xx一般表示成功
        if (request.readyState === 4) {
            if (request.status >= 200 && request.status < 300) {

            // 创建一个div标签
                const div = document.createElement("div");

               // 填写div内容
                div.innerHTML = request.response;

                // 插入body中
                 document.body.appendChild(div);
                 } else {
                     alert("加载1.html失败");
                     }
             }
      }
     request.send()//read state = 2
}
```

### 解析方法：

- 得到 CSS 后生成 style 标签
- 得到 JS 后生成 script 标签
- 得到 HTML 后使用 innerHTML 和 DOM API
- 得到 XML 后使用 responseXML 和 DOM API
- 不同类型数据有不同的解析方式

### 总结：

- HTTP 可以装 HTML,CSS,JS,XML,JSON 等等。
- 设置正确的 Content-Type。
- 知道如何解析这些内容，就可以使用这些内容。

### [完整加载代码，请点击此链接](https://github.com/Suizhazha/AJAX-demo-1)
