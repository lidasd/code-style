# 前端开发规范

## 命名规则

#### 项目命名

全部采用小写方式， 以下划线分隔。
> 例：my_project_name

#### 目录命名
全部采用小写方式， 以下划线分隔。
有复数结构时，要采用复数命名法。
> 例：scripts, styles, images, data_models

#### JS文件命名
全部采用小写方式， 以下划线分隔。

> 例：account_model.js

#### CSS, SCSS文件命名
类名使用小写字母，以下划线分隔
id采用驼峰式命名
scss中的变量、函数、混合、placeholder采用驼峰式命名

> 例：retina_sprites.scss

#### HTML文件命名
全部采用小写方式， 以下划线分隔。

> 例：error_report.html

#### vue组件名称
全部采用驼峰命名

> 例：errorReport.vue

## HTML

#### 代码风格

* 使用 4 个空格 或 tab 字符做为一个缩进层级。
* 同一页面，应避免使用相同的 name 与 id。
* 标签名必须使用小写字母。
* HTML 标签的使用应该遵循标签的语义。
* 属性名必须使用小写字母。
* 自定义属性建议以 data- 为前缀。
* 使用 HTML5 的 doctype 来启用标准模式，建议使用大写的 DOCTYPE
* 在 html 标签上设置正确的 lang 属性。如：lang="zh-cn"。
* 页面必须使用精简形式，明确指定字符编码。指定字符编码的 meta 必须是 head 的第一个直接子元素。
* 引入 CSS 时必须指明 rel="stylesheet"。
* 在 head 中引入页面需要的所有 CSS 资源。
* JavaScript 应当放在页面末尾，或采用异步加载。
* 页面必须包含 title 标签声明标题。 title 必须作为 head 的直接子元素，并紧随 charset 声明之后。
*  禁止 img 的 src 取值为空。延迟加载的图片也要增加默认的 src。

```HTML
<html lang="zh-CN">
    <head>
        <meta charset="UTF-8">
        <title>页面标题</title>
        <link rel="shortcut icon" href="favicon.ico">
        <link rel="stylesheet" href="page.css">
        ......
    </head>
    <style>
      .buttons .button-group {
        float: right;
      }
    </style>

    <body>
        ......
    </body>
    <script src="init-behavior.js"></script>
</html>
```



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
