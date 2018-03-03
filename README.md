# 前端开发规范
此为前端开发团队遵循和约定的代码书写规范，意在提高代码的规范性和可维护性。  
此规范为参考规范，不全是硬性要求，部分硬性约定见下一条[语法](# 一. 语法)，统一团队编码规范和风格。让所有代码都是有规可循的，并且能够得到沉淀，减少重复劳动。

## 黄金定律
永远遵循同一套编码规范 -- 可以是这里列出的，也可以是你自己总结的。如果你发现本规范中有任何错误，敬请指正。
> 不管有多少人共同参与同一项目，一定要确保每一行代码都像是同一个人编写的。

## 一.文件及文件夹  
* 命名全部英文小写字母+数字或连接符"`-` , `_` "，不可出现其他字符
* 根据不同的用途使用不同的目录，如，src源文件， dist项目打包目录，plugins插件目录
* 外部库文件根据需要增加版本号及压缩文件`min`关键词
> 例如：`jquery.1.9.1.js`,`modernizr-1.7.min.js`,`fileuploader.js`,`plugins.js`
* 文本文件： `.xxx` 采用UTF-8编码
* 图片文件： `.png` _(PNG-24)_ `.jpg` _(压缩率8-12)_
* 动态图片： `.gif`
* 压缩文件： `.tar.gz` `.zip`
```

xc-chain
├── package.json
├── dist/
├── build/
└── src/
    ├── assets/
    │   └── images/
    ├── components/
    │       ├── xc-card.vue
    │       └── xc-inclination.vue
    ├── plugins/
    │   ├── geetest.js
    │   └── hash-calc.js
    ├── router/
    │   └── index.js
    ├── services/
    │   ├── api.js
    │   └── news-api.js
    └── store/
        ├── constants.js
        ├── index.js
        └── mutation-types.js
```

## 二.HTML

### 2.1 语法
- 用两个空格来代替制表符（tab） -- 这是唯一能保证在所有环境下获得一致展现的方法。
- 嵌套元素应当缩进一次（即两个空格）。
- 标签及属性全部采用小写形式
- 对于属性的定义，确保全部使用双引号，绝不要使用单引号。
- 标签使用尽量遵循 HTML 标准和语义，但是不要以牺牲实用性为代价。任何时候都要尽量使用最少的标签并保持最小的复杂度。
- 不要在自闭合（self-closing）元素的尾部添加斜线(例如，`<meta>`或`<input>`) -- HTML5 规范中明确说明这是可选的。
- 不要省略可选的结束标签（closing tag）（例如，`</li>` 或 `</body>`）。
- `<img>`标签默认缺省格式：`<img src="xxx.png" alt="缺省时文字" />` 避免出现[src="" 问题]
- `<a>`标签缺省格式：`<a href="#" title="链接名称">xxx</>` 注：`target="_blank"` 根据需求决定
- 避免使用已过时标签，如：`<b>` `<u>` `<i>` 而用 `<strong>` `<em>`等代替
- 使用`data-xxx`来添加自定义数据，如：`<input data-xxx="yyy"/>`
- 避免使用`style="xxx:xxx;"`的内联样式表
```html
<!DOCTYPE html>
<html>
  <head>
    <title>Page title</title>
  </head>
  <body>
    <img src="images/company-logo.png" alt="Company">
    <h1 class="hello-world">Hello, world!</h1>
    <input type="text" placeholder="username">
  </body>
</html>
```

### 2.2 HTML5 doctype
为每个 HTML 页面的第一行添加标准模式（standard mode）的声明，这样能够确保在每个浏览器中拥有一致的展现。
```html
<!DOCTYPE html>
<html>
  <!-- ... -->
</html>
```

### 2.3 语言属性
根据 HTML5 规范：
> 强烈建议为 html 根元素指定 lang 属性，从而为文档设置正确的语言。这将有助于语音合成工具确定其所应该采用的发音，有助于翻译工具确定其翻译时所应遵守的规则等等。
```html
<html lang="zh-cn">
  <!-- ... -->
</html>
```

### 2.4 字符编码
通过明确声明字符编码，能够确保浏览器快速并容易的判断页面内容的渲染方式。这样做的好处是，可以避免在 HTML 中使用字符实体标记（character entity），从而全部与文档编码一致（一般采用 UTF-8 编码）。
```
<head>
  <meta charset="UTF-8">
</head>
```

### 2.5 IE 兼容模式
IE 支持通过特定的 <meta> 标签来确定绘制当前页面所应该采用的 IE 版本。除非有强烈的特殊需求，否则最好是设置为 edge mode，从而通知 IE 采用其所支持的最新的模式。
```html
<meta http-equiv="X-UA-Compatible" content="IE=Edge">
```

### 2.6 自定义标签建议使用中划线表示法
> eg:`my-btn`,`my-card`，`my-card-header`
```html
<my-card>
  <my-card-header>
    自定义标签
  </my-car-header>
  <my-card-content>
    <!-- ... -->
  </my-card-content>
</my-card>
```

## 三.CSS

### 3.1 语法
- 用两个空格来代替制表符（tab） -- 这是唯一能保证在所有环境下获得一致展现的方法。
- 为选择器分组时，将单独的选择器单独放在一行。
- 为了代码的易读性，在每个声明块的左花括号前添加一个空格。
- 声明块的右花括号应当单独成行。
- 每条声明语句的`:`后应该插入一个空格。
- 为了获得更准确的错误报告，每条声明都应该独占一行。
- 所有声明语句都应当以分号结尾。最后一条声明语句后面的分号是可选的，但是，如果省略这个分号，你的代码可能更易出错。
- 十六进制值应该全部小写，例如，`#fff`。在扫描文档时，小写字符易于分辨，因为他们的形式更易于区分。
- 尽量使用简写形式的十六进制值，例如，用 `#fff` 代替 `#ffffff`
- 为选择器中的属性添加双引号，例如，`input[type="text"]`。只有在某些情况下是可选的，但是，为了代码的一致性，建议都加上双引号。
- 避免为 0 值指定单位，例如，用`margin: 0;`代替`margin: 0px;`
```css
/* Bad CSS */
.selector, .selector-secondary, .selector[type=text] {
  padding:15px;
  margin:0px 0px 15px;
  background-color:rgba(0, 0, 0, 0.5);
  box-shadow:0px 1px 2px #CCC,inset 0 1px 0 #FFFFFF
}

/* Good CSS */
.selector,
.selector-secondary,
.selector[type="text"] {
  padding: 15px;
  margin-bottom: 15px;
  background-color: rgba(0,0,0,.5);
  box-shadow: 0 1px 2px #ccc, inset 0 1px 0 #fff;
}
```

#### 3.2 选择器
- 对于通用元素使用 class ，这样利于渲染性能的优化。
- 对于经常出现的组件，避免使用属性选择器（例如，[class^="..."]）。浏览器的性能会受到这些因素的影响。
- 选择器要尽可能短，并且尽量限制组成选择器的元素个数，建议不要超过 3 。
- 只有在必要的时候才将 class 限制在最近的父元素内（也就是后代选择器）（例如，不使用带前缀的 class 时 -- 前缀类似于命名空间）。
```css
/* Bad example */
span { ... }
.page-container #stream .stream-item .tweet .tweet-header .username { ... }
.avatar { ... }

/* Good example */
.avatar { ... }
.tweet-header .username { ... }
.tweet .avatar { ... }
```

#### 3.3 class命名
- class 名称中只能出现小写字符和破折号（dashe）（不是下划线，也不是驼峰命名法）。破折号应当用于相关 class 的命名（类似于命名空间）（例如，.btn 和 .btn-danger）。
- 避免过度任意的简写。.btn 代表 button，但是 .s 不能表达任何意思。
- class 名称应当尽可能短，并且意义明确。
- 使用有意义的名称。使用有组织的或目的明确的名称，不要使用表现形式（eg:`red`,`grey`等）和方位性（eg:`left`,`bottom`等）的名称。
- 基于最近的父 class 或基本（base） class 作为新 class 的前缀。
- 使用 .js-* class 来标识行为（与样式相对），并且不要将这些 class 包含到 CSS 文件中。
```css
/* Bad example */
.t { ... }
.red { ... }
.header { ... }

/* Good example */
.important { ... }
.tweet { ... }
.tweet-header { ... }
```

#### 3.4 避免在css中使用@import
与 `<link>` 标签相比，`@import` 指令要慢很多，不光增加了额外的请求次数，还会导致不可预料的问题。替代办法有以下几种：
- 使用多个 `<link>` 元素
- 通过 `Sass` 或 `Less` 类似的 CSS 预处理器将多个 CSS 文件编译为一个文件
- 通过 Rails、Jekyll 或其他系统中提供过 CSS 文件合并功能

## CSS, SCSS

* 使用soft tab（4个空格）。
* 每个属性声明末尾都要加分号。
* 注释统一用下面写法；缩进与下一行代码保持一致；可位于一个代码行的末尾，与代码间隔一个空格。

```css
/* element */
.element {
    position: absolute;
    top: 10px;
    left: 10px;
    border-radius: 10px;
    width: 50px;
    height: 50px;
}
```

> 切勿修改body的背景颜色来控制整个项目的背景颜色，如果项目中有其他子组件需要修改背景颜色，那么组件中无法修改body的背景颜色。

## js

代码缩进最好使用 4 个空格做为一个缩进层级。提交代码之前，使用快捷键 Ctrl+Alt+Shift+L 格式化代码。

* 标准变量采用驼峰式命名（除了对象的属性外）。
* 函数名采用驼峰式命名。
* 不要直接使用undefined进行变量判断，使用typeof和字符串'undefined'对变量进行判断。
* 在语句的行长度超过 120 时，根据逻辑条件合理缩进。
* 不同行为或逻辑的语句集，使用空行隔开，更易阅读。
* 对于 if...else...、try...catch...finally 等语句，推荐使用在 } 号后添加一个换行 的风格，使代码层次结构更清晰，阅读性更好。




