---
title: "JavaScript对象"
date: 2020-01-27T21:13:53+08:00
draft: false
---

## 对象 object

唯一复杂数据类型

- 定义

  - 无序的数据集合
  - 键值对（name 是键，frank 是值，组成了一对键值对）的集合

- 写法

  ```
  1. let obj={'name':'frank','age':18} //name，age 只能是字符串，就算引号删掉，也还是字符串

  2. let obj=new Object({name':'frank'}) //正规写法，上面是简单写法

  3. console.log({'name':'frank','age':18}) //匿名字符串
  ```

- notes：

  - 键名 key 是字符串，不是标识符（标识符不能以数字开头的，键名可以用数字），可以包含任意字符（空字符串、空格字符串也合法）
  - 引号可省略，省略之后只能写标识符，但中文、空格需要加引号。
  - 就算引号省略了，键名也还是字符串！
  - 每一个 key 都是对象的属性名，name 是属性名，每一个 value 都是对象的属性值，frank 是属性值。

- 奇怪的属性名

所有属性名会自动变成字符串

```
 let obj={
   1:'a',
   3.2:'b',
   1e2:true,
   1e-2:true,
   .234:true,
   0xFF:true
 }
 Object.key(obj)
 =>["1","100","255","3.2","0.01","0.234"]
 //Object.key(obj)为打出所有的键名（key）
```

- 变量做属性名

![](https://user-gold-cdn.xitu.io/2020/1/26/16fe22aca74fd8bd?w=323&h=416&f=png&s=41500)

#### notes：

1. 使用变量的值作为 key，需要加[]。
2. 不加[]的属性名会自动变成字符串。
3. 值如果不是字符串，则自动变成字符串。

## 对象的隐藏属性：

JS 中每一个对象都有一个隐藏属性,这个隐藏属性储存着其共有属性组成的对象的地址,这个共有属性组成的对象叫做原型,即隐藏属性储存着原型的地址。例如：

![](https://user-gold-cdn.xitu.io/2020/1/26/16fe2336d606fb73?w=516&h=470&f=png&s=146450)

可以使用 obj 访问那些共有属性:

![](https://user-gold-cdn.xitu.io/2020/1/26/16fe2346a47fe9af?w=292&h=220&f=png&s=31287)

note：除了字符串，，symbol 也能做属性名，但目前用不到，迭代是会用。

```
let a=symbol()
let obj={[a]:'Hello'}
```

---

## 增删改查

- 删除属性

  - delete obj.xxx 或 delete obj['xxx']

  Notes：

  1. 区分属性值为 undefined 和不含属性名。

  2. 使用`'属性名' in obj`可以查看不管是自身还是共有的属性是否存在。

  3. delete 只能删属性，不能删除对象。

- 查看属性

      - 查看自身所有属性

  `Object.keys(obj)` - 查看自身所有值：
  `Object.values(obj)` - 查看自身所有属性和值：
  `obj`或`Object.entries(obj)` - 查看自身属性和共有属性
  `console.dir(obj)` - 也可依次用出 `obj.__xxx__`查看共有属性 - 查看单个属性： 1. 中括号语法：`obj['key']` 2. 点语法：`obj.key` 3. 错误语法：`obj[key] // 变量 key 值一般不为'key'`

      Q：如何判断一个属性是自身的还是共有的

      A：obj.hasOwnProperty('toString')

note：对象的原型也是对象，而原型（对象的根）的原型，值为 null。

- 修改或增加属性

  - 直接赋值

```
let obj={name:'frank'} // name是字符串
obj.name='frank' // name是字符串
obj['name']='frank'
obj['na'+'me']='frank'
let key='name';obj[key]='frank'
let key='name';obj.key='frank' // 错误，因为obj.key等价于obj['key']
obj[name]='frank' // 错误，因为name值不确定
```

- 批量赋值(ES6 新出的 API)  
   `Object.assign(obj,{age:18,gender:'man'})`

  - 修改或者增加共有属性

  无法通过自身修改或增加共有属性

  ```
  let obj={},obj2={} // 共有 toString
  obj.toString='xxx'//只会在改 obj 自身属性
  obj2.toString //还是在原型上
  ```

  若非要修改或增加原型上的属性

  ```
  obj.__proto__.toString='xxx' // 不推荐用__proto__
  Object.prototype.toString='xxx'
  //一般来说，永远不要修改原型，会引起很多问题，比如代码崩溃，代码异常
  ```

  - 修改隐藏属性:

  不推荐使用 proto

  ```
  let obj={name:'frank'}
  let obj2={name:'jack'}
  let common={kind:'human'}
  obj.__proto__=common
  obj2.__proto__=common
  ```

  推荐使用 Object.create

  ```
  let obj=Object.create(common)
  obj.name='frank'
  let obj=Object.create(common)
  obj2.name='suixin'
  ```
