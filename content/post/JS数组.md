---
title: "JS数组"
date: 2020-01-31T15:10:34+08:00
draft: false
---

## JS 数组

一种特殊的对象，JS 其实没有真正的数组，只是用对象模拟数组。

- 元素的数据类型可以不同。
- 内存不一定是连续的（因为对象是随机存储的）。
- 不能通过数字下标，而是通过字符串下标。
- 意味着数组可以有任何 key。

## 创建数组

- 新建

```
let arr=[1,2,3]
let arr=new Array(1,2,3)
let arr=new Array(3)//数组长度为3
```

- 转化

```
let arr='1,2,3'
arr.split(',')//使用字符串创建数组
或
let arr='123'
arr.split('')

Array.from('123')//存在下标和length的对象，可以转化为数组
```

- 伪数组

```
let divList=document.querySelector('div')
```

notes：

1. 伪数组的原型链中没有数组的原型。
2. 没有数组共用属性的数组就是伪数组。

- 合并两个数组

```
arr1.concat(arr2)//返回新的数组，不会影响arr1，arr2的值
```

- 截取数组的一部分

```
arr1.slice(1)//从第二个元素开始截取，不会改变原数组arr1的值
arr2.slice(0)//全部截取
```

note：JS 只提供浅拷贝

## 数组中元素的增删改查

- 删除元素

  - 跟删除对象一样的方式，不推荐

  ```
  let arr=['a','b','c']
  delete arr['0']//数组长度不会变，JS设计问题
  ```

  ```
  let arr=[1,2,3,4,5]
  arr.length=1//修改length可以删除元素，但不要随便修改length
  ```

  - 正规删除元素的方式

  ```
  删除头部元素
  arr.shift()// arr值会修改，并返回被删元素
  删除尾部元素
  arr.pop()//arr值会修改，并返回被删元素
  删除中间的元素
  arr.slice(2,1)//从第三个元素开始，删除一个元素
  arr.slice(2,1,'x')//再删除位置添加一个'x'
  arr.slice(2,1,'x''y')//再删除位置添加一个'x''y'
  ```

- 查看所有元素
  - 查看数字（字符串）属性名和属性值
  ```
  for(let i=0;i<arr.length;i++){
      console.log(`${i} : ${arr[i]}`)
  }
  ```
  ```
  arr.forEach(function(item,index){
      console.log(`${index}: ${item}`)
  } )//forEach/map等原型上的函数
  ```
  - 查看单个属性
  ```
  let arr=[a,b,c]
  arr[1]
  ```
  - 索引越界
  ```
  arr[arr.length]===undefined
  arr[-1]===undefined
  ```
  越界常见报错：Cannot read property 'toString' of undefined
  意思就是你读取了 undefined 的 toString 属性，不是 toString 的 undefined。
  - 查看元素是否存在数组中
  ```
  arr.indexOf(111)//存在返回索引，否则返回-1
  ```
  - 使用条件查找元素
  ```
  arr.find(item=>item%2===0)//找第一个偶数
  ```
  - 使用条件查找元素的索引
  ```
  arr.findIndex(item=>item%2===0)//找第一个偶数的索引
  ```
- 增加数组中的元素

  - 在尾部加元素

  ```
  arr.push(newItem)
  arr.push(item1,item2)//都是修改arr，返回新长度
  ```

  - 在头部加元素

  ```
  arr.unshift(newItem)
  arr.unshift(item1,item2)
  ```

  - 在中间加元素和改元素

  ```
  arr.splice(index,0,'x')
  arr.splice(index,0,'x','y')//在index后添加'x''y'元素

  arr.splice(index,1,'x')//删除index，添加'x'
  ```

  - 反转顺序

  ```
  arr.reverse()//修改了原数组
  ```

  ### note：如何将 var s = 'abcde'反转

  ```
  1. s.split('')
  2. s.split('').reverse
  3. s.split('').reverse.join('')
  ```

  - 自定义排序

  ```
  arr.sort()//默认按从小到大顺序排序
  ```

  若数值大的需要排在前面，则需要：

  ```
  arr.sort(function(a,b){
      if(a>b){
          return -1
      }else if(a===b){
          return 0
      }else{
          return 1
      }
  })
  ```

  可以简写：

  ```
  arr.sort((a,b) => {
      return a - b
  })
  或
  arr.sort((a,b) => a - b)
  ```

## 数组变换

- map

```
let arr = [1,2,3,4,5]
arr.map(item => item*item)//返回每个元素的平方，不会改变原数组
```

- filter

```
let arr = [1,2,3,4,5]
arr.filter(item => item %2 ===0 //返回偶数，不会改变原数组
```

- reduce：数组中最强大的 API

```
let arr = [1,2,3,4,5]
arr.reduce((sum,item) =>{return sum+item },0)//返回15，不会改变原数组
```

```
let arr = [1,2,3,4,5]
arr.reduce((result,item) =>{ return result.concat(item*item) },[])//利用reduce返回元素平方，不会改变原数组
```

```
arr.reduce((result,item) =>{
  if(item %2 === 1){
      return result
  }else{
      return result.concat(item)
  }
 },[])//利用reduce返回偶数，不会改变原数组
或者
arr.reduce((result,item) =>{
  item %2 === 1  ？
    result
    ：
    return result.concat(item)
  ,[])
 或者
 let arr = [1,2,3,4,5]
arr.reduce((result,item) =>
    result.concat(item %2 === 1 ? [] :item)
,[])//炫技！！！
```
