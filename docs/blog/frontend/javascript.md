## JavaScript 简介

[JavaScript](https://developer.mozilla.org/zh-CN/docs/Glossary/JavaScript)（缩写：JS）是一门完备的动态编程语言。当应用于 [HTML](https://developer.mozilla.org/zh-CN/docs/Glossary/HTML) 文档时，可为网站提供动态交互特性。由布兰登·艾克（Brendan Eich，Mozilla 项目、Mozilla 基金会和 Mozilla 公司的联合创始人）发明。

JavaScript 的应用场合极其广泛，简单到幻灯片、照片库、浮动布局和响应按钮点击，复杂到游戏、2D/3D 动画、大型数据库驱动程序等等。

JavaScript 相当简洁，却非常灵活。开发者们基于 JavaScript 核心编写了大量实用工具，可以使 开发工作事半功倍。其中包括：

- 浏览器应用程序接口（[API](https://developer.mozilla.org/zh-CN/docs/Glossary/API)）—— 浏览器内置的 API 提供了丰富的功能，比如：动态创建 HTML 和设置 CSS 样式、从用户的摄像头采集处理视频流、生成 3D 图像与音频样本等等。
- 第三方 API —— 让开发者可以在自己的站点中整合其它内容提供者（Twitter、Facebook 等）提供的功能。
- 第三方框架和库 —— 用来快速构建网站和应用。

JavaScript 在[Ecma International](https://www.ecma-international.org/)进行了标准化 - 欧洲信息和通信系统标准化协会（ECMA 以前是欧洲计算机制造商协会的首字母缩写），以提供基于 JavaScript 的标准化国际编程语言。

这个 JavaScript 的标准化版本，称为 ECMAScript，在所有支持该标准的应用程序中的行为方式都相同。公司可以使用开放标准语言来开发他们的 JavaScript 实现。ECMAScript 标准记录在 ECMA-262 规范中。

目前大多数浏览器都支持 ES5.1 标准，ES6 

## 语法和数据类型

### 引入 JavaScript

```javascript
<script src="other.js" defer></script>
// defer 表示异步延迟加载
```

### 变量

在 JS 中，变量可以通过三个关键字定义：

[`var`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/var)

声明一个变量，可选初始化一个值。

[`let`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/let)

声明一个块作用域的局部变量，可选初始化一个值。

[`const`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/const)

声明一个块作用域的只读常量。

### 数据类型

变量可以有多种不同的数据类型，在 JS 中不需要显示指定数据类型。

| 变量                                                         | 解释                                                         | 示例                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| [String](https://developer.mozilla.org/zh-CN/docs/Glossary/String) | 字符串（一串文本）：字符串的值必须用引号（单双均可，必须成对）扩起来。 | `let myVariable = '李雷';`                                   |
| [Number](https://developer.mozilla.org/zh-CN/docs/Glossary/Number) | 数字：无需引号。                                             | `let myVariable = 10;`                                       |
| [Boolean](https://developer.mozilla.org/zh-CN/docs/Glossary/Boolean) | 布尔值（真 / 假）： `true`/`false` 是 JS 里的特殊关键字，无需引号。 | `let myVariable = true;`                                     |
| [Array](https://developer.mozilla.org/zh-CN/docs/Glossary/array) | 数组：用于在单一引用中存储多个值的结构。                     | `let myVariable = [1, '李雷', '韩梅梅', 10];` 元素引用方法：`myVariable[0]`, `myVariable[1]` …… |
| [Object](https://developer.mozilla.org/zh-CN/docs/Glossary/Object) | 对象：JavaScript 里一切皆对象，一切皆可储存在变量里。这一点要牢记于心。 | `let myVariable = document.querySelector('h1');` 以及上面所有示例都是对象。 |

### 运算符

[运算符 (en-US)](https://developer.mozilla.org/en-US/docs/Glossary/Operator) 是一类数学符号，可以根据两个值（或变量）产生结果。以下表格中介绍了一些最简单的运算符，可以在浏览器控制台里尝试一下后面的示例。

> **备注：** 这里说“根据**两个**值（或变量）产生结果”是不严谨的，计算两个变量的运算符称为“二元运算符”，还有一元运算符和三元运算符，下表中的“取非”就是一元运算符。

| 运算符     | 解释                                                         | 符号          | 示例                                                         |
| :--------- | :----------------------------------------------------------- | :------------ | :----------------------------------------------------------- |
| 加         | 将两个数字相加，或拼接两个字符串。                           | `+`           | `6 + 9;"Hello " + "world!";`                                 |
| 减、乘、除 | 这些运算符操作与基础算术一致。只是乘法写作星号，除法写作斜杠。 | `-`, `*`, `/` | `9 - 3;8 * 2; //乘法在JS中是一个星号9 / 3;`                  |
| 赋值运算符 | 为变量赋值（你之前已经见过这个符号了）                       | `=`           | `let myVariable = '李雷';`                                   |
| 等于       | 测试两个值是否相等，并返回一个 `true`/`false` （布尔）值。   | `===`         | `let myVariable = 3;myVariable === 4; // false`              |
| 不等于     | 和等于运算符相反，测试两个值是否不相等，并返回一个 `true`/`false` （布尔）值。 | `!==`         | `let myVariable = 3;myVariable !== 3; // false`              |
| 取非       | 返回逻辑相反的值，比如当前值为真，则返回 `false`。           | `!`           | 原式为真，但经取非后值为 `false`： `let myVariable = 3;!(myVariable === 3); // false` |

运算符种类远不止这些，不过目前上表已经够用了。完整列表请参阅 [表达式和运算符](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators)。

### 条件语句

条件语句是一种代码结构，用来测试表达式的真假，并根据测试结果运行不同的代码。一个常用的条件语句是 `if ... else`。下面是一个示例：

```javascript
let iceCream = 'chocolate';
if (iceCream === 'chocolate') {
  alert('我最喜欢巧克力冰激淋了。');
} else {
  alert('但是巧克力才是我的最爱呀……');
}
```

`if ( ... )` 中的表达式进行测试，用（上文所提到的）等于运算符来比较变量 `iceCream` 与字符串 `'chocolate'` 是否相等。如果返回 `true`，则运行第一个代码块；如果返回 `false`，则跳过第一块直接运行 `else` 之后的第二个代码块。

### 函数

[函数](https://developer.mozilla.org/zh-CN/docs/Glossary/Function) 用来封装可复用的功能。如果没有函数，一段特定的操作过程用几次就要重复写几次，而使用函数则只需写下函数名和一些简短的信息。之前已经涉及过一些函数，比如：

```javascript
let myVariable = document.querySelector('h1');
```

```javascript
alert('hello!');
```

`document.querySelector` 和 `alert` 是浏览器内置的函数，随时可用。

如果代码中有一个类似变量名后加小括号 `()` 的东西，很可能就是一个函数。函数通常包括[参数](https://developer.mozilla.org/zh-CN/docs/Glossary/Argument)，参数中保存着一些必要的数据。它们位于括号内部，多个参数之间用逗号分开。

比如， `alert()` 函数在浏览器窗口内弹出一个警告框，还应为其提供一个字符串参数，以告诉它警告框里要显示的内容。

好消息是：人人都能定义自己的函数。下面的示例是为两个参数进行乘法运算的函数：

```javascript
function multiply(num1, num2) {
  let result = num1 * num2;
  return result;
}
```

尝试在控制台运行这个函数，不妨多试几组参数，比如：

```javascript
multiply(4, 7);
multiply(20, 20);
multiply(0.5, 3);
```

**备注：** [`return`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/return) 语句告诉浏览器当前函数返回 `result` 变量。这是一点很有必要，因为函数内定义的变量只能在函数内使用。这叫做变量的 [作用域](https://developer.mozilla.org/zh-CN/docs/Glossary/Scope)。（详见 [变量作用域](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Grammar_and_types#variable_scope)。）

### 事件

事件能为网页添加真实的交互能力。它可以捕捉浏览器操作并运行一些代码做为响应。最简单的事件是 [点击事件](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/click_event)，鼠标的点击操作会触发该事件。可尝试将下面的代码输入到控制台，然后点击页面的任意位置：

```javascript
document.querySelector('html').onclick = function() {
    alert('别戳我，我怕疼。');
}
```

将事件与元素绑定有许多方法。在这里选用了 [``](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/html) 元素，把一个匿名函数（就是没有命名的函数，这里的匿名函数包含单击鼠标时要运行的代码）赋值给了 `html` 的 [onclick (en-US)](https://developer.mozilla.org/en-US/docs/Web/API/Element/click_event) 属性。

请注意：

```javascript
document.querySelector('html').onclick = function() {};
```

等价于

```javascript
let myHTML = document.querySelector('html');
myHTML.onclick = function() {};
```

只是前者更简洁。

刚刚我们传递给 `onclick` 的函数被称为匿名函数，因为它没有名字。匿名函数还有另一种我们称之为箭头函数的写法，箭头函数使用 `() =>` 代替 `function ()`：

```javascript
document.querySelector('html').addEventListener('click', () => {
  alert('别戳我，我怕疼。');
});
```

## 浏览器对象 BOM

浏览器对象模型 (BOM) 使 JavaScript 有能力与浏览器"对话"。

Window 对象是BOM中所有对象的核心，除了是BOM中所有对象的父对象外，还包含一些窗口控制函数。

### Window 对象

所有浏览器都支持 window 对象。它表示浏览器窗口。

所有 JavaScript 全局对象、函数以及变量均自动成为 window 对象的成员。

全局变量是 window 对象的属性。

全局函数是 window 对象的方法。

甚至 HTML DOM 的 document 也是 window 对象的属性之一：

```javascript
window.document.getElementById("header"); 
```

与此相同：

```javascript
document.getElementById("header");  
```

Window 中关于窗口的方法：

- window.open() - 打开新窗口
- window.close() - 关闭当前窗口
- window.moveTo() - 移动当前窗口
- window.resizeTo() - 调整当前窗口的尺寸

### window.screen

> window.screen 对象包含有关用户屏幕的信息，这些信息可以用来了解客户端硬件的基本配置。
>

- screen.availWidth - 可用的屏幕宽度
- screen.availHeight - 可用的屏幕高度

### window.location

> window.location 对象用于获得当前页面的地址 (URL)，并把浏览器重定向到新的页面。
>
> 这种方法既可以用于具有onclick事件的标签，也可以用于满足某些条件进行跳转，特点是方便且灵活。

- location.hostname 返回 web 主机的域名
- location.pathname 返回当前页面的路径和文件名
- location.port 返回 web 主机的端口 （80 或 443）
- location.protocol 返回所使用的 web 协议（http:// 或 https://）

### window.history

> window.history 对象包含浏览器的历史。

- history.back() - 与在浏览器点击后退按钮相同
- history.forward() - 与在浏览器中点击向前按钮向前相同

### window.navigator

> window.navigator 对象包含有关访问者浏览器的信息。

**警告**：来自 navigator 对象的信息具有误导性，**不**应该被用于检测浏览器版本，这是因为：

- navigator 数据可被浏览器使用者更改
- 一些浏览器对测试站点会识别错误
- 浏览器无法报告晚于浏览器发布的新操作系统

### JavaScript 弹窗

可以在 JavaScript 中创建三种消息框：警告框、确认框、提示框。

**警告框**

警告框经常用于确保用户可以得到某些信息。当警告框出现后，用户需要点击确定按钮才能继续进行操作。

```
window.alert("sometext");
```

**确认框**

确认框通常用于验证是否接受用户操作。当确认卡弹出时，用户可以点击 "确认" 或者 "取消" 来确定用户操作。当你点击 "确认", 确认框返回 true， 如果点击 "取消", 确认框返回 false。

```
window.confirm("sometext");
```

**提示框**

提示框经常用于提示用户在进入页面前输入某个值。当提示框出现后，用户需要输入某个值，然后点击确认或取消按钮才能继续操纵。如果用户点击确认，那么返回值为输入的值。如果用户点击取消，那么返回值为 null。

```
window.prompt("sometext","defaultvalue");
```

## 文档对象 DOM





## 参考资料

[JavaScript MDN 官方文档](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript)

[JavaScript教程 W3Cschool](https://www.w3cschool.cn/javascript/)

