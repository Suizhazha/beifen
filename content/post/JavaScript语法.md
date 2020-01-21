---
title: "JavaScript语法"
date: 2020-01-20T23:54:36+08:00
draft: false
---

### 推荐书籍：

- 你不知道的 JavaScript（先买上卷，适合进阶）
- 阮一峰的免费教程
- 网道

### 表达式

- 1+2 表达式的值为 3。
- add(1,2）表达式的值为函数的返回值。

  note：值和返回值不一样，只有函数才有返回值。

- console.log 表达式的值为函数本身。
- console.log(3)表达式的值为 undefined，但会打印出来 3。

### 语句

- var a = 1 是一个语句

Notes：

- 表达式一般都有值，语句可能有值，也可能没有。
- 语句一般会改变环境（声明、赋值）。
- 上面两句并不绝对。

### JS 区分大小写，例如：

           var a和var A
           object和Object
           function和Function都是不同的含义

### 空格和回车

只要不影响断句，空格没有实际意思，回车大部分一样没有实际意思。

#### 但 return 后不能加回车，否则会返回一个 undefined！！！

### 标识符

变量名，第一个字符可以是 Unicode 字母，\$,下划线或者中文。

### 注释

/ xxx /只能注释一行，而/_ xxx _/可以注释多行。

- 不好的注释：将代码翻译成中文的注释，无用过时的注释，发泄不满的注释。
- 好的注释：踩坑的注释，奇怪的代码和 bug 注释。

### block 区块

    {
      let a = 1;
      let b = 2;
    }

常与 if，for 和 while 一起用。

---

### if...else...语句

- 语法

      if(表达式){
          语句 1
         } else {
             语句 2
              }

  Notes：

  - { }在语句只有一句的时候可以省略，不建议这样做。
  - if 语句中还可以嵌套 if else，同理 else 中也可以。

- 最推荐的写法：

  ```
  if(表达式){
    语句
  }else if(表达式){
    语句
  }else{
    语句
  }
  ```

- 次推荐的写法：

````
 function fn(){
  if(表达式){
    return 表达式
  }
  if(表达式){
    return 表达式
  }
    return 表达式
  }
  ```

### switch 语句
不推荐，容易用错。
- 语法：
````

a = 2;
switch(a){
case 1：
case 3:
console.log('单数')；
break;
case 2：
case 4：
console.log('双数')；
break；
}

```
- break：
  - 大部分时候，如果要使用switch,一定要记得使用break。
  - 少部分时候，可以利用 break。

### 问号冒号表达式
简洁版的if...else...语句
- 语法：

         表达示1？表达式2：表达式3；

### &&短路逻辑（全真才真）


`A&&B`

若AB都为真，则取B的值，若A为假，则`A&&B`为假，
并不会取 true/false。

### ||短路逻辑（一真就真）

`A||B`
若A为真，则为真。若A为假，则看B，B为真则为真，B为假则为假。
如果能写成||或者&&，就绝对不写 if ...else...语句。

***

### while循环语句

- 语法：


```

while(表达式){
语句
}

```
1. 首先判断表达式的真假。
2. 当表达式为真，执行语句，执行完再判断表达式的真假。
3. 当表达式为假，执行while后面的语句。



note：

```

var a=0.1
while(a!==1){
console.log(a)
a=a+0.1
}

```
会出现死循环，这是因为浮点数不精确造成的问题，永远到不了1。

而do...while语句用的不多，自行了解。

### for循环语句

 for是while循环的方便写法

 - 语法

       for（语句1;表达式2;语句3）{
           循环体
       }

1. 先执行语句 1
2. 然后判断表达式 2
3. 如果为真，执行循环体，然后执行语句 3（break可以跳出循环）
4. 如果为假，直接退出循环，执行后面的语句

例如：
```

for(var i=0;i<5;i++){
setTimeout(()=>{
console.log(i)
})
}

```
因为setTimeout是过一会时间才打印，过一会，for已经执行完，这时i=5，所以，会打印出五个5。而将var改成let的话，就会打出01234。

### break 和 continue

 - break：退出所有循环

note：break 只会退出离它最近的循环，如果是多for嵌套循环，不会全退。

- continue：退出当前循环

### label 语句


```

foo:{
console.log(1);
break foo;
console.log('本行不会输出');
}
console.log(2);

```
输出 1 2
- 问：下面的东西是什么？

```

{
a:1;
}

```
答：不一个对象，a 是一个 label，它的语句就是一个 1。
```
