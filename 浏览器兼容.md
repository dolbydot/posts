### 什么是 CSS hack
**CSS hack**是一个编程技术，指根据浏览器的版本、功能来隐藏或显示CSS标记语言。也用来在多个渲染效果不同的浏览器中取得一致的表现。
由于不同的浏览器及相同浏览器不同的版本和标准之间（比如IE6,IE7,Mozilla Firefox等）对CSS行为的解释以及W3C标准的支持不同而导致生成的页面效果不一样，得不到我们所需要的页面效果。 这时我们就需要针对不同的浏览器去写不同的CSS，让它能够同时兼容不同的浏览器，得到我们想要的页面效果。 
这个针对不同的浏览器写不同的CSS code的过程，就叫CSS hack。

### 谈一谈浏览器兼容的思路
1. 要不要做
产品的角度（产品的受众、受众的浏览器比例、效果优先还是基本功能优先）
成本的角度 (有无必要做某件事)

2. 做到什么程度
让哪些浏览器支持哪些效果

3.  如何做
- 根据兼容需求选择技术框架/库(如jquery 1.x.x)
- 根据兼容需求选择兼容工具：
[html5shiv](https://zhuanlan.zhihu.com/html5shiv)、[Respond.js](http://link.zhihu.com/?target=https%3A//github.com/scottjehl/Respond)、[CSS Reset](http://link.zhihu.com/?target=https%3A//segmentfault.com/a/1190000003021766)、[normalize.css](http://link.zhihu.com/?target=https%3A//github.com/necolas/normalize.css)、[Modernizr.js](http://link.zhihu.com/?target=https%3A//github.com/Modernizr/Modernizr)、 [postcss](http://link.zhihu.com/?target=https%3A//github.com/postcss/postcss)
- 条件注释、CSS Hack、js 能力检测做一些修补

### 列举5种以上浏览器兼容的写法 
- 合适的框架
```
Bootstrap (>=ie8)
jQuery 1.~ (>=ie6), jQuery 2.~ (>=ie9)
Vue (>= ie9)
```
- 清除浮动
```
.clearfix::after{
    content: '';
    display: block;
    clear: both;
}
.clearfix{
    /*  仅对IE6/7有效，zoom:1;触发hasLayout，起到类似BFC的效果  */
      *zoom: 1;      
}
```
- 生成行内块框
```
.target{
  display: inline-block;
  *display: inline; /*仅对ie67生效*/
  *zoom: 1; /*仅对ie67生效*/
}
```
- 条件注释引入shiv、respond脚本
```
<!--[if lt IE 9]>
    <script src="https://oss.maxcdn.com/html5shiv/3.7.3/html5shiv.min.js"></script>
    <script src="https://oss.maxcdn.com/respond/1.4.2/respond.min.js"></script>
<![endif]-->
```
- 条件注释
```
<!--[if IE 6]>
<p>You are using Internet Explorer 6.</p>
<![endif]-->
```
- 属性前缀
```
.box{
     color: red;  /*所有浏览器都支持*/
     color:red !important;   ⁄* Firefox、IE7支持 *⁄
     _color: blue; /*ie6支持*/
    *color: pink; /*ie6、7支持*/
     color: yellow\9;  /*ie/edge 6-8*/
}
```

### 以下工具/名词是做什么的
- 条件注释：
条件注释 (conditional comment) 是于HTML源码中被IE有条件解释的语句。条件注释可被用来向IE提供及隐藏代码。使用了条件注释的页面在 Windows IE 9 中可正常工作，但在 IE 10 中无法正常工作。 [IE10不再支持条件注释](https://msdn.microsoft.com/zh-cn/library/ie/hh801214(v=vs.85).aspx)。
- IE Hack：
针对IE浏览器编写不同的CSS的让IE能够正常渲染的过程。
使用特殊的符号或者方式写出只有IE浏览器可以解析的代码，有CSS属性前缀法、选择器前缀法以及IE条件注释法。
1、CSS属性前缀法： 比如IE6能识别下划线和星号，IE7能识别星号 ，但不能识别下划线，而firefox两个都不能认识。
2、选择器前缀法： 比如IE6能识别`html .class{}`，IE7能识别`+html .class{}`或者`*:first-child+html .class{}`。
3、HTML头部引用(if IE)Hack：针对所有IE：`<!--[if IE]><![endif]-->`，针对IE6及以下版本：`<!--[if lt IE 7]><![endif]-->`，这类Hack不仅对CSS生效，对写在判断语句里面的所有代码都会生效。
5、书写顺序： 一般是将识别能力强的浏览器的CSS写在前面。浏览器优先级别：FF < IE7 < IE6，CSS hack书写顺序一般为FF IE7 IE6。

- js 能力检测：
检测浏览器是否支持某种特定的能力，然后给出特定的解决方案。

- html5shiv.js：
用于解决IE9以下版本浏览器对HTML5新增标签不识别导致CSS不起作用的脚本。

- respond.js：
respond.js 是一个快速、轻量的 polyfill，用于为 IE6-8 以及其它不支持 CSS3 Media Queries 的浏览器提供媒体查询的 `min-width` 和 `max-width` 特性，实现响应式网页设计（Responsive Web Design）。

- css reset：
早期的CSS Reset用来清除所有浏览器默认样式，这样更易于保持各浏览器渲染的一致性。但
暴力清零带来如下问题：
1.*{ margin:0; padding:0; }会带来性能问题
2.使用通配符存在隐性问题
3.过渡的标签重置等于画蛇添足
4.过渡的标签重置导致语言元素失效

- normalize.css：
可定制的 CSS 文件，使浏览器呈现的所有元素更一致和符合现代标准；是在现代浏览器环境下对于CSS reset的替代。
依赖于研究浏览器默认元素风格之间的差异，精确定位需要重置的样式。相比CSS Reset，Normalize.css是一种为HTML5准备的优质替代方案。Normalize.css现在已经被用于Twitter Bootstrap、HTML5 Boilerplate、GOV.UK、Rdio、CSS Tricks 以及许许多多其他框架、工具和网站上。
作用：
1.保护有用的浏览器默认样式而不是完全去掉它们
2.为大部分HTML元素提供一般化的样式
修复浏览器自身的bug并保证各浏览器的一致性
3.用一些小技巧优化CSS可用性
4.用注释和详细的文档来解释代码

- Modernizr：
Modernizr.js既能给老版本浏览器打补丁，又能保证新浏览器渐进增强的用户体验。
Modernizr是一个检测用户浏览器HTML5和CSS3能力的JavaScript库。Modernizr在页面加载时快速运行来检测功能，然后创建一个保存检测结果的JavaScript对象，接着页面中的html标签上添加一系列class属性来接通你的CSS。Modernizr支持大量的测试和可选地包括YepNope.js来视情况加载外部的js和css资源。

- postCSS：
一个使用 JS 插件来转换 CSS 的工具。这些插件可以支持使用变量，混入(mixin)，转换未来的 CSS 语法，内联图片等操作。PostCSS使CSS变成JavaScript的数据，使它变成可操作。PostCSS是基于JavaScript插件，然后执行代码操作。PostCSS自身并不会改变CSS，它只是一种插件，为执行任何的转变铺平道路。

### 一般在哪个网站查询属性兼容性？
[Can I use?](http://caniuse.com/)

**参考资料**：
- [*聊一聊浏览器兼容*](https://zhuanlan.zhihu.com/p/24413264)
- [*CSS hack*](https://site.douban.com/196754/widget/notes/11827403/note/253661846/)