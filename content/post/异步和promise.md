---
title: "异步和promise"
date: 2020-02-18T23:25:11+08:00
draft: false
---

## 异步

- 相关解释：

  1. 若能直接拿到结果，不拿到结果不离开,就是同步。

     例如：去医院挂号，拿到号才能离开窗口。

  2. 不能直接拿到结果，则是异步。

     例如：去餐厅门口等位，可以拿到号去逛逛，而每 10 分钟去餐厅问一下，为轮询，扫码用微信接收通知，就是回调。

  3. 轮询和回调都能拿到结果，只是方式不同。

  4. 以 AJAX 为例，`request.send()`后，并不能直接拿到`request.response`,必须等到 readyState 变 4 后，浏览器才回头调用(回调)`request.onreadystatechange()`，之后才能得到`request.response`。

- 回调 callback

  写了一个函数 A，传给另一个函数 B 调用，那么函数 A 就是回调。

  例如：有的时候回调还可以传给一个对象，`request.onreadystatechange()`就是写给浏览器调用的，就是让浏览器将来回头调用一下这个函数。

  再例如：

  ```
  function f1(){}
  function f2(fn){
      fn()
  }

   f2(f1)
  //自己没有调用f1，而f2调用了f1,f1就是回调，f2为自己调用的
  ```

- 异步和回调的关系

  1. 关联：异步任务在需要在得到结果时通知 JS 来拿结果，让 JS 留一个函数地址给浏览器，异步任务完成时浏览器调用该函数地址即可，同时将结果作为参数传给该函数该函数就是写给浏览器调用的，为回调函数。
  2. 区别：异步任务需要用到回调函数来通知结果，但回调函数不一定只用在异步任务中，回调还可以用到同步任务中。

  例如：

  ```
  array.forEach(n=>console.log())
  //同步回调
  ```

- 判断同步异步

  如果一个函数返回值处于

  1. setTimeout
  2. AJAX(即 XMLHttpRequest)
  3. AddEventListener

  上述三个函数内部，那么这个函数就是异步函数。

## promise

异步任务有两个结果时，可以用一个回调接收两个参数，还可以使用两个回调，但两个方法都有问题，而 promise 正好解决了这些问题。

1. 代码更规范。
2. 容易出现回调地狱，让代码可读性更强。
3. 方便进行错误处理。

以简单的 AJAX 的封装为例：

```
ajax = (method,url,options) =>{

    //析构赋值，从options里拿出两个变量，后面直接使用
    const {success,fail} = options

    const request = new XMLHttpRequest();
    request.open(method，url);
    request.onreadystatechange = () =>{
    if (request.readyState === 4) {

        //成功就调用 success，失败则调用fail
        if (request.status < 400) {
            success.call(null,request.response)
            }else if(request.status >= 400){
                fail.call(null,request,request.status)
                 }
         }
    }
    request.send()
}//封装完成

ajax('get','/xxx',{

    //左边是function缩写，右边为箭头函数
    success(response){},fail:(request,status) =>{}
})//调用
```

使用 promise 修改：

```
ajax = (method,url,options) =>{

    //new Promise接收一个函数
    return new Promise((resolve,reject)=>{
        const {success,fail} = options//析构赋值
        const request = new XMLHttpRequest();
        request.open(method，url);
        request.onreadystatechange = () =>{
        if (request.readyState === 4) {

            //成功就调用 resolve，失败则调用reject
            if (request.status < 400) {
                resolve.call(null,request.response)
            }else if(request.status >= 400){
                reject.call(null,request)
                 }
         }
    }
    request.send()
  })
}//封装完成

ajax('get','/xxx')
    .then((response) => {}, (request)=>{})
```

1. 虽然也是回调，但不需要记 success，fail。

2. then 的第一个参数为 success，第二个参数为 fail。
3. ajax()返回了一个.then()方法的对象。

4. 背下`return new Promise((resolve,reject)=>{})`以后就理解了。

如何将一个回调的异步函数改成 promise 异步函数：

1. 首先 `return new Promise((resolve,reject)=>{...})`

   - 任务成功调用`resolve(result)`，任务失败调用`reject(error)`。
   - resolve 和 reject 会再去调用成功和失败函数。

2. 再使用.then(success,fail)传入成功和失败函数

## jQuery.ajax

优点：

1. 支持更多形式的参数
2. 支持 Promise
3. 支持功能更多

### 但现在很少使用了，专业前端都用 axios

## axios

最新的 AJAX 库，抄袭了 jQuery 的封装思路 ，[推荐方方的博客](https://juejin.im/post/5a9cddb46fb9a028bc2d3c2f)快速了解 axiosd 的用法。

- 代码示例

```
axios.get
```

- axios 高级用法

1. JSON 自动处理

   axios 发现响应的 Content-Type 是 json，就会自动调用 JSON.parse。

2. 请求拦截器

   可以在所有请求里加东西，如加查询参数。

3. 响应拦截器

   可以在所有响应里加东西，甚至改内容。

4. 可以生成不同实例（对象）

   不同实例可以设置不同配置，用于复杂场景。
