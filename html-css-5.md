2/26/2017 8:47:21 AM 
#### 设置元素堆叠顺序属性Z-index ####
**z-index只能在定位元素上奏效（例如 position:absolute;）**
z-index属性设置元素的堆叠顺序。该属性设置一个定位元素沿z轴的位置，z轴定义为垂直延伸到显示区的轴。z-index的值默认为auto，即堆叠顺序继承自父元素，也可设置值为number，number值可以为负数。如果为正数，则离用户更近，为负数则表示离用户更远，拥有更高堆叠顺序（number值越大）的元素总是会处于堆叠顺序较低的元素的上面。

#### div元素 ####
块级元素，浏览器通常会在 div 元素前后放置一个换行符。**div元素定义文档中的节或区域**，`<div>`标签可以把文档分割为独立的、不同的部分。它**可以用作严格的组织工具**，是组合其他html元素的容器，并且不使用任何格式与其关联,与CSS一同使用，`<div>`元素可用于对大的内容块设置样式属性。
**用 id 或 class 来标记 `<div>`，那么该标签的作用会变得更加有效**。
**提示：请使用`<div>`元素来组合块级元素，这样就可以使用样式对它们进行格式化。**
例如：
```html
<!DOCTYPE html>
<html>
<head>
	<title>无标题</title>
<link rel="stylesheet" type="text/css" href="外部样式表.css">
<style type="text/css">
	h1{color: #000;}
</style>
</head>
<body>
 <h1>NEWS WEBSITE</h1>
  <p>some text. some text. some text...</p>
 
 <div class="news">
  <h2>News headline 1</h2>
  <p>some text. some text. some text...</p>
 </div>

 <div class="news">
  <h2>News headline 2</h2>
  <p>some text. some text. some text...</p>
 </div>
</body>
```
```css
h1{
	color: #0f0;
}
h2{
    color: green;
}
p{
	color: blue;
}
div.news{
	color: gray;
}
```
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-a006a2b494adac58.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**注意：**
css外部样式表中有四个选择器，分别指向h1,h2,p和class=news的div元素。

html内部样式表中也有h1选择器，所以内部样式表h1会覆盖外部样式表h1定义的属性。

`div.news{color: gray;}`选择的是所有class=news的div元素，此div元素内包含有h2元素和p元素，在没有定义h2和p的样式的情况下，所有div元素内的内容全部会被div.class渲染，而此时css外部样式表中有定义p选择器和h2选择器，所以优先选择了p和h2选择器的属性，无论在css中p/h2选择器排列在div.news的前面还是后面。
如果此时将css替换成:
```css
h1{
	color: #0f0;
}
div.news p,h2{
	color: gray;
}
h2{
    color: green;
}
p{
	color: blue;
}
```
`div.news p,h2{color: gray;div.news}`选择的是所有class=news的div内的p元素和代码中所有的h2元素，此div元素内包含有h2元素和p元素，所以所有的class=news的div内的p元素颜色都变成gray，后面单独定义了p只能改变除了div中的之外其余地方的p的颜色；而div后又单独定义了h2选择器，所以这个h2选择器会覆盖前面的h2选择器，所有的h2的color表现为green。

