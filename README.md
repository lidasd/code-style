# 前端开发规范
此为前端开发团队遵循和约定的代码书写规范，意在提高代码的规范性和可维护性。  
此规范为参考规范，不全是硬性要求。旨在统一团队编码规范和风格，让所有代码都是有规可循的，并且能够得到沉淀，减少重复劳动。

## 黄金定律
永远遵循同一套编码规范 -- 可以是这里列出的，也可以是你自己总结的。如果你发现本规范中有任何错误，敬请指正。
> 不管有多少人共同参与同一项目，一定要确保每一行代码都像是同一个人编写的。

## 目录
- [一.文件及文件夹](#一文件及文件夹)
- [二.HTML](#二HTML)
  * [2.1 语法](#21-语法)
  * [2.2 HTML5 doctype](#22-html5-doctype)
  * [2.3 语言属性](#23-语言属性)
  * [2.4 字符编码](#24-字符编码)
  * [2.5 IE 兼容模式](#25-ie-兼容模式)
  * [2.6 自定义标签及组件](#26-自定义标签及组件)
- [三.CSS](#三css)
  * [3.1 语法](#31-语法)
  * [3.2 选择器](#32-选择器)
  * [3.3 class命名](#33-class命名)
  * [3.4 避免在css中使用@import](#34-避免在css中使用@import)
- [四.JavaScript](#四javascript)
  * [4.1 语法](#41-语法)
  * [4.2 变量命名](#42-变量命名)
  * [4.3 注释使用](#43-注释使用)
- [五.代码提交规范](#五代码提交规范)
  * [5.1 规范](#51-规范)
  * [5.2 commit message格式](#52-commit-message格式)
    * [5.2.1 Header](#521-header)
    * [5.2.2 Body](#522-body)
    * [5.2.3 Footer](#523-footer)
    * [5.2.4 Revert](#524-revert)
- [六.编辑器配置](#六编辑器配置)



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

### 2.6 自定义标签及组件
* 自定义标签及组件建议使用中划线表示法
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


## 四.JavaScript

### 4.1 语法
* 用两个空格来代替制表符（tab） -- 这是唯一能保证在所有环境下获得一致展现的方法。
* 为了便于阅读每行字符建议小于数 80 个。如果一个 JavaScript 语句超过了 80 个字符，建议在运算符或者逗号后换行。
* 对于大段代码块，根据不同行为或逻辑，建议拆分成不同函数，也可以使用一定的空行隔开，必要时增加相应的注释。
* 一条语句通常以分号作为结束符。
* 复杂语句的通用规则:
> * 将左花括号放在第一行的结尾。  
> * 左花括号前添加一空格。  
> * 将右花括号独立放在一行。  
> * 不要以分号结束一个函数声明。  
```javascript
function getUserInfo() {
  // 函数声明
  // ...
}   // <- 末尾不要加分号,因为函数声明中 } 就是一个完整的语句结束符，添加分号相当于增加了一条没有任何代码的空语句

var getUserInfo = function() {
    // 函数表达式
};  // <- 末尾增加分号，函数表达式和其它表达式一个道理，类似于var i=0这样的，加不加分号都行，如果没加js会自动帮你加上的，让js帮你加分号，是一种危险的行为，具体细节自行百度,Google  JS自动填写分号导致的坑

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

// 数组和对象初始化的混用，数组开始`[`和结束`]`在单独的行书写，对象开始 `{` 和结束 `}` 根据对象字段的多少来确定是否有必要在独立一行的风格书写。
//对象字段较少
var users = [
  {id: 1, name: 'Tom', age: 6},
  {id: 2, name: 'Jerry', age: 5}
]
//对象字段较多
var array = [
  {
    // ...
  },
  {
    // ...
  }
];
```

### 4.2 变量命名
*  **遵循当前语言的变量命名规则。** 
*  **变量名推荐使用驼峰法来命名(camelCase)。** e.g.`firstName`,`lastName`,`price`。
*  **采用有意义的命名。** 变量的名字必须准确反映它的含义和内容，你可以通过"userInfo"知道该变量保存的是用户信息，但你不能通过"a", "b"知道变量保存的是什么
*  **根据不同使用目的的变量使用不同变量名。** 这同样对保持可读性和可维护性很重要。
*  **变量名不要使用非ASCII字符（non-ASCII chars）。** 这样做可能会在跨平台使用时产生问题。
*  **不要使用过长的变量名（例如50个字符）。** 
*  **不同的代码段采用不同的命名长度。** 通常来说，循环计数器（loop counters）采用1位的单字符来命名，循环判断变量（condition/loop variables）采用1个单词来命名，方法采用1-2个单词命名，类采用2-3个单词命名，全局变量采用3-4个单词命名
*  **使用有意义的方法参数命名** ，这样做可以在没有文档的情况下尽量做到"自解释（documentate itself）"。


### 4.3 注释使用
* 对于注释的使用可参考JSDoc[中文文档](http://www.css88.com/doc/jsdoc/index.html)  [英文文档](http://usejsdoc.org/)
* 若有必要对整个文件进行注释应保持以下风格
```javascript
/**
 * @module Core模块  模块描述声明
 * @date 2017-12-10 日期
 * @version 1.0.0   版本号
 * @author Scott<scott@gmail.com>     作者1信息
 *         author<author@hotmail.com> 作者2信息
 */
```
* 方法注释风格
```javascript
/**
 * 函数功能简述
 * @param  {string}   address        地址
 * @param  {array}    com            商品数组
 * @param  {string}   pay_status     支付方式
 * @returns  void
 */
```

## 五.代码提交规范
### 5.1 规范
* commit的message必须填写
* 提交只提交必要的变动，确保提交影响范围尽可能小

### 5.2 commit message格式
每次提交，Commit message 都包括三个部分：header，body 和 footer。
```
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```
其中，header 是必需的，body 和 footer 可以省略。
不管是哪一个部分，任何一行都不得超过72个字符（或100个字符）。这是为了避免自动换行影响美观。

#### 5.2.1 Header

 **type**  
type用于说明 commit 的类别，只允许使用下面7个标识。

- feat：新功能（feature）
- fix：修补bug
- docs：文档（documentation）
- style： 格式（不影响代码运行的变动）
- refactor：重构（即不是新增功能，也不是修改bug的代码变动）
- test：增加测试
- chore：构建过程或辅助工具的变动

 **scope**  
用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同。

例如在Angular，可以是$location, $browser, $compile, $rootScope, ngHref, ngClick, ngView等。
如果你的修改影响了不止一个scope，你可以使用*代替。


 **subject**  
是 commit 目的的简短描述，不超过50个字符。

其他注意事项：  
以动词开头，使用第一人称现在时，比如change，而不是changed或changes  
第一个字母小写  
结尾不加句号（.）  

#### 5.2.2 Body

Body 部分是对本次 commit 的详细描述，可以分成多行。有以下两点需要注意：  
- 永远别忘了第2行是空行
- 应该说明代码变动的动机，以及与以前行为的对比。

#### 5.2.3 Footer

Footer 部分只用于以下两种情况：  

 **不兼容变动** 

如果当前代码与上一个版本不兼容，则 Footer 部分以BREAKING CHANGE开头，后面是对变动的描述、以及变动理由和迁移方法。

```
BREAKING CHANGE: isolate scope bindings definition has changed.

    To migrate the code follow the example below:

    Before:

    scope: {
      myAttr: 'attribute',
    }

    After:

    scope: {
      myAttr: '@',
    }

    The removed `inject` wasn't generaly useful for directives so there should be no code using it.
```

 **关闭 Issue** 

如果当前 commit 针对某个issue，那么可以在 Footer 部分关闭这个 issue 。
```
Closes #234
```

#### 5.2.4 Revert 
还有一种特殊情况，如果当前 commit 用于撤销以前的 commit，则必须以revert:开头，后面跟着被撤销 Commit 的 Header。
```
revert: feat(pencil): add 'graphiteWidth' option

This reverts commit 667ecc1654a317a13331b17617d973392f415f02.
```
Body部分的格式是固定的，必须写成This reverts commit `<hash>`.，其中的`<hash>`是被撤销 commit 的 SHA 标识符。


## 六.编辑器配置
将你的编辑器按照下面的配置进行设置，以避免常见的代码不一致和差异：

- 用两个空格代替制表符（soft-tab 即用空格代表 tab 符）。
- 保存文件时，删除尾部的空白符。
- 设置文件编码为 UTF-8。
- 在文件结尾添加一个空白行。

参照文档并将这些配置信息添加到项目的`.editorconfig`文件中。例如：[.editorconfig](.editorconfig)。