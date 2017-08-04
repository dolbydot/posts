2/22/2017 10:26:28 PM 
## 联网状态下代码高亮步骤： ##
单击左下角“M”标志，选择GFM，在代码开始标志“```”后面加入代码类型，如“html/css/js”


## CSS ##

#### Q1:当同一个 HTML 元素被不止一个样式定义时，会使用哪个样式呢？ ####
A:一般而言，所有的样式会根据下面的规则层叠于一个新的虚拟样式表中：
**优先级从高到低**排列为：
1. head元素中!important
2. body元素中inline style内联样式（行内样式）
3. head元素中id选择器（无论这个id声明放在class选择器上面还是下面）
4. head元素中class选择器（同一个body元素内应用到两个及以上的class，无论body中class值如何排序，head元素中靠内的class选择器优先级高于靠外的class选择器）
5. head元素中tag标签选择器
6. css外部样式表
7. body标签内style样式
8. 浏览器缺省设置(即默认样式)
*如：*
```html
<head>
<style type="text/css">
	.bgc1{background-color: #F00 !important;}
	#bgc{background-color: #00F;}
	.bgc2{background-color: #0F0;}
</style>
</head>
<body style="background-color: yellow">
<p class="bgc2 bgc1" id="bgc" style="background-color: #000">背景颜色</p>
</body>
```
显示效果如下图：
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-30977c8b6824eda3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

----------
#### CSS语法 ####
CSS 规则由两个主要的部分构成：选择器，以及一条或多条声明。
CSS 对大小写不敏感。不过存在一个例外：如果涉及到与HTML文档一起工作的话，class和id名称对大小写是敏感的。
***格式：***
```html
h1{color:red; font-size:14px;font-family: Georgia, Palatino, serif;}
```

**如果值为若干单词，则要给值加引号：**
```html
p{font-family:"sans serif";}
```

**选择器分组：**
```html
h1,h2,h3,h4,h5,h6 {color: green;}
```

**继承：**
如果不希望 "Verdana, sans-serif" 字体被所有的子元素继承，又要照顾忽略继承和body元素规则的浏览器，可以单独为这些子元素创建特殊规则。
```html
body{font-family: Verdana, sans-serif;}

td, ul, ol, ul, li, dl, dt, dd{font-family: Verdana, sans-serif;}

p{font-family: Times, "Times New Roman", serif;}
```

**派生选择器：**
根据文档的上下文关系来确定某个标签的样式。
```html
<head>
<style>
li strong {
    font-style: italic;
    font-weight: normal;
  }
</style>
</head>
<body>
<p><strong>我是粗体字，不是斜体字，因为我不在列表当中，所以这个规则对我不起作用</strong></p>

<ol>
<li><strong>我是斜体字。这是因为 strong 元素位于 li 元素内。</strong></li>
<li>我是正常的字体。</li>
</ol>
</body>
```
显示效果如下图：
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-38060054e751e5e2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**id选择器：**
一个页面可以有很多不同的id选择器，但一个id 属性只能在每个 HTML 文档中出现一次。
```html
<style>
#red {color:red;}
#green {color:green;}
</style>
<body>
<p id="red">这个段落是红色。</p>
<p id="green">这个段落是绿色。</p>
</body>
```
即使被标注为 sidebar 的元素只能在文档中出现一次，这个 id 选择器作为派生选择器也可以被使用很多次：
```html
#sidebar p {
	font-style: italic;
	text-align: right;
	margin-top: 0.5em;
	}

#sidebar h2 {
	font-size: 1em;
	font-weight: normal;
	font-style: italic;
	margin: 0;
	line-height: 1.5;
	text-align: right;
	}
