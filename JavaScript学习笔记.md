# JavaScript 学习笔记

## 一、什么是 JavaScript

JavaScript（简称 JS）是网页里负责"交互"的语言。HTML 决定内容，CSS 决定外观，JavaScript 决定用户操作之后页面怎么反应：点按钮切换主题、表单提交校验、点击弹出提示、页面动态加载内容，都靠它。

这次个人主页里，点一下"切换深色/浅色模式"按钮，页面配色跟着变，就是用 JavaScript 实现的。

## 二、JS 在网页里放在哪里

最简单的方式是在 HTML 底部写一个 `<script>` 标签，代码放在里面：

```html
<script>
    // JS 代码写在这里
</script>
```

放在 `</body>` 之前，是为了让浏览器先把页面元素加载完，JS 再去找页面上的按钮，避免找不到元素报错。

## 三、变量和基本类型

### 1. 声明变量

```js
const btn = document.getElementById("modeBtn");
let name = "杜新宇";
```

- `const`：声明后不会再重新赋值的变量，这次存按钮对象就用它。
- `let`：声明后面可能会改变值的变量。
- 早期的 `var` 现在不推荐使用，作用域容易出问题。

### 2. 常见数据类型

- 字符串：用引号包起来，比如 `"hello"`、`'网安新生'`
- 数字：比如 `18`、`3.14`
- 布尔值：`true` / `false`
- 数组：`[1, 2, 3]`
- 对象：`{ name: "杜新宇", age: 18 }`

## 四、函数

函数是一段可以重复执行的代码块。这次给按钮绑定点击事件，写的就是一个函数：

```js
btn.onclick = function () {
    document.body.classList.toggle("dark");
};
```

拆开看：

- `btn.onclick`：给按钮设置点击事件。
- `function () { ... }`：点击之后要执行的函数。
- 函数里的 `document.body.classList.toggle("dark")`：给页面主体切换 `dark` 这个类名。

也可以写成先定义函数、再绑定的形式：

```js
function switchTheme() {
    document.body.classList.toggle("dark");
}

btn.onclick = switchTheme;
```

## 五、DOM 操作：JS 怎么找到页面元素

DOM（文档对象模型）可以理解成浏览器把 HTML 页面整理成的一棵节点树，JS 通过它来读取和修改页面。

### 1. 按 id 找元素

```js
const btn = document.getElementById("modeBtn");
```

页面上按钮写的是 `id="modeBtn"`，这里用 `getElementById` 把它取出来存到 `btn` 里。

### 2. 修改元素的类名

```js
document.body.classList.toggle("dark");
```

- `document.body`：页面的 `<body>` 元素。
- `classList`：这个元素身上的类名集合。
- `toggle("dark")`：如果有 `dark` 类就去掉，没有就加上。点一次切换一次，正好对应主题切换的需求。

### 3. 控制台调试

浏览器按 F12 打开开发者工具，在 Console（控制台）里可以直接写 JS 语句查看结果，比如：

```js
console.log("页面加载完成");
```

`console.log` 会把内容打印到控制台，是排查问题最常用的手段。

## 六、这次项目的完整交互逻辑

个人主页的主题切换，完整流程是：

1. HTML 里放一个按钮，`id="modeBtn"`。
2. JS 用 `getElementById` 把按钮取出来。
3. 给按钮绑定 `onclick` 点击事件。
4. 点击时对 `body` 执行 `classList.toggle("dark")`。
5. CSS 里提前写好 `.dark` 下的一套颜色变量，类名加上之后，整套配色自动切换成深色。

对应代码：

```js
const btn = document.getElementById("modeBtn");

btn.onclick = function () {
    document.body.classList.toggle("dark");
};
```

## 七、踩过的坑

1. **找不到元素**：JS 写在 `<head>` 里、页面元素还没加载完就执行，`getElementById` 取到的是 `null`，后面调用方法就报错。解决办法是把 `<script>` 放到页面底部，或者等页面加载完成后再执行代码。
2. **类名写错**：CSS 里写的是 `.dark`，JS 里 `toggle` 写成了别的名字，点击之后页面没反应。两边类名必须完全一致。
3. **把 HTML 和 JS 混在一起想**：一开始以为按钮点击效果是 HTML 自带的，后来才理清——按钮是 HTML 放上去的，外观是 CSS 改的，"点了之后做什么"才是 JavaScript 管的。
4. **括号和引号漏写**：写函数时漏了花括号 `}`，或者字符串引号没闭合，控制台会直接报语法错误。报错信息先看提示的行号，定位起来会快很多。

## 八、学习感想

JavaScript 是三件套里最"活"的部分，也是我目前觉得最难的一部分：HTML 和 CSS 大多是静态的，而 JS 要考虑事件什么时候触发、变量存的是什么、页面元素能不能找到。这次只做了一个点击切换主题的小功能，已经能体会到 DOM 操作的基本思路：先找到元素，再给它绑定事件，事件里修改页面状态。

后面还需要继续补基础语法：条件判断、循环、数组和函数的更多用法，再慢慢接触表单校验、页面动态渲染这些更实用的功能。

> （注：部分内容由豆包 AI 生成）