---
title: "关于DOM"
date: 2020-02-09T21:02:40+08:00
draft: false
---

DOM:文档对象模型(Document Object Model)

## API

- 获取任意元素，也叫标签

```
window.idxxx或直接idxxx

document.getElementByid('idxxx')
//获取与全局属性冲突的id

document.getElementsByTagName('div')[0]
//获取所有标签名为div的元素，因为是全部div，需要下标获取单独的div

document.getElementsByClassName('div')[0]
//获取class的类名元素

document.querySelector('#idxxx')
//获取id

document.querySelector('div>span:nth-child(2  )')

document.querySelectorAll('.red')[0]
```

notes：

1. 兼容 IE 才用 getElement(s)Byxxx
2. 工作用 querySelector 和 querySelectorAll
3. 做 demo 直接用 idxxx

- 获取特定元素

```
document.documentElement
//获取html元素

document.head
//获取head元素

document.body
//获取body元素

window
//获取窗口（窗口不是元素），为添加全局的事件监听

document.all
//获取所有元素，IE发明的，在其他浏览器里为假值，为第六个falsy值
```

## Node

x.nodeType 可以得到一个数字，其中

1. 元素 Element，也叫便签 Tag
2. 文本 text
3. 注释 Comment
4. 文档 Document
5. 表示文档片段 DocumentFragment

### 节点的增删改查

- 增
  1. 创建一个标签节点
  ```
  let div1 = document.createElement('div')
  document.createElement('style')
  document.createElement('script')
  ```
  2. 创建一个文本节点
  ```
  text1 = document.createTextNode('你好')
  ```
  3. 标签里插文本
  ```
  div1.appendChild(text1)
  //Node接口
  或者
  div1.innerText = '你好'
  或者
  div1.textContent = '你好'
  //Element接口
  ```
  4. 插入页面里
  创建的标签默认在 JS 线程中，必须插到 head 或 body 中，才会生效
  ```
  document.body.appendChild(div1)
  ```
- 删
  ```
  div1.parentNode.removechild(div1)
  //从DOM中删除div1，但还在内存中，而div1 = null可彻底移除
  或者
  div1.remove()
  //IE不支持

  document.body.appendChild(div1)
  //  恢复div1
  ```
- 改

  1. 修改属性

  ```
  div1.className = 'red'
  //全覆盖
  div1.classList.add('green')
  //新语法，推荐

  div1.style.color = 'bule'
  //修改部分样式

  div1.style.backgroundColor = 'white'
  ```

  2.  改事件处理函数

  ```
  div1.onclick = function(x){
      console.log(this)
      console.log(arguments[0])
  }
  //当用户点击div时，该this为div，arguments[0] 是事件相关的信息组成的对象

  div1.addEventListener
  //div1.onclick升级版
  ```

  3. 修改内容

  ```
  text.innerText = 'hi'
  或者
  text.textContent = 'hi'
  //修改文本内容

  div.innerHTML = '<strong>hi</strong>'
  //修改HTML内容

  div.innerHTML = ''
  div.appendChild(div1)
  //修改标签，先清空，再修改
  ```

  4. 修改 parent

  ```
  newParent.appendChild(div)
  ```

- 读

  ```
  div1.classList
  或者
  div1.getAttribute('class')
  //但两种获取的值可能有所不同
  ```

- 查

  1. 查 parent

  ```
  node.parentNode
  或
  node.parentElement
  ```

  2. 查 child

  ```
  node.childNodes
  //包括文本节点
  或
  node.children
  //不包括文本节点，推荐
  ```

  3. 查兄弟

  ```
  node.perentNode.children
  //需要利用遍历排除自己
  ```

  4. 查看老大老幺

  ```
  node.firstChild
  node.lastChild
  ```

  5. 查看上一个哥哥或下一个弟弟

  ```
  node.previousSibling
  node.nextSibling
  ```

  6. 遍历一个 div 中所有元素

  ```
  travel = (node, fn) => {
      fn(node)
      if(node.children){
          for(let i = 0;i<node.children.length;i++){
              travel(node.children[i],fn)
          }
      }
  }
  travel( div1,(node) => console.log(node) )
  ```
