---
title: "CSS知识总结"
date: 2020-01-13T22:01:29+08:00
draft: false
---

### 浏览器渲染过程：

1. 根据 HTML 构建 HTML 树（DOM）

   - 文档对象模型(DOM)是 HTML 和 XML 文档的编程接口，它会将 web 页面和脚本或程序语言连接起来。

2. 根据 CSS 构建 CSS 树（CSSOM）

   - CSS 对象模型 (CSS Object Model, CSSOM) 是一个存放所有 CSS 选择器与相关特性的树状结构容器，拥有根节点、邻居节点、后代节点、子代节点以及其他关系。 CSSCOM 非常类似于 DOM 文件对象模型 。

3. 将两棵树合并成一颗渲染树（render tree）
4. Layout 布局（文档流，盒模型，计算大小和位置）
5. Paint 绘制（将边框颜色，文字颜色，阴影等画出来）
6. Compose 合成（根据层叠关系展示画面）

### 如何更新样式：

一般用 JS 更新样式：

- div.style.background='red'
- div.style.display='none'
- div.classList.add('red')（加样式不如加类）

### 三种渲染方式和更新方式：

1.  JS/CSS>样式>布局>绘制>合成

- 例如`div.remove()`会触发当前消失，其他元素 relayout。

2.  JS/CSS>样式>绘制>合成

- 例如改变背景颜色，则直接 repaint+composite。

3.  JS/CSS>样式>合成

- 改变 transform，只需 composite

Notes：

- 必须全屏查看效果，在 iframe 里看问题。
- csstriggers.com 可查看每种属性触发哪些流程。

---

### CSS 动画优化

详细可查看<a herf="https://developers.google.com/web/fundamentals/performance/rendering/stick-to-compositor-only-properties-and-manage-layer-count">google 团队文章</a>

- JS 优化：使用 requestAnimationFrame 代替 setTimeout 或 setInterval
- CSS 优化：使用 will-change 或 translate

### transform 属性

1. 四个常用功能

- 位移 transsform

  `transsform:translate(50px);`X 轴位移 50 像素。

  Notes：

  - 若要在 Z 轴（垂直于视点）位移，需要在父元素上添加 perspective 属性。
  - `transsform:translate(-50%，-50%);`可做绝对定位元素的居中。
  - MDN 语法格式很重要！！！

- 缩放 scale：

  `transsform:scale(1.5)；`
  。用的很少，因为变形，容易出现模糊。

- 旋转 rotate：

`transsform:rotate(45deg)；`顺时针旋转 45 度。一般用于 360 度旋转制作 loading，或者按钮的交互（鼠标移到按钮上就转一圈），多看 MDN 文档。

- 倾斜 skew：

`transsform:skewX(15deg)；`X 轴倾斜 15 度。用得较少，用时搜 MDN 文档。

---

### transition

- 作用：补全中间帧。

  例如：
  ![](https://user-gold-cdn.xitu.io/2020/1/13/16f9ee7518795180?w=781&h=397&f=png&s=53303)<a herf="https://jsbin.com/rapokih/edit?html,css,js,output">效果</a>

- 语法：

  - transition：属性名 时长 过渡时间 延迟；

    `transition：right 10s linear；`

  - 可用逗号分隔开两个不同属性

    `transition：right 10s,top 10s；`

  - 可用 all 代表所有属性

    `transition：all 10s linear；`

  - 过渡方式：linear，ease，ease-in，ease-out，
    ease-in-out，cubic-bezier，step- start，step-end，steps。
    具体效果查看<a herf="https://developer.mozilla.org/zh-CN/docs/Web/CSS/transition-timing-function">MDN</a>

- Notes：并非所有属性都使用 transition。
  - display:block;=>display:none;不能过渡，而修改成透明度 opacity，也只是看不见了，位置还一直占着。
    一般改成 visibility:visible=>hidden，visibility 也是占位置的。
  - background 背景颜色可以过渡。
  - opacity 透明度可以过渡，但不推荐。

---

过渡必须有起始，一般只有一次或两次动画，比如 hover 和非 hover 状态的过渡。

若有中间过渡，可以使用两次 transform，用 setTimeout 或者监听 transitionend 事件确认中间点。

也可以使用 animation（声明关键帧，添加动画）来实现。

### animation

- keyframes 语法：
  一种是 from to:

```
@keyframes slidein {
  from {
    transform: translateX(0%);
  }

  to {
    transform: translateX(100%);
  }
}
```

或者百分数

```
@keyframes identifier {
  0% { top: 0; left: 0; }
  30% { top: 50px; }
  68%, 72% { left: 50px; }
  100% { top: 100px; left: 100%; }
}
```

- 语法：animation:时长|过渡方式|延迟|次数|方向|填充模式|是否暂停|动画名；

  - 时长：1s 或者 1000ms
  - 过渡方式：跟 transition 取值一样，如 linear
  - 次数：数字 或着 infinite（无限次）
  - 方向： - normal：每个循环内动画向前循环，换言之，每个动画循环结束，动画重置到起点重新开始，这是默认属性。 - reverse：反向运行动画，每周期结束动画由尾到头运行。 - alternate：动画交替反向运行，反向运行时，动画按步后退，同时，带时间功能的函数也反向，比如，ease-in 在反向时成为 ease-out。 - alternate-reverse：反向交替，反向开始交替
    动画第一次运行时是反向的，然后下一次是正向，后面依次循环。
  - 填充模式：
    - none：这是默认值，由该元素的 CSS 规则来显示该元素。
    - forwards：动画将停留在最后一个关键帧。
    - backwards：动画将在应用于目标时立即应用第一个关键帧中定义的值，并在 animation-delay 期间保留此值。第一个关键帧取决于 animation-direction 的值。
    - both：动画将遵循 forwards 和 backwards 的规则，从而在两个方向上扩展动画属性。
  - 是否暂停：
    - paused：当前动画已被停止。
    - running：当前动画正在运行。

  note：以上所有属性都有对应的单独属性。只改一个属性的话就要单独写。
