---
title: "JavaScrip历史及设计缺陷总结"
date: 2020-01-17T23:26:49+08:00
draft: false
---

### JS 的起源（始于网景）

1993 年，伊利诺伊大学厄巴纳-尚佩恩分校的国家超级电脑应用中心（NCSA）发表了 NCSA Mosaic，这是最早流行的图形接口网页浏览器，它在万维网的普及上发挥了重要作用。1994 年，一家名为 Mosaic Communications 的公司在加州芒廷维尤成立了，并雇用了许多原来的 NCSA Mosaic 开发者用来开发 Mosaic Netscape，该公司的目标是取代 NCSA Mosaic 成为世界第一的网页浏览器。第一个版本的网页浏览器 Mosaic Netscape 0.9 于 1994 年底发布。在四个月内，已经占据了四分之三的浏览器市场，并成为 1990 年代互联网的主要浏览器。为避免 NCSA 的商标所有权问题，该浏览器于同年更名为 Netscape Navigator，该公司命名为 Netscape Communications。网景预见到网络需要变得更动态。公司的创始人马克·安德森认为 HTML 需要一种胶水语言，让网页设计师和兼职程序员可以很容易地使用它来组装图片和插件之类的组件，且代码可以直接编写在网页标记中。

1995 年，网景招募了布兰登·艾克，目标是把 Scheme 语言嵌入到 Netscape Navigator 浏览器当中。但更早之前，网景已经跟昇阳合作在 Netscape Navigator 中支持 Java，这时网景内部产生激烈的争论。后来网景决定发明一种与 Java 搭配使用的辅助脚本语言并且语法上有些类似，这个决策导致排除了采用现有的语言，例如 Perl、Python、Tcl 或 Scheme。为了在其他竞争提案中捍卫 JavaScript 这个想法，公司需要有一个可以运作的原型。艾克在 1995 年 5 月仅花了十天时间就把原型设计出来了。

最初命名为 Mocha，1995 年 9 月在 Netscape Navigator 2.0 的 Beta 版中改名为 LiveScript，同年 12 月，Netscape Navigator 2.0 Beta 3 中部署时被重命名为 JavaScript，当时网景公司与昇阳电脑公司组成的开发联盟为了让这门语言搭上 Java 这个编程语言“热词”，因此将其临时改名为 JavaScript，日后这成为大众对这门语言有诸多误解的原因之一。

#### 以上资料来自维基百科

---

### JS 的设计缺陷

以下介绍参考了阮一峰的文章，链接：[Javascript 的 10 个设计缺陷](http://www.ruanyifeng.com/blog/2011/06/10_design_defects_in_javascript.html)

1.  不适合开发大型程序

    因为 Javascript 没有名称空间（namespace），很难模块化；没有如何将代码分布在多个文件的规范；允许同名函数的重复定义，后面的定义可以覆盖前面的定义，很不利于模块化加载。

2.  非常小的标准库

    因为 Javascript 提供的标准函数库非常小，只能完成一些基本操作，很多功能都不具备。

3.  null 和 undefined

    null 属于对象（object）的一种，意思是该对象为空；undefined 则是一种数据类型，表示未定义。

          typeof null; // object
          typeof undefined; // undefined

    两者非常容易混淆，但是含义完全不同，而在编程实践中，null 几乎没用，根本不应该设计它。

```
    var foo;
    alert(foo == null); // true
    alert(foo == undefined); // true
    alert(foo === null); // false
    alert(foo === undefined); // true
```

4. 全局变量难以控制

   Javascript 的全局变量，在所有模块中都是可见的；任何一个函数内部都可以生成全局变量，这大大加剧了程序的复杂性。

```
    a = 1
    (function(){
          b=2;
          alert(a);
          })(); // 1
          alert(b); //2
```

5. 自动插入行尾分号

   Javascript 的所有语句，都必须以分号结尾。但是，如果你忘记加分号，解释器并不报错，而是为你自动加上分号。有时候，这会导致一些难以发现的错误。

比如，下面这个函数根本无法达到预期的结果，返回值不是一个对象，而是 undefined。

         function(){
             return
          {
             i=1
          };
          }

原因是解释器自动在 return 语句后面加上了分号。

         function(){
             return;
         {
             i=1
         };}

6.  加号运算符

    +号作为运算符，有两个含义，可以表示数字与数字的和，也可以表示字符与字符的连接。

          alert(1+10); // 11

          alert("1"+"10"); // 110

    如果一个操作项是字符，另一个操作项是数字，则数字自动转化为字符。

          alert(1+"10"); // 110

          alert("10"+1); // 101

    这样的设计，不必要地加剧了运算的复杂性，完全可以另行设置一个字符连接的运算符。

7.  NaN

    NaN 是一种数字，表示超出了解释器的极限。它有一些很奇怪的特性：

          NaN === NaN; //false

          NaN !== NaN; //true

          alert( 1 + NaN ); // NaN

    与其设计 NaN，不如解释器直接报错，反而有利于简化程序。

8.  数组和对象的区分

由于 Javascript 的数组也属于对象（object），所以要区分一个对象到底是不是数组，相当麻烦。Douglas Crockford 的代码是这样的：

         if ( arr &&
              typeof arr === 'object' &&
              typeof arr.length === 'number' &&
              !arr.propertyIsEnumerable('length')){
              alert("arr is an array");
           }

9. == 和 ===

==用来判断两个值是否相等。当两个值类型不同时，会发生自动转换，得到的结果非常不符合直觉。

         "" == "0" // false

         0 == "" // true

         0 == "0" // true

         false == "false" // false

         false == "0" // true

         false == undefined // false

         false == null // false

         null == undefined // true

         " \t\r\n" == 0 // true

因此，推荐任何时候都使用"==="（精确判断）比较符。

10. 基本类型的包装对象

Javascript 有三种基本数据类型：字符串、数字和布尔值。它们都有相应的建构函数，可以生成字符串对象、数字对象和布尔值对象。

         new Boolean(false);
         new Number(1234);
         new String("Hello World");

与基本数据类型对应的对象类型，作用很小，造成的混淆却很大。

         alert( typeof 1234); // number

         alert( typeof new Number(1234)); // object

关于 Javascript 的更多怪异行为，请参见 Javascript Garden 和 wtfjs.com。

---

### 既然 Javascript 有缺陷，数量还不少，那么它是不是一种很糟糕的语言？有没有前途？

其实 Javascript 并不算糟糕，相反它的编程能力很强大，前途很光明。如果遵守良好的编程规范，加上第三方函数库的帮助，Javascript 的这些缺陷大部分可以回避。

Javascript 目前是网页编程的唯一语言，只要互联网继续发展，它就必然一起发展。目前，许多新项目大大扩展了它的用途，node.js 使得 Javascript 可以用于后端的服务器编程，coffeeScript 使你可以用 python 和 ruby 的语法，撰写 Javascript。
只要发布新版本的语言标准，就可以弥补这些设计缺陷。当然，标准的发布和标准的实现是两回事，上述的很多缺陷也许会一直伴随到 Javascript 存在的最后一天。
