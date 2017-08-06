###  1. CSS的全称是什么?
Cascading Style Sheets, 层叠样式表。

----------
###  2. @charset有什么作用
告诉浏览器使用什么字符集去解码。

----------
###  3. 以下这几种文件路径分别用在什么地方，代表什么意思?

 - `css/a.css`:相对路径-当前目录下css文件夹内a.css文件。
 - `./css/a.css`：相对路径-当前目录下css文件夹内a.css文件。
 - `b.css`：相对路径-当前目录下b.css文件。
 - `../imgs/a.png`：相对路径-上级目录下imgs文件夹a.png文件。
 - `/Users/hunger/project/css/a.css`：绝对路径-从根目录向下直到a.css文件。
 - `/static/css/a.css`：绝对路径-从根目录向下直到a.css文件。
 - `http://cdn.jirengu.com/kejian1/8-1.png`：网站路径-http服务提供的图片地址。

----------
###  4. id选择器和class选择器的使用场景分别是什么？

 - id选择器：每个id在文档中必须是唯一的且一个标签只能绑定一个id。所以id选择器通常用于大的模块上，多用于父级。
 - class选择器：文档中多个元素可以拥有一个类名且一个标签可以绑定多个class。所以class选择器通常用于重复使用率高的元素上，多用于子级。

----------
###  5. CSS常见选择器、伪类选择器和伪元素。
详见 [My Github](https://github.com/dolbydot/demos/blob/master/CSS-Selector.html)

----------
###  6. 下列代码是什么意思？
`.item+p {color: red}`:使class="item"的元素的子元素p的下一相邻元素字色为红色。
`.item~p {color: yellow}`:使class="item"的元素的子元素p的下N个相邻元素字色为黄色。
`.item p {color: blue}`:使class="item"的元素的子元素p字色为蓝色。
`p.item {color: blue}`:使p元素的后代class="item"的元素字色为蓝色。
`.item>p{color: blue}`:使父元素为class="item"的直接子元素p字色为蓝色。

----------
###  7. em、rem分别是什么？
**em：**
相对长度单位，表示元素的font-size的计算值，代表了默认字体大小的倍数(比如不设置时是字体是16px，那2em 就是32px)。
常用于创建可伸缩布局，这样即便用户更改了字体尺寸也不影响页面整体布局。CSS属性line-height，font-size，margin-bottom和margin-top常具有一个用em表示的值。

**rem：**
代表根元素（如`<html>`）font-size大小，当用在根元素的font-size上面时，它代表了它的初始值，默认初始值是html默认font-size大小。
当未在根元素上设置font-size大小时,1rem=1em,当设置font-size=2rem的时候,就使得页面中1rem的大小相当于html的根字体默认大小的2倍,当然此时页面中字体的大小也是html的根字体默认大小的2倍)。
该单位在实际使用中一般用于创建完美的可扩展布局。如果不被目标浏览器支持，可以使用em单位。IE8及之前版本不支持rem。

----------
###  8. 颜色有几种写法？
```
color:直接写颜色名，如：red;
color:#000000---#ffffff;
color:#000---#fff;
color:rgb(0,0,0);---rgb(255,255,255);
color:rgb(0%,0%,0%);---rgb(100%,100%,100%)
```

----------
###  9. CSS 选择器的权重是如何计算的？
以下为亲测结果：
**优先级从高到低**排列为：
1. head元素中!important
2. body元素中inline style内联样式（行内样式）
3. head元素中id选择器（无论这个id声明放在class选择器上面还是下面）
4. head元素中class选择器（同一个body元素内应用到两个及以上的class，无论body中class值如何排序，head元素中靠内的class选择器优先级高于靠外的class选择器）
5. head元素中tag标签选择器
6. css外部样式表
7. body标签内style样式
8. 浏览器缺省设置(即默认样式)

**计算方式：
选择器的特殊性由选择器本身决定，出现冲突时，高特殊性的声明胜出。
对于复杂场景，可以使用特殊值来计算优先级，特殊性值表述为4个部分：0，0，0，0，计算规则如下：
ID —— +0，1，0，0
类、属性选择、伪类 —— +0，0，1，0
元素、伪元素 —— +0，0，0，1
所有内联属性 —— +1，0，0，0
对于得到的值，相同位置上的数字越大的值代表的优先级越高；不同的位置按从前到后优先级依次降低，即 0，1，0，0 的优先级比 0，0，1，15 更高。
越是“特殊”的选择器优先级越高，具有相同优先级的选择器，如果样式出现冲突，那么后出现的样式会覆盖先出现的样式。

----------
###  10. 如何在js.jirengu.com上展示一个图片?
定制图片操作：[示例](https://dolbydot.github.io/demos/form.html)
将图片xxx.ico放在代码当前目录下，按如下配置来生成地址栏左侧图标：
```
<link rel="shortcut icon" href="xxx.ico" type="image/x-icon">
```
其中shortcut icon特指浏览器中地址栏左侧显示的图标，一般大小位16*16，后缀名为.icon。href的值为图片链接。

----------
###  11. 列出5条以上html和css的书写规范。
html书写规范：

 - 遵循语义化标准但注重实用性，避免多余的父节点，以较小复杂度和较少的标签解决问题。
 - 在页面开头用doctype来启用标准模式，使其在每个浏览器中尽可能一致的展现，照惯例DOCTYPE大写。
 - 在html标签上加上lang属性。这会告诉语音工具和翻译工具应怎么去发音和翻译。
 - 指定`<meta charset="UTF-8">`，让浏览器轻松渲染并减少乱码的可能。
 - 嵌套的节点需缩进以保持结构工整。
 - 属性名全小写。
 - 属性值使用双引号。
 - 除自闭合标签外所有标签都应成对出现。

css书写规范：

 - 选择器内的属性值对要使用缩进。
 - 不使用内联样式。
 - 使用有意义的单词作为选择器名称。
 - 每个属性声明属性名后加空格，属性值末尾要加分号。
 - 注释统一用/* */，缩进与下一行代码保持一致。
 - 最外层统一使用双引号，url的内容要用引号，属性值要用引号。
 - 类名使用小写字母以中划线分隔，id采用驼峰式命名。
 - 十六进制颜色名用小写字母且能简写一定简写。
 - 属性值0后不要加单位。

----------
###  12. 截图介绍 chrome 开发者工具的功能区
右键打开开发者工具：

![元素面板](http://upload-images.jianshu.io/upload_images/6851923-892e3c4dea848de7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![样式区](http://upload-images.jianshu.io/upload_images/6851923-491798e00985e5d8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![事件监听区、DOM断点区](http://upload-images.jianshu.io/upload_images/6851923-21013f64a18036b6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![元素属性区](http://upload-images.jianshu.io/upload_images/6851923-e88dd184aee341aa.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![控制台](http://upload-images.jianshu.io/upload_images/6851923-72718c260c0ceaae.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![资源面板](http://upload-images.jianshu.io/upload_images/6851923-7a5a43d993e7affb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![网络面板](http://upload-images.jianshu.io/upload_images/6851923-64539a7d70cd71dd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![性能面板](http://upload-images.jianshu.io/upload_images/6851923-8ffcf8d7d536b808.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