```
在这里，与页面中的其他 p 元素明显不同的是，sidebar 内的 p 元素得到了特殊的处理，同时，与页面中其他所有 h2 元素明显不同的是，sidebar 中的 h2 元素也得到了不同的特殊处理。
**类选择器**
- 格式一
```html
<style>
.center {text-align: center}
</style>
<body>
<h1 class="center">类选择器</h1>
</body>
```
- 格式二
```html
<style>
td.fancy {color: #f60;background: #666;}
</style>
<body>
<td class="fancy">
</body>
```
注意：类名的第一个字符不能使用数字！它无法在 Mozilla 或 Firefox 中起作用。
**属性选择器**
可以为拥有指定属性的 HTML 元素设置样式,在为不带有 class 或 id 的表单设置样式时特别有用。
- 格式一
```html
<style>
[title]
{
color:red;
}
</style>
```
- 格式二
```html
<style>
[title="W3School"]
{
border:5px solid blue;
}
</style>
```
- 格式三
```html
<style>
input[type="text"]
{
  width:150px;
  display:block;}
input[type="button"]
{
  width:120px;
  margin-left:35px;}
</style>
<body>
<form name="input" action="" method="get">
<input type="text" name="Name" value="Gates" size="20">
<input type="button" value="Example Button">
</form>
</body>
```

----------
#### 颜色： ####
Hexadecimals（或hex）是十六进制数字，符号 0-9代表数值零到九，再使用A、B、C、D、E、F 代表数值十到十五。即用**0到F可为我们提供16个可能的数值**。
16个值和6个位置意味着我们有16的6次方，即超过1600万种可能的颜色。

Hex code遵循rgb（红-绿-蓝）格式。
- 前两位代表红色的数量（红色：#FF0000）
- 第三四位代表绿色的数量（绿色：#00FF00）
- 第五六位代表蓝色的数量（蓝色：#0000FF）
- 平均混合的颜色可缩短为三位（红色#F00）
**属性:值；**
三种写法
```
color:#000---#fff;
color:rgb(0,0,0);---rgb(255,255,255);
color:rgb(0%,0%,0%);---rgb(100%,100%,100%)
```
----------
#### 正则表达式 ####
**a{1,4}**
a
aa
aaa
aaaa

**[fa|ba|ca|fafdafsaf]**
fa
ba
ca
fafdafsaf

**ab{0,1}cde{0,1}f{0,1}g**
或**ab?cde?f?g**
acdefg
abcdfg
abcdeg
abcdg
acdeg
acdfg
acdg

----------
## HTML ##
#### 格式 ####
```html
<form id="form" action="form.php" method="post" style="font-size:25px;background-color:red;">
</form>
```
----------
#### pre标签 ####
html中对空格不敏感。pre元素可定义预格式化的文本，被包围在pre元素中的文本通常会保留空格和换行符，而文本也会呈现为等宽字体。
pre标签的一个常见应用就是用来表示计算机的源代码。
可以导致段落断开的标签（例如标题、p和address标签）绝不能包含在pre所定义的块里。
属性="值"：width="number"，描述：定义每行的最大字符数（通常是40、80或132）
*如：*
```html
<pre>
   鹅鹅鹅
曲项向天歌
		            白  毛浮绿   水
		            红掌拨清
		            波
</pre>
```
显示效果如下图：
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-016c75afb148bbb8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

----------
#### abbr标签 ####
abbr标签指示简称或首字母缩写
属性="值"：title="全拼"
```html
<abbr title="etcetera">etc.</abbr>
<br />
<abbr title="World Wide Web">WWW</abbr>
```
显示效果如下图：鼠标移到文本区域会显示完整的单词或句子。
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-219af4a5fd77648f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-f880d4af54321884.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

----------
#### bdo标签 ####
bdo 元素可覆盖默认的文本方向
属性="值"：dir="ltr/rtl"，定义文字的方向。
```html
<bdo dir="rtl">Here is some Hebrew text</bdo>
```
显示效果如下图：
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-d8032d018890de7f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
#### 做一个表单 ####
```html
<!DOCTYPE html>
<html>
<head>
	<title>登录注册</title>
</head>
<body>
<form id="form" action="form.php" method="post" enctype="multipart/form-data">
<fieldset>
	<legend>用户</legend>
	<input id="hiddenField" type="hidden" name="hiddenField" value="hiddenvalue"/>
	<label for="username">用户：</label>
	<input id="username" type="text" name="username" value="" size="15" maxlength="25"/>
	<br/>
	<label for="pass">密码：</label>
	<input id="password" type="password" name="pass" value="" size="15" maxlength="25"/>
</fieldset>

	<fieldset>
		<legend>性别</legend>
		<label for="sex">基佬</label>
		<input id="sex" type="radio" value="1" name="sex"/>
		<label for="sex">同志</label>
		<input id="sex" type="radio" value="2" name="sex"/>
		<label for="sex">玻璃</label>
		<input id="sex" type="radio" value="3" name="sex"/>
	</fieldset>

	<fieldset>
		<legend>爱好</legend>
		<label for="fav">吃饭</label>
		<input id="fav" type="checkbox" value="1" name="fav"/>
		<label for="sex">睡觉</label>
		<input id="fav" type="checkbox" value="2" name="fav"/>
		<label for="sex">打豆豆</label>
		<input id="fav" type="checkbox" value="3" name="fav"/>
		<label for="sex">自闭症</label>
		<input id="fav" type="checkbox" value="4" name="fav"/>
	</fieldset>
<fieldset>
	<legend>靓照</legend>
	<label for="myimage">照片上传</label>
	<input id="myimage" type="file" value="" name="myimage" size="35" maxlength="255"/>
</fieldset>
<fieldset>
	<legend>提交</legend>
	<input id="submit" type="submit" value="提交" name="submit"/>
	<input id="reset" type="reset" value="重置" name="reset"/>
</fieldset>
</form>
</body>
</html>
```
显示效果如下图：
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-3887be652fce47ac.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

----------
#### 块级元素： ####
    <div></div>
    <p></p>
    <h></h>
    <ul></ul>
    <table></table>
    <dt></dt>

1. `<p>`内不能嵌套任何块级元素，`<h>`不能嵌套自身和其他`<h>`，`<dt>`不能嵌套自身（嵌套自身显示网页效果没有问题，但在网页上按"ctrl+shift+c"查看源代码是有问题的）；内联元素不能嵌套块级元素，只能包含其他内联元素；块元素可以包含内联元素和某些特定的块元素。
`<p><div></div></p>`—— 错
`<span><div></div></span>` —— 错
`<div><p></p></div>`—— 对
`<div><div><p></p></div></div>`—— 对
`<div><h1></h1><p></p></div>` —— 对
`<a href=http://www.cnblogs.com/jyybeam/p/"#">` —— 对
`<p><p></p></p>`—— 错
`<h2><h2></h2></h2>`—— 错
`<h2><h3></h3></h2>`—— 错
`<p><h2></h2></p>`—— 错
`<h2><p></p></h2>`—— 对
`<dt><dt></dt></dt>`—— 错

2. 有几个特殊的块级元素只能包含内嵌元素，不能再包含块级元素，这几个特殊的标签是：
　　h1、h2、h3、h4、h5、h6、p、dt。
- 当输入`<h2><h2></h2></h2>`时，浏览器出现的html文档是：`<h2></h2><h2></h2>`，原本是嵌套的属于父子关系的标签成为了2个兄弟标签。
- 当输入`<h2><h3></h3></h2>`时，浏览器出现的html文档是：`<h2></h2><h3></h3>`，原本是嵌套的属于父子关系的标签成为了2个兄弟标签。
- 当输入`<p><p></p></p>`时，浏览器出现的html文档是：`<p></p><p></p><p></p>`,原本是嵌套的属于父子关系的标签成为了3个兄弟标签。
- 当输入`<p><h2></h2></p>`时，浏览器出现的html文档是：`<p></p><h2></h2><p></p>`。
- 当输入`<dt><dt></dt></dt>`时，浏览器出现的html文档是：`<dt></dt><dt></dt>`。
- 当输入`<h2><p></p></h2>`时，浏览器出现的html文档是：`<h2><p></p></h2>`，是正确的用法。

----------
#### 创建CSS ####
插入样式表的三种方法
1. 外部样式表
样式需要应用于很多页面时，使用外部样式表可以通过改变一个文件来改变整个站点的外观。每个页面使用 <link> 标签链接到样式表。
<link> 标签在（文档的）头部：
`<head>
<link rel="stylesheet" type="text/css" href="mystyle.css" />
</head>`）
**外部样式表中不能能包含任何的 html 标签**，样式表应该以 **.css 扩展名**进行保存。
格式如下
`hr {color: sienna;}
p {margin-left: 20px;}
body {background-image: url("images/back40.gif");}`

2. 内部样式表
当单个文档需要特殊的样式时，就应该使用内部样式表。你可以使用 `<style>` 标签在html文档头部定义内部样式表，就像这样:
```html
<head>
<style type="text/css">
  hr {color: sienna;}
  p {margin-left: 20px;}
  body {background-image: url("images/back40.gif");}
</style>
</head>
```

3. 内联样式
当样式仅需要在一个元素上应用一次时,可以使用内联样式。
```html
<p style="color: sienna; margin-left: 20px">This is a paragraph</p>
```
