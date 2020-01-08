---
title: "HTML重点标签"
date: 2020-01-03T22:14:28+08:00
draft: false
---

最近两天看了饥人谷的 HTML 网课，结合 mdn 文档写了篇博客，分享给大家。如有错误之处，欢迎指正！（没有奖励 😝）

### a 标签

`<a href="" target=""></a>`

---

### 属性：

- href：超链接
- target：打开超链接窗口方式
  （http-server -c-1 或着 parcel+文件名来打开 vscode 网址）
- download 下载网页（很多浏览器不支持）
- rel=noopener（防止一个 bug，以后会讲）

---

### a 的 href 取值：

- 网址：
  1.  https://网址
  2.  http://网址
  3.  //网址（最高级，推荐。查看：开发者工具，勾选 preserve log,浏览器自动补全跳转）
- 路径
  1.  /a/b/c 以及 a/b/c（当前目录下查找）
  2.  index.com 以及./index.com（都是当前目录下查找）
- 伪协议
  1.  Javascript:;`<a href="Javascript:;"></a>`为了直接执行 js，现在常作点击之后无动作的 a 标签）
  2.  mailto:邮箱`<a href="mailto:573505403@qq.com"></a>`
  3.  tel:手机号（简历用）`<a href="tel:17853318194"></a>`
- id :`<a href="#xxx"></a>`（内部锚点，跳转到指定标签位置）

---

### a 的 targe 取值：

- 内置名字：
  1.  \_blank（在新窗口打开）
  2.  \_self（在当前窗口打开）
  3.  \_top（在最顶层窗口打开）
  4.  \_parent（在父级窗口打开）
  5.  xxx（有 xxx 窗口就使用，没有就在新窗口打开就命名新窗口为 xxx，多链接看效果）

---

### iframe 标签：

内嵌窗口，已经很少使用，现在都用 ajax 方式。

---

### table 标签

table 内只能有 thead，tbody，tfoot 标签，包括：

- tr：table 一行
- th：table 表头
- td：table 数据
  table 三个标签可以不按顺序写，浏览器自动纠正顺序。

#### 相关样式：

1. table-layout：
   用于布局单元格，行和列的算法。其属性：

   - auto：浏览器采用自动表格布局算法对表格布局。表格及单元格的宽度取决于其包含的内容。
   - fixed：表格和列的宽度通过表格的宽度来设置，某一列的宽度仅由该列首行的单元格决定。在当前列中，该单元格所在行之后的行并不会影响整个列宽。

2. border-collapse：用来决定表格的边框是分开的还是合并的。
   - collapse：合并，相邻的单元格共用同一条边框。
   - separate：分开，默认值。每个单元格拥有独立的边框。

---

### img 标签：

发出 get 请求，展示一张图片。

#### 属性：

- src：必须存在，包含图片的网络地址或文件路径。
- alt：不一定存在，包含对图像的文本描述，加载失败会提示代替的文本。
- weight：只写高度，宽度会自适应。
- height：只写宽度，高度会自适应。

note:永远不要让图片变形！可以只写高度或宽度。

#### js 事件:

onload/onerror:监听图片是否加载成功。

![](https://user-gold-cdn.xitu.io/2020/1/3/16f6a81fca1ffd9f?w=275&h=118&f=png&s=31091)

#### 响应式：

先所有元素 css reset，加句
`img{max-width：100%}`

---

### form 标签：

表单标签，内一般含有输入框和提交按钮（input 标签）。作用：发送一个 get 或 post 请求，然后刷新页面。

#### 属性：

- action：处理此表单信息所在的 URL。
- method：可使用 HTTP post 或 get 方式来提交表单。
- autocomplete：浏览器自动填充,使用 on 或 off 来打开或着关闭此功能。
- target：在提交表单之后，在哪个页面显示收到的回复，包括\_self，\_blank，\_top 和\_parent。

#### 事件：

onsubmit：用户点击提交按钮后触发。提交按钮可使用 value 更改提交按钮名称。
例如：`<input type="submit" value="发射">`<input type="submit" value="发射">

或者`<button type="submit">发射</button>`<button type="submit">发射</button>。

note:两个区别 input 内不能再加其他标签，只能是纯文本，而 button 可以，甚至可以加图片。例如：`<button type="submit"><strong>发射</strong></button>`<button type="submit"><strong>发射</strong></button>。

---

### input 标签：

为了让用户输入内容。

#### 常用属性：

- text：单行文本框，默认 type。
- color：颜色控件。
- password：值被遮盖的单行文本字段。
- radio：单选按钮，name 属性使用同一个值可实现二选一。
- checkbox：多选按钮，name 属性使用同一个值，使其在同一数组中。
- file：选择文件，多选文件可添加 multiple 属性。
- hidden：隐藏的控件，用于 js 自动填入 id，字符串之类的。
- image：图片提交按钮。可以使用 height 和 width 属性定义图片的大小。

#### 事件：

onchange：用户输入改变时触发。
onfocus：用户鼠标集中时触发。
onblur：用户鼠标离开时触发。

#### 验证器：

HTML5 新增功能。例如必须提交文本：`<input type="text" required>`

   <input type="text" required>
   
#### 注意事项：
- 一般不监听input的click事件。
- form内的input要有name。
- form内放一个type=submit才能触发submit事件。
***

#### 其他标签:

- textarea：多行文本框。固定文本框大小可用`<textarea style="resize: none;"></textarea>`具体大小可用 width，height 属性固定。

  <textarea style="resize: none;"></textarea>

- select:选择标签，例如：
  `<select><option value="1">周一</option><option value="1">周二</option></select>`

  <select><option value="">请选择</option><option value="1">周一</option><option value="2">周二</option></select>
