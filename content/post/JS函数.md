---
title: "JS函数"
date: 2020-02-01T23:57:11+08:00
draft: false
---

函数是一种特殊的对象

## 定义一个函数

- 具名函数

```
function 函数名(形参1，形参2){
    语句
    return 返回值
}
```

- 匿名函数（去掉函数名）

```
let a =function(x,y){
    return x+y
}//也叫函数表达式
```

note：

```
let a =function fn(x,y){
    return x+y
}
fn(1,2)//会报错，因为fn函数在等号右边，则作用域范围只在等号右边
```

- 箭头函数

```
let f1 = x =>x*x//箭头左边为输入，右边为输出
f1(9)//输出81
```

```
let f2 = (x，y) => x*y//若箭头左边有两个输入参数，需要括号括起来
f2(8,9)//输出72
```

```
let f3 = (x，y) => {
    console.log('hi')
    return x*y
}//若箭头右边有多个语句，必须加花括号和return 返回值
```

```
let f4 = x =>({
    name:x
})//若要在箭头右边直接返回一个对象，需要加括号
```

- 构造函数（很少用）

```
let fn1 = new function('x'，'y',
    'console.log(\'hi\');
    return x*y'
)
```

所有函数都是 Function 构造出来的，包括 Object，Array，Function 都是。

## 函数自身 v 函数调用

- 函数自身

```
let fn = () =>console.log('hi')
fn//没有结果，因为fn没有执行(调用)
```

- 函数调用

```
let fn = () =>console.log('hi')
fn()//打印出hi，有圆括号才是调用
```

```
let fn = () =>console.log('hi')//fn只保存了匿名函数的地址
let fn2 = fn//地址复制给fn2
fn2()//fn和fn2都是匿名函数的引用而已
```

## 函数的要素

- 调用时机

  调用时机不同，结果不同

```
let a = 1
function fn(){
    console.log(a)
}
a = 2
fn()//打印出2
```

```
let a = 1
function fn(){
  setTimeout(() => {
    console.log(a)
  },0)
}
fn()
a = 2//先执行完程序，再打印出2
```

```
 let i= 0
 for(i = 0;i < 6;i++){
    setTimeout(() =>{
        console.log(i)
    },0)
 }//打印出6个6，而不是0，1，2，3，4，5
```

```
 for(let i = 0;i < 6;i++){
    setTimeout(() =>{
        console.log(i)
    },0)
 }//打印出0，1，2，3，4，5，因为JS在for和let一起用时会加东西，每次循环会多创建（复制）一个i（迎合新手想法）。
```

- 作用域

  - 全局变量和局部变量

  在顶级作用域声明的变量就是全局变量，window 的属性是全局变量，其他都局部变量。

  - 函数嵌套

  ```
  function f1(){
      let a = 1
      function f2(){
          let a = 2
          console.log(a)
      }
      console.log(a)
      a = 3
      f2()
  }
  f1()//打印出1，2
  ```

  当多个作用域有同名变量 a，那么查找 a 的声明时，就向上取最近的作用域（就近原则），查找 a 的过程与函数执行无关（静态作用域或词法作用域），但 a 的值和函数执行有关。

- 闭包

  ```
    function f1(){
        let a = 1
        function f2(){
            let a = 2
          function f3(){
            console.log(a)
          }
        a = 22
        f3()
    }
    console.log(a)
    a = 100
    f2()
    }
    f1()//打印出1，2
  ```

  如果一个函数用到了外部的变量，那么这个函数加这个变量就叫做闭包，如上面的 a 和 f3 组成了闭包。

- 形式参数

```
function add(x,y){
    return x+y
}//x和y为形参，因为不是实际的参数
add(1,2)//调用add时，1和2为实参，会被赋值给 x，y
```

```
function add(){
    var x = arguments[]
    var y = arguments[]
    return x+y
}//形参其实可认为是变量声明
```

- 返回值

每个函数都有返回值

```
function hi(){
    console.log('hi')
}
hi()//返回值为undefined，因为没写return
```

```
function hi(){
    return console.log('hi')
}
hi()//返回值为console.log('hi')的值，即undefined,只是打印了hi
```

函数执行完后才会返回，只有函数才有返回值。

- 调用栈

1. JS 引擎在调用一个函数前，需要把函数所在的环境 push 到一个数组里，数组即为调用栈。
2. 等函数执行完后，就会把环境 pop 出来。
3. 然后 return 到之前的环境，继续执行后续代码。

   - 递归函数

     1. 阶乘

        ```
        function f(n){
            return n === 1 ? 1 : n*f(n-1)
        }
        f(100)//压100次栈
        ```

     2. 递归的调用栈最长为

        Chrome：12578

        Firefox：26773

        Node：12536

     3. 爆栈

        调用栈中压入得帧过多，程序会崩溃。

- 函数提升

```
function fn(){}
```

不管将具名函数声明在哪，都会跑到第一行。

```
let fn = function(){}//为赋值，右边的匿名函数声明不会提升到第一行
```

- **arguments(箭头函数没有)**

伪数组

```
Array.from()//可以将伪数组变成数组
```

- **this(箭头函数没有)**
  如果不给任何条件，this 默认指向 window，如果传的不是对象，JS 会自动封装成对象。

  - 传 this

  ```
  fn.call(xxx,1,2,3)//传this或arguments
  ```

  如果非要传数字，不想自动封装成对象

  ```
  function fn(){
      'use strict'
      console.log('this:'+this)
  }
  ```

  this 是一个隐藏参数， arguments 是普通参数。

  - 假如没有 this

    ```
    let person = {
        name: 'frank',
        sayHi(){
            console.log(`你好，我叫` + person.name)
        }
    }
    //可以直接保存对象地址的变量获取'name',简称引用
    ```

    1. 如果 person 改名了，sayHi 函数就挂了。
    2. 或者 sayHi 函数有可能在另一个文件里。
    3. 而 JS 中 person.sayHi()会隐式地 person 作为 this 传给 sayHi，方便 sayHi 通过 this 获取 person 对应的对象。

- 新手调用法

```
person.sayHi()
//会自动把person传到函数里，作为this
```

- 老手调用法

```
person.sayHi.call(person)
//要手动把person传到函数里，作为this
```

例如：

```
function add(x,y){
    return x+y
}
add.call(undefined,1,2)//3
```

第一个参数要作为 this，而原函数没有 this，只能用 undefined 占位，null 也可以。

再如：

```
Array.prototype.forEach2 = function(){
    console.log(this)
}


```

未完！
