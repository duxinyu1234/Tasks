# CSS 学习笔记

## 一、什么是 CSS

CSS（Cascading Style Sheets，层叠样式表）负责网页的外观：颜色、字号、间距、圆角、阴影、位置、深色浅色主题等等。HTML 把内容摆好之后，CSS 负责把它装修得整齐好看。

和 HTML 的分工可以记成一句话：**HTML 说"页面上有什么"，CSS 说"它长什么样"。**

## 二、CSS 的三种引入方式

### 1. 内部样式表（这次项目用的方式）

在 HTML 文件的 `<head>` 里写一个 `<style>` 标签，样式全部写在里面：

```html
<style>
    body {
        background-color: #f5f7fa;
        color: #222;
    }
</style>
```

这次个人主页就是用这种方式，所有 CSS 集中在一个文件里，写起来方便，适合小页面。

### 2. 行内样式

直接写在某个标签的 `style` 属性里：

```html
<p style="color: blue;">这一段文字是蓝色的</p>
```

只对这一个标签生效，改动很零散，一般不推荐大面积使用。

### 3. 外部样式表

把样式单独存成一个 `.css` 文件，再在 HTML 里引入：

```html
<link rel="stylesheet" href="style.css">
```

适合大项目，多个网页共用一套样式，维护起来更清楚。

## 三、选择器

选择器决定 CSS 样式作用到哪些标签上。

### 1. 标签选择器

直接写标签名，作用到页面上所有这个标签：

```css
body {
    padding: 30px;
}
```

### 2. 类选择器（最常用）

HTML 里给标签加 `class` 属性，CSS 里用 `.类名` 选中：

```html
<div class="card">一块卡片</div>
```

```css
.card {
    background: #ffffff;
    border-radius: 14px;
    padding: 25px;
}
```

一个类可以给多个标签用，一个标签也可以同时写多个类名，中间用空格隔开。

### 3. id 选择器

HTML 里写 `id`，CSS 里用 `#id名` 选中：

```html
<button id="modeBtn">切换主题</button>
```

```css
#modeBtn {
    background-color: #4070f4;
    color: white;
}
```

一个页面里 id 一般只对应一个元素，后面 JavaScript 也常用 id 来找元素。

## 四、这次项目用到的常用属性

### 1. 文字和颜色

```css
color: #222;              /* 文字颜色 */
background-color: #f5f7fa; /* 背景颜色 */
font-family: "Microsoft Yahei", sans-serif; /* 字体 */
font-size: 18px;          /* 字号 */
line-height: 1.7;         /* 行高，控制文字行距 */
```

颜色可以用十六进制（`#4070f4`）、英文单词（`white`）或者 rgba 写法。

### 2. 盒子模型与间距

每个标签都可以看成一个盒子，从内到外是：内容、内边距 padding、边框 border、外边距 margin。

```css
.card {
    padding: 25px;        /* 内容和边框之间的距离 */
    margin-bottom: 20px;  /* 卡片和下面元素之间的距离 */
    border-left: 4px solid #4070f4; /* 左边一条竖边框 */
}
```

- `padding`：盒子内部留白。
- `margin`：盒子和外面其他元素之间的距离。

### 3. 圆角和阴影

```css
.card {
    border-radius: 14px; /* 卡片四角变圆 */
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08); /* 淡淡的投影 */
}
```

### 4. 居中与宽度限制

```css
.container {
    max-width: 750px; /* 内容最宽 750 像素 */
    margin: 0 auto;  /* 左右自动留白，实现水平居中 */
}
```

### 5. CSS 变量（这次做主题切换的关键）

把颜色统一存到根变量里，后面直接引用变量名：

```css
:root {
    --bg-color: #f5f7fa;
    --text-color: #222;
    --card-bg: #ffffff;
}

body {
    background-color: var(--bg-color);
    color: var(--text-color);
}
```

切换深色模式时，只要再定义一套 `.dark` 下的变量值，整个页面颜色就跟着一起变，不用逐个元素去改颜色。

## 五、踩过的坑

1. **盒模型宽度超出**：一开始没写 `box-sizing: border-box`，给卡片加了 `padding` 和边框之后，盒子总宽度比预期宽，把页面撑出横向滚动条。加上下面这句之后，padding 和边框会算进宽度里面，排版就正常了：

```css
* {
    box-sizing: border-box;
}
```

2. **样式不生效**：检查顺序一般是——类名有没有写错、HTML 里 `class` 和 CSS 里 `.类名` 对不对得上、选择器优先级是不是被别的样式覆盖了。
3. **颜色写在 JS 里逐个改**：最开始想切换主题时，在 JS 里一个个元素改颜色，代码又长又容易漏。后来改用 CSS 变量，只切换一个类名就完成整套配色，这是这次收获最大的一点。
4. **过渡效果**：颜色切换时加上 `transition: all 0.4s ease;`，颜色变化会平滑过渡，不会突然跳变。

## 六、学习感想

CSS 看起来都是属性名，实际最需要理解的是"盒子模型"：每个元素都是一个盒子，padding、border、margin 分别控制哪一层距离，想清楚之后，页面排版就不容易乱。

这次做个人主页，从最朴素的白字黑底，到加上卡片、圆角、阴影和深浅主题切换，能明显看到 CSS 对页面观感的影响。属性记不全没关系，用到的时候查文档，多调几次参数就有手感了。

> （注：部分内容由豆包 AI 生成）