![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-e19b2d379833f5aa.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 在html中插入链接 ####
- 创建超级链接
```html
<html>
<body>
<p>
<a href="/index.html">本文本</a> 是一个指向本网站中的一个页面的链接。</p>
<p><a href="http://www.microsoft.com/">本文本</a> 是一个指向万维网上的页面的链接。</p>
</body>
</html>
```
- 把图像作为链接
只要把图像元素img放在锚点元素a中就可以了。如下：
```html
<html>
<body>
<p>
您也可以使用图像来作链接：
<a href="/example/html/lastpage.html">
![](/i/eg_buttonnext.gif)
</a>
</p>
</body>
</html>
```
**a标签中的内容就是链接的载体/链接名称。**

有两种使用 `<a>` 标签的方式：
1. 通过使用href属性 - 创建指向另一个文档的链接。把a标签中链接的target属性设置为"_blank"，该链接会在新窗口中打开。
2. 通过使用name属性命名锚a - 创建文档内的书签。
```html
<!DOCTYPE html>
<html>
<head>
	<title>无标题</title>
<link rel="stylesheet" type="text/css" href="外部样式表.css">
</head>
<body>
 
 <a href="#News">这是需要点击的地方</a>

 <br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

 <a name="News">这是点击之后出现的地方</a>
</body>
```
上例会在页面上形成以下效果：
![图1](http://upload-images.jianshu.io/upload_images/6851923-162daae00cdda9e1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![图2](http://upload-images.jianshu.io/upload_images/6851923-4bd6ad4ff9939401.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
点击图1文本会自动跳转到图2文本区域。
即：可以把`<a href="#News">`看作定义了一个id属性，指向`<a name="News">`
提示：命名锚经常用于在大型文档开始位置上创建目录。可以为每个章节赋予一个命名锚，然后把链接到这些锚的链接放到文档的上部。如果您经常访问百度百科，您会发现其中几乎每个词条都采用这样的导航方式。
提示：假如浏览器找不到已定义的命名锚，那么就会定位到文档的顶端。不会有错误发生。

**定义图像的语法**
`![](url)`，img是空标签，它只包含属性，没有闭合标签。源属性（src）。src 指 "source"。源属性的值是图像的URL地址。
URL 指存储图像的位置。
- 如果名为 "boat.gif" 的图像位于 www.w3school.com.cn 的 images 目录中，那么其 URL 为 `http://www.w3school.com.cn/images/boat.gif`。
- 如果名为"boat.gif" 的图像和"我的文件.html"位于电脑的同一个文件夹里的同一层，那么图像插入到该html文件中的URL值为`boat.gif`或者`./boat.gif`。
- 如果名为"boat.gif" 的图像在"我的文件.html"的上级菜单里，那么图像插入到该html文件中的URL值为`../boat.gif`。
- 如果名为"boat.gif" 的图像在"我的文件.html"的下级菜单-名为“图片”的文件夹里，那么图像插入到该html文件中的URL值为`图片./boat.gif`。

浏览器将图像显示在文档中图像标签出现的地方。如果将图像标签置于两个段落之间，那么浏览器会首先显示第一个段落，然后显示图片，最后显示第二段。

**替换文本属性（Alt）**
alt 属性用来为图像定义一串预备的可替换的文本。替换文本属性的值是用户定义的。
`![](boat.gif)`
在浏览器无法载入图像时，替换文本属性告诉读者她们失去的信息。此时，浏览器将显示这个替代性的文本而不是图像。**为页面上的图像都加上替换文本属性是个好习惯**，这样有助于更好的显示信息，并且对于那些使用纯文本浏览器的人来说是非常有用的。

提示：
假如某个 HTML 文件包含十个图像，那么为了正确显示这个页面，需要加载 11 个文件。加载图片是需要时间的，所以我们的建议是：慎用图片。

**`<map>`定义图像映射image-map**
利用map和area属性可以创建带有可供点击区域的图像地图。其中的每个区域都是一个超级链接。
area是自闭合标签`<area/>`,area元素永远嵌套在map元素内，area元素定义的是图像映射中的区域。
注释：`<img>`中的usemap属性可引用 `<map>` 中的id或name属性（取决于浏览器），所以我们应同时向 `<map>` 添加id和name属性。
```html
<html>
<body>

<p>请点击图像上的星球，把它们放大。</p>

<img
src="/i/eg_planets.jpg"
border="0" usemap="#planetmap"
alt="Planets" />

<map name="planetmap" id="planetmap">

<area
shape="circle"
coords="180,139,14"
href ="/example/html/venus.html"
target ="_blank"
alt="Venus" />

<area
shape="circle"
coords="129,161,10"
href ="/example/html/mercur.html"
target ="_blank"
alt="Mercury" />

<area
shape="rect"
coords="0,0,110,260"
href ="/example/html/sun.html"
target ="_blank"
alt="Sun" />

</map>

<p><b>注释：</b>img 元素中的 "usemap" 属性引用 map 元素中的 "id" 或 "name" 属性（根据浏览器），所以我们同时向 map 元素添加了 "id" 和 "name" 属性。</p>

</body>
</html>
```
`<img usemap="#planetmap>`图像映射在img元素上（即在img元素内点击）
`<map name="planetmap" id="planetmap">`
img标签的usemap属性将图像定义为客户器端图像映射，map定义一个客户端图像映射，这两行代码定义了一个id="planetmap"，name="planetmap"的图像映射。
**shape="circle" coords="129,161,10"：**
shape和coords配合使用，上面这段代码指的是，可点击跳转链接的区域是一个圆形，圆心坐标是（129,161）（"0,0" 是映射基础图像图像左上角的坐标），圆形半径是10px。
**shape="rect" coords="0,0,110,260"**
这段代码指的是，可点击跳转链接的区域是一个矩形，左上角坐标是（0，0），右下角坐标是（110,260）。

#### 表格table ####
每个表格由table标签开始，一般开头格式为`<table border="1">`，border为边框的宽度，**不设置border的值表格就没有边框。**
- 一个表格的标签顺序为：table（表）,caption（表格标题）,tr（行）,th（表头）,td（单元格）.
- 如果不用tr换行，td再多也不会自动换行。
- 当设置了一个border值，但一个单元格没有内容，如`<td></td>`，在浏览器中可能不能正常显示边框时，可以插入一个空格占位符“ ”，`<td> </td>`，这样就可以了。
- td即table data数据单元格，数据单元格可以包含文本、图片、列表、段落、表单、水平线、表格等等。
- thead,tbody,tfoot标签存在的意义就是将表格分组便于分组渲染。

#### html列表 ####
列表项内部可以使用段落、换行符、图片、链接以及其他列表等等。
- 无序列表：
```html
<ul>
<li>Coffee</li>
<li>Milk</li>
</ul>
```
- 有序列表：
```html
<ol>
<li>Coffee</li>
<li>Milk</li>
</ol>
```
- 定义列表：
```html
<dl>
<dt>Coffee：</dt>
<dd>Black hot drink。</dd>
<dt>Milk：</dt>
<dd>White cold drink。</dd>
</dl>
```
浏览器显示如下：
Coffee：
Black hot drink。
Milk：
White cold drink。
**列表嵌套：**列表可以嵌套多层，有序/无序/定义列表可以互相嵌套。

#### HTML 内联元素 ####
内联元素在显示时通常不会以新行开始。
例子：`<b>, <td>, <a>, <img>，<span>`
`<span>` 元素是内联元素，可用作文本的容器。
`<span>` 元素也没有特定的含义。
与CSS一同使用时，`<span>` 元素可用于为部分文本设置样式属性。 

#### line-height行高 ####
两行文字基线baseline之间的距离。
各种语言文字的基线不一样，英语的基线就是英语本四行线的从上往下数第三条，即小写字母“x”底端紧贴的线。

#### 行内框盒子模型 ####
行内框盒子模型：`<p>这是一行普通的文字，里面包含一个<em>em</em>标签</p>`
上面这段代码包含四种盒子模型。

1. content area：内容盒子（选中文字时的蓝色区域）
2. inline boxes：内联盒子（span,a,em，strong都属于内联盒子），“这是一行普通的文字，里面包含一个”和“标签”属于匿名内联盒子。
3. line boxes：行框盒子，每一行文字就是一个行框盒子，两行就是两个行框盒子。
4. contaning box：包含盒子，本例中是P标签所在的“包含盒子”
**其中：4包含3，3包含2**
