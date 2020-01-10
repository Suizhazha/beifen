---
title: "CSS布局和定位"
date: 2020-01-10T19:54:28+08:00
draft: false
---

### 布局是什么：

把页面分成一块一块，按左中右，上中下等排列。

### 布局分类:

- 固定宽度布局，例如淘宝网， 一般宽度 960/1000/1024px。
- 不固定宽度布局，例如手机端，主要靠文档流原理布局。
  文档流本身就是自适应的，不需要额外添加样式。
- 响应式布局，pc 上固定宽度，手机上不固定宽度，是一种混合布局。

### 布局思路：

- 从大到小:先定大局，再完善每个小布局。
- 从小到大:先完成小布局，再组合成大布局，推荐新手。

---

### 三种布局套路：

- float 布局：

      1. 子元素上加float：left和width。
      2. 在父元素上加.clearfix。

      例如：

      ![](https://user-gold-cdn.xitu.io/2020/1/7/16f801aab2022468?w=1279&h=699&f=png&s=116392)

  Notes：

  - 有时最后一个元素不加 width，留些空间，可加上最大宽度`max-width：100px；`若加上 width 会出现下图情况:
    ![](https://user-gold-cdn.xitu.io/2020/1/7/16f80226f625feb8?w=139&h=51&f=png&s=3749)
  - 不需要做响应式，float 布局专为 IE 准备。
  - 解决 IE6/7 存在双倍 margin 的 bug，

         1. 针对IE6/7，把margin减半，如下图，则IE上显示5px乘2，正常浏览器上显示10px：

    ![](https://user-gold-cdn.xitu.io/2020/1/7/16f803169194f6f8?w=267&h=55&f=png&s=8283) 2. 加一个 display：inline-block； - 若图片下有多余的东西：
    添加
    `vertical-align: top;`
    或者`vertical-align: middle;`
    ![](https://user-gold-cdn.xitu.io/2020/1/7/16f806065bc2dd9d?w=403&h=107&f=png&s=30878)

  - 有时 border 调试会干扰 width，可用 outline 调试。
  - 如果有块级元素且 width 固定，则左右 margin 的 auto 可让元素自动居中。
  - 关于平均布局，计算出 x，y 的值，必要时中间加一层 div，用到负 margin，值为 y 的值。

- flex 布局：

      flex container（容器）样式：一般作父元素

       - 让一个元素变成flex容器：

  ![](https://user-gold-cdn.xitu.io/2020/1/8/16f8519c00157e08?w=292&h=136&f=png&s=10623)

  1.  justify-content 属性：将 flex 元素与主轴对齐。

      - flex-start: 元素和容器的左端对齐
      - flex-end: 元素和容器的右端对齐
      - center: 元素在容器里居中
      - space-between:元素之间保持相等的距离
      - space-around:元素周围保持相等的距离

  2.  align-items 属性：在交叉轴上对齐多个元素。

      - flex-start: 元素与容器的顶部对齐
      - flex-end: 元素与容器的底部对齐。
      - center: 元素纵向居中
      - baseline: 元素在容器的基线位置显示
      - stretch: 元素被拉伸以填满整个容器

  3.  flex-direction 属性:决定主轴的方向。
      - row: 元素摆放的方向和文字方向一致
      - row-reverse: 元素摆放的方向和文字方向相反
      - column: 元素从上放到下
      - column-reverse: 元素从下放到上
  4.  flex-wrap 属性：定义元素必须在一行，或者自动换行。
      - nowrap: 所有的元素都在一行
      - wrap: 元素自动换成多行
      - wrap-reverse: 元素自动换成逆序的多行
  5.  flex-flow 属性：
      flex-flow 属性包括 flex-direction 和 flex-wrap 两个属性，这个缩写属性接受两个属性的值，两个值中间以空格隔开。

          例如：`flex-flow: row wrap;`设置行并自动换行。

  6.  align-content 属性：决定行与行之间的间隔，而 align-items 决定元素整体在容器的什么位置。
      - flex-start: 多行都集中在顶部。
      - flex-end: 多行都集中在底部。
      - center: 多行居中。
      - space-between: 行与行之间保持相等距离。
      - space-around: 每行的周围保持相等距离。
      - stretch: 每一行都被拉伸以填满容器。


    flex items（项目）样式：一般作子元素

![](https://user-gold-cdn.xitu.io/2020/1/9/16f89d7b43b2400c?w=189&h=186&f=png&s=23768)

1.  order 属性:决定 flex 元素的顺序，元素的属性默认值为 0，还可设置属性为正数或负数。
2.  flex-grow 属性：决定 flex 元素的拉伸程度，元素的属性默认值为 0，还可设置属性为正数。
3.  flex-shrink 属性：决定了 flex 元素的收缩程度，flex 元素仅在默认宽度之和大于容器的时候才会发生收缩，其收缩的大小是依据 flex-shrink 的值，属性默认值为 0，还可设置属性为正数。
4.  flex-basis 属性：决定了 flex 元素的基准宽度，如果不使用 box-sizing 改变盒模型的话，那么这个属性就决定了 flex 元素的内容盒（content-box）的尺寸，属性默认值为 auto。
5.  flex-grow、flex-shrink 和 flex-basis 属性可以缩写，例如:

          flex-grow: 1;
          flex-shrink: 0;
          flex-basis: 100px;

    可以写成：

          flex： 1 0 100px;

6.  align-self 属性：在交叉轴上对齐一个元素，其值和 align-items 相同，但会覆盖 align-items 属性值。

### 推荐一款 flex 青蛙游戏，轻松愉快学习 flex 布局，以上 flex 元素属性解释也参考此游戏，详细可访问https://flexboxfroggy.com/#zh-cn。

- grid 布局：功能最强大的布局方案，但目前兼容性还不好。也分 container 和 items 样式，使用 grid-template-rows 和 grid-template-columns 属性来定义网格的 columns 和 rows，也可使用 grid-column-start, grid-column-end, grid-row-start 和 grid-row-end 属性定位网格线。
  例如：

```
.container {
           display: grid;
           grid-template-columns: 1fr 1fr 1fr;
           grid-template-rows: 100px 100px;
         }
.items{
     grid-column-start: 1;
     grid-column-end: 2;
     grid-row-start: 1;
     grid-row-end: 2;
 }
```

![](https://user-gold-cdn.xitu.io/2020/1/9/16f8a5ad65608989?w=651&h=335&f=png&s=13874)

#### grid 尤其适合不规则的布局。

---

### CSS 定位：

- position

  - static：默认值，待在文档流里
  - relative：相对定位，未脱离文档流，可在不改变页面布局的前提下调整元素位置。

    1.  现在已经很少用作位移，常用作 absolute 父元素。
    2.  配合 z-index：默认值 auto，不创建新层叠上下文，还可取正负数。

  - absolute：绝对定位，相对于祖先元素中最近的一个定位元素定位的，定位基准是祖先非 static 的定位元素。

    1. 脱离原来位置，另起一层，如对话框关闭按钮或鼠标提示。
    2. 配合 z-index。
    3. 和 relative 父元素配合使用。

  Notes：

        1.white-space:nowrap;文字内容不准换行。
        2.善用left：100%。
        3.善用left：50%；加负margin。
        4.有些浏览器不写top/left会位置错乱。

  - fixed：固定定位，定位基准是 viewport，手机上尽量不要用这个属性（坑）。

    1.  用于烦人的广告或者回到顶部按钮。

    2.  配合 z-index。

  - sticky：沾滞定位，适合导航，目前兼容性很差。
