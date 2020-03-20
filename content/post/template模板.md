---
title: "Template模板"
date: 2020-03-20T23:08:43+08:00
draft: false
---

Vue模板使用XML语法，使用{{}}插入表达式，使用v-html，v-on， v-bind等指令操作DOM，使用v-if，v-for等指令实现条件判断和循环。

## 展示内容

- 表达式:
    
    1. {{ object.a }}  表达式 
    2. {{ n+1 }} 任何运算(不支持 if else)
    3. {{ fn(n) }} 调用函数
    4. 若值为undefined 或者 null 就不显示
    
    5. 另一种写法`<div v-text="表达式"></div>`可代替{{}}
    
- HTML内容:
    
    若 data.x 的值为`<strong>hi</strong>`

    则`<div v-html="x"></div>`即可显示粗体的hi。

- 展示{{ n }} 

     `<div v-pre>{{ n }} </div>`
     
     v-pre 不会对模板进行编译

## 绑定属性

- 绑定src

```
<img v-bind:src="x" />
可简写为:
<img :src="x" />
```
- 绑定对象

```
//绑定内联事件
<div 
    :style = "{border: '1px' solid red,height:100}">
</div>//100px可以写成100，但100em不行    
```

## 绑定事件

- v-on：事件名


```
//只写函数名，点击之后，Vue会运行add()
<button v-on:click= "add">+1<button>

//函数名后加参数，点击之后，Vue会运行xxx(1)
<button v-on:click= "xxx(1)">xxx<button>

//直接写可执行代码，点击之后，Vue会运行n+=1
<button v-on:click= "n+=1">xxx<button>
```

- **缩写!!!**

```
<button @click>="add">+1</button>
```

## 条件判断

- if...else:

```
<div v-if="x > 0">x>0</div>

<div v-else-if="x === 0">x === 0</div>

<div v-else>x < 0</div>

```

## 循环

- for(value,key) in 对象或数组

```
//遍历数组
<ul>
    <li v-for="(u,index) in users" :key="index"> 
    索引:{{index}} 值:{{u.name}}
    </li>
</ul>//:key="index"有bug，后面说

//遍历对象
<ul>
    <li v-for="(value,index) in obj" :key="name"> 
    属性名:{{name}},属性值:{{value}}
    </li>
</ul>//：key需要唯一性的值
```

## 显示，隐藏

- v-show:

```
<div v-show="n % 2 ===0"> n是偶数 </div>
```
- 近似等于：

```
<div :style="{display: n % 2 ===0?'block':'none'}">n是偶数</div>
```
note:

看的见得元素display不只有block，如table的display为table,li的display为list-item。