```javascript


// 较复杂的逻辑条件组合，将每个条件独立一行，逻辑运算符放置在行首进行分隔，或将部分逻辑按逻辑组合进行分隔。
// 建议最终将右括号 ) 与左大括号 { 放在独立一行，保证与 `if` 内语句块能容易视觉辨识。
if (user.isAuthenticated()
    && user.isInRole('admin')
    && user.hasAuthority('add-admin')
    || user.hasAuthority('delete-admin')
) {
    // Code
}

// 按一定长度截断字符串，并使用 + 运算符进行连接。
// 分隔字符串尽量按语义进行，如不要在一个完整的名词中间断开。
// 特别的，对于 HTML 片段的拼接，通过缩进，保持和 HTML 相同的结构。
var html = '' // 此处用一个空字符串，以便整个 HTML 片段都在新行严格对齐
    + '<article>'
    +     '<h1>Title here</h1>'
    +     '<p>This is a paragraph</p>'
    +     '<footer>Complete</footer>'
    + '</article>';

// 也可使用数组来进行拼接，相对 `+` 更容易调整缩进。
var html = [
    '<article>',
        '<h1>Title here</h1>',
        '<p>This is a paragraph</p>',
        '<footer>Complete</footer>',
    '</article>'
];
html = html.join('');

// 当参数过多时，将每个参数独立写在一行上，并将结束的右括号 ) 独立一行。
// 所有参数必须增加一个缩进。
foo(
    aVeryVeryLongArgument,
    anotherVeryLongArgument,
    callback
);

// 也可以按逻辑对参数进行组合。
// 最经典的是 baidu.format 函数，调用时将参数分为“模板”和“数据”两块
baidu.format(
    dateFormatTemplate,
    year, month, date, hour, minute, second
);

// 当函数调用时，如果有一个或以上参数跨越多行，应当每一个参数独立一行。
// 这通常出现在匿名函数或者对象初始化等作为参数时，如 `setTimeout` 函数等。
setTimeout(
    function () {
        alert('hello');
    },
    200
);

order.data.read(
    'id=' + me.model.id,
    function (data) {
        me.attchToModel(data.result);
        callback();
    },
    300
);

// 链式调用较长时采用缩进进行调整。
$('#items')
    .find('.selected')
    .highlight()
    .end();

// 三元运算符由3部分组成，因此其换行应当根据每个部分的长度不同，形成不同的情况。
var result = thisIsAVeryVeryLongCondition
    ? resultA : resultB;

var result = condition
    ? thisIsAVeryVeryLongResult
    : resultB;

// 数组和对象初始化的混用，严格按照每个对象的 `{` 和结束 `}` 在独立一行的风格书写。
var array = [
    {
        // ...
    },
    {
        // ...
    }
];
```


* 文件顶部必须包含文件注释，用 @file 标识文件说明。
* 文件注释中可以用 @author 标识开发者信息。

```JavaScript
/**
 * @file Describe the file
 * @author author-name(mail-name@domain.com)
 *         author-name2(mail-name2@domain.com)
 */
```


## 代码提交规范

###### commit 信息

提交信息主要分为三种：

* feature:新增内容
* enhancement:改变内容
* bug:修复内容


> 要求内容中清楚的写明本次提交中所有的更改。

> 代码缩进最好使用 4 个空格做为一个缩进层级。提交代码之前，使用快捷键 Ctrl+Alt+Shift+L 格式化代码。


## vue项目文件


#### 组件命名规范

 组件在components下面新建文件夹
 名字以x_开头

> 例：x_login > index.vue
