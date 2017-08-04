2/27/2017 12:45:49 PM
#### 使用HTML5的网站布局（多列布局） ####
`<header>`定义文档或节的页眉
`<nav>`定义导航链接的容器
`<section>`定义文档中的节
`<article>`定义独立的自包含文章
`<aside>`定义内容之外的内容（比如侧栏）
`<footer>`定义文档或节的页脚
`<details>`定义额外的细节
`<summary>`定义`details>` 的标题
可利用float属性使各个框浮动。
 
#### height及width ####
属性height及width指的是盒子中内容区的高度和宽度。

2/28/2017 8:58:23 PM 
#### 响应式web设计RWD ####
RWD能够以可变尺寸传递网页，RWD对于平板和移动设备是必需的。
创建RWD有两种方法：
1. 自己创建
利用浮动float，把各框架尺寸写死，窗口最大化时各框架会按浮动特性水平排列，如果页面缩放变小，会得到从上到下排列的外观。利用百分比写相对尺寸的话，无论页面怎样缩放，始终保持一样的布局。
2. 使用Bootstrap
Bootstrap是现在最流行的开发响应式web的HTML，CSS和JS框架，它可帮助开发出在任何尺寸都外观出众的站点，如显示器，笔记本电脑，平板或手机。
[响应式web设计](http://www.w3school.com.cn/html/html_responsive.asp)


3/3/2017 9:44:19 AM 
#### HTML框架 ####
通过使用框架，你可以在同一个浏览器窗口中显示不止一个页面。每份HTML文档称为一个框架，并且每个框架都独立于其他的框架。

- 框架结构标签`<frameset>`定义如何将窗口分割为框架,每个frameset定义了一系列行或列,rows/columns的值规定了每行或每列占据屏幕的面积.
- `<Frame>`定义了放置在每个框架中的HTML文档。
**提示：**
- 假如一个框架有可见边框，用户可拖动边框来改变它的大小。为了避免这种情况发生，可以在 <frame> 标签中加入：noresize="noresize"。
- 为不支持框架的浏览器添加 `<noframes>`。 
- `<body></body>`标签与 `<frameset></frameset>`标签不能同时使用，因为body和frameset谁靠外浏览器就解析谁，另一个相当于完全不存在。
- 不过，假如添加包含一段文本的 `<noframes>` 标签，就必须将这段文字嵌套于 <body></body> 标签内。
```html
<html>
<frameset cols="25%,50%,25%">
  <frame src="/example/html/frame_a.html">
  <frame src="/example/html/frame_b.html">
  <frame src="/example/html/frame_c.html">
<noframes>
<body>您的浏览器无法处理框架！</body>
</noframes>
</frameset>
</html>
```
**frameset可以嵌套自身达到混合框架的效果**
```html
<html>
<frameset rows="50%,50%">
<frame src="/example/html/frame_a.html">
<frameset cols="25%,75%">
<frame src="/example/html/frame_b.html">
<frame src="/example/html/frame_c.html">
</frameset>
</frameset>
</html>
```
**内联框架iframe**
height 和 width 属性用于规定 iframe 的高度和宽度。
属性值的默认单位是像素，但也可以用百分比来设定（比如 "80%"）
```html
<!DOCTYPE html>
<html>
<body>
<iframe src="/example/html/demo_iframe.html" width="200" height="200"></iframe>
<p>某些老式的浏览器不支持内联框架。</p>
<p>如果不支持，则 iframe 是不可见的。</p>
</body>
</html>
```
iframe 可用作链接的目标（target）。
链接的 target 属性必须引用 iframe 的 name 属性：
```html
<!DOCTYPE html>
<html>
<body>
<iframe src="/example/html/demo_iframe.html" name="iframe_a"></iframe>
<p><a href="http://www.w3school.com.cn" target="iframe_a">W3School.com.cn</a></p>
<p><b>注释：</b>由于链接的目标匹配 iframe 的名称，所以链接会在 iframe 中打开。</p>
</body>
</html>
```

#### 插入脚本 ####
.css在head中的link标签内 .js在head/body中的script标签中。
```html
<!DOCTYPE html>
<html>
<body>
<script type="text/javascript">
document.write("Hello World!")
</script>
<noscript>Sorry, your browser does not support JavaScript!</noscript>
<p>不支持 JavaScript 的浏览器将显示 noscript 元素中的文本。</p>
</body>
</html>
```
script 元素既可包含脚本语句，也可通过 src 属性指向外部脚本文件。
noscript 元素可包含普通 HTML 页面的 body 元素中能够找到的所有元素。

**如何应付老式的浏览器?**
如果浏览器压根没法识别 `<script>` 标签，那么 `<script>` 标签所包含的内容将以文本方式显示在页面上。为了避免这种情况发生，你应该将脚本隐藏在注释标签当中。那些老的浏览器（无法识别 `<script>` 标签的浏览器）将忽略这些注释，所以不会将标签的内容显示到页面上。而那些新的浏览器将读懂这些脚本并执行它们，即使代码被嵌套在注释标签内。
实例:`JavaScript`:
```html
<body>
  <script type="text/javascript">
    <!--
    document.write("Hello World!")
    //-->
  </script>
  <noscript>Your browser does not support JavaScript!</noscript>
</body>
```
#### head中如何把用户定向到新网址 ####
```html
<!DOCTYPE HTML>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=gb2312" />
<meta http-equiv="Refresh" content="5;url=http://www.w3school.com.cn" />
</head>

<body>
<p>
对不起。我们已经搬家了。您的 URL 是 <a href="http://www.w3school.com.cn">http://www.w3school.com.cn</a>
</p>
<p>您将在 5 秒内被重定向到新的地址。</p>
<p>如果超过 5 秒后您仍然看到本消息，请点击上面的链接。</p>
</body>
</html>
```
`content="5;url=http://www.w3school.com.cn"` 中“5”指的是5秒，后面的url就是5秒后将跳转的地址。
content属性与 :before及:after 伪元素配合使用，来插入生成内容。该属性用于定义元素之前或之后放置的生成内容。默认的是行内内容。

#### head元素 ####
`<head>` 元素是所有头部元素的容器。`<head>` 内的元素可包含脚本，指示浏览器在何处可以找到样式表，提供元信息，等等。
以下标签都可以添加到 head 部分：`<title>、<base>、<link>、<meta>、<script>、<style>`。
**html文档基本结构：**
```html
<!DOCTYPE html>
<html>
<head>
	<title>工具栏中的标题，添加到收藏夹时显示的标题，显示在搜索引擎结果中的页面标题</title>
<!--meta标签始终未予head元素中，提供关于 HTML 文档的元数据。元数据不会显示在页面上，但是对于机器是可读的，典型的情况是，meta 元素被用于规定页面的描述、关键词、文档的作者、最后修改时间以及其他元数据。元数据可用于浏览器（如何显示内容或重新加载页面），搜索引擎（关键词），或其他 web 服务。一些搜索引擎会利用 meta 元素的 name 和 content 属性来索引页面。name 和 content 属性的作用是描述页面的内容。-->
	<meta charset="utf-8" name="description" content="Free Web tutorials on HTML, CSS, XML" />
	<meta name="keywords" content="HTML, CSS, XML" />
<!--base标签为页面上的所有链接规定默认地址或默认目标（target:在哪个页面打开）：-->
    <base href="http://www.w3school.com.cn/images/" />
    <base target="_blank" />
    <link rel="stylesheet" type="text/css" href="mystyle.css" />
    <style type="text/css">
    body {background-color:yellow}
    p {color:blue}
    </style>
</head>

<body>
    <script type="text/javascript">
<!--
	document.write("hello dolby!!!")
	//-->
    </script>
    <noscript>你的浏览器不支持脚本</noscript>
</body>
</html>
```

#### html实体 ####
- 在HTML中不能使用小于号（<）和大于号（>），这是因为浏览器会误认为它们是标签。如果希望正确地显示预留字符，我们必须在 HTML 源代码中使用字符实体（character entities）。
- 如需显示小于号，我们必须这样写：**`<`** 或** `<`**
- 提示：使用实体名而不是数字的好处是，名称易于记忆。不过坏处是，浏览器也许并不支持所有实体名称（对实体数字的支持却很好）。
- 浏览器总是会截短 HTML 页面中的空格。如果您在文本中写 10 个空格，在显示该页面之前，浏览器会删除它们中的 9 个。如需在页面中增加空格的数量，您需要使用   字符实体。
**注意：**
实体名称对大小写敏感。

#### URL-Uniform Resource Locator统一资源定位符 ####
当您点击 HTML 页面中的某个链接时，对应的 `<a>` 标签指向万维网上的一个地址。
统一资源定位器（URL）用于定位万维网上的文档（或其他数据）。
网址，比如 (http://www.w3school.com.cn/html/index.asp)，
遵守以下的语法规则：
scheme://host.domain:port/path/filename
解释：
scheme - 定义因特网服务的类型。最常见的类型是 http
host - 定义域主机（http 的默认主机是 www）
domain - 定义因特网域名，比如 w3school.com.cn
:port - 定义主机上的端口号（http 的默认端口号是 80）
path - 定义服务器上的路径（如果省略，则文档必须位于网站的根目录中）。
filename - 定义文档/资源的名称

#### 浮动float ####
如何让包围元素在视觉上包围浮动元素呢？需要在这个元素中的某个地方应用 clear：
常用的方法：**对布局中的所有东西包括容器div进行浮动，然后使用适当的有意义的元素（常常是站点的页脚）对这些浮动进行清理（clear：both；），这有助于减少或消除不必要的标记。**
**清除浮动（clear：both；）会换行。后面的内容不再是环绕浮动。**

3/4/2017 2:06:45 PM 
#### css选择器（区分大小写）分组 ####
假设希望h2元素和段落p都有灰色。为达到这个目的，最容易的做法是使用以下声明：`h2, p {color:gray;}`
将h2和p选择器放在规则左边，然后用逗号分隔，就定义了一个规则。

#### 通配符选择器 ####
通配选择器（universal selector），显示为一个星号（*）。该选择器可以与任何元素匹配，就像是一个通配符。
```html
<head>
<style type="text/css">
* {color:red;}
</style>
</head>
```
上面的规则可以使文档中的每个元素都为红色。

#### 声明分组 ####
假设希望所有 h1 元素都有红色背景，并使用 28 像素高的 Verdana 字体显示为蓝色文本，可以写以下样式：
```html
h1 {font: 28px Verdana;}
h1 {color: blue;}
h1 {background: red;}
```
可以上写法效率太低且麻烦，可写成如下样式：
```html
h1 {
  font: 28px Verdana;
  color: blue;
  background: red;
  }
```
**注意：**对声明分组，一定要在各个声明的最后使用分号，包括最后一个声明。若一个声明有多个值，值用空格分开，最后一个值后加分号。

#### 类选择器 ####
```html
<html>
<head>
<style type="text/css">
.important {color:red;}
</style>
</head>

<body>
<h1 class="important">This heading is very important.</h1>
<p class="important">This paragraph is very important.</p>
<p>This is a paragraph.</p>
</body>
</html>
```
**注意：**`.important {color:red;}`和`*.important {color:red;}`效果是一样的。

#### 类选择器结合元素选择器 ####
例如希望只有段落显示为红色文本：`p.important {color:red;}`：class属性值为important的所有段落。

#### 多类选择器 ####
一个 class 值中可能包含一个词列表，各个词之间用空格分隔。例如，如果希望将一个特定的元素同时标记为重要（important）和警告（warning），就可以写作：
```html
<p class="important">This paragraph is very important.</p>
<p class="warning">This is a warning.</p>
<p class="important warning">
This paragraph is a very important warning.
</p>
```
这两个词的顺序无关紧要，写成 warning important 也可以。
```css
.important {font-weight:bold;}
.warning {font-style:italic;}
.important.warning {background:silver;}
```
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-205aa8c6d6732f65.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
class="important warning"的p元素中的内容呈现粗斜体且有银色背景。

**注意：**如果像上面一样把两个类选择器链接在一起，仅可以选择同时包含这些类名的元素（类名的顺序不限），少了其中任何一个都会匹配失败，但是多出除了这两个之外的别的选择器没有关系。但可能出现优先级的问题，不是什么大问题。

#### id选择器（区分大小写） ####
语法：
`*#intro {font-weight:bold;}`
与类选择器一样，ID 选择器中可以忽略通配选择器。
也可以写作：`#intro {font-weight:bold;}`
两个的效果将是一样的。
例子：
```html
<html>
<head>
<style type="text/css">
#intro {font-weight:bold;}
</style>
</head>
<body>
<p id="intro">This is a paragraph of introduction.</p>
</body>
</html>
```
**注意：**
- 在一个html文档中，id选择器只能使用一次
- id选择器不能结合使用（即ID 属性不允许有以空格分隔的词列表）
- 知道在一个给定的文档中会有一个 ID 值为 mostImportant 的元素。但不知道这个最重要的东西是一个段落、一个短语、一个列表项还是一个小节标题，这种情况下可编写类似如下规则：
`#mostImportant {color:red; background:yellow;}`这个规则会与id="mostImportant"的元素匹配。

#### 属性选择器 ####
**根据属性选择的用法：**
- 如果希望选择有某个属性的元素，而不论属性值是什么，可以使用简单属性选择器。如希望把包含标题（title）的所有元素变为红色，可以写作：
`*[title] {color:red;}`通配符去掉也没影响。
- 可以只对有 href 属性的锚（a 元素）应用样式：
`a[href] {color:red;}`
- 可以根据多个属性进行选择，只需将属性选择器链接在一起即可。例如，为了将同时有 href 和 title 属性的 HTML 超链接的文本设置为红色，可以这样写：
`a[href][title] {color:red;}`
- 特例：用来诊断图像是否确实有效，可以对所有带有 alt 属性的图像应用样式，从而突出显示这些有效的图像：
`img[alt] {border: 5px solid red;}`
- 为XML文档使用属性选择器。

**根据具体属性值选择的用法：**
只选择有特定属性值的元素。
- 假设希望将指向 Web 服务器上某个指定文档的超链接变成红色，可以这样写：
`a[href="http://www.w3school.com.cn/about_us.asp"] {color: red;}`
- 与简单属性选择器类似，可以把多个属性-值选择器链接在一起来选择一个文档。
`a[href="http://www.w3school.com.cn/"][title="W3School"] {color: red;}`
这样会使以下标记中的第一个超链接的文本变为红色。`<a href="http://www.w3school.com.cn/" title="W3School">W3School</a>`
如果写作`a[href="http://www.w3school.com.cn/"],[title="W3School"] {color: red;}`
那么所有包含`href="http://www.w3school.com.cn/"`的a元素和所有包含`[title="W3School"]`的元素都会变成红色。
- XML语言也可以利用这种方法来设置样式。

**属性与属性值必须完全匹配**
```html
p[class="important warning"] {color: red;}
<p class="important warning">This paragraph is a very important warning.</p>
```

**根据部分属性值选择：**
如果需要根据属性值中的词列表的某个词进行选择，则需要使用波浪号（~）。
假设您想选择class属性中包含important的元素，可以用下面这个选择器做到这一点：
```html
p[class~="important"] {color: red;}
<h1>可以应用样式：</h1>
<p class="important warning">This is a paragraph.</a>
<p class="important">This is a paragraph.</a>
```
如果忽略了波浪号，则说明需要完成完全值匹配。

**部分值属性选择器与点号类名记法的区别:**
`p.important`和`p[class="important"]` 应用到HTML文档时是等价的。
"~="属性选择器能用于任何属性，而不只是 class。
例如，可以有一个包含大量图像的文档，其中只有一部分是图片。对此，可以使用一个基于 title文档的部分属性选择器，只选择这些图片：
```html
img[title~="Figure"] {border: 1px solid gray;}
<h1>可以应用样式：</h1>
![](/i/figure-1.gif)
![](/i/figure-2.gif)
```
这个规则会选择title文本包含"Figure"的所有图像。没有title属性或者title属性中不包含"Figure"的图像都不会匹配。

**子串匹配属性选择器**
包含了更多的部分值选择器，**任何属性都可以使用这些选择器**。
- `[abc^="def"]`选择abc属性值以"def"开头的所有元素；
- `[abc$="def"]`选择abc属性值以"def"结尾的所有元素；
- `[abc*="def"]`选择abc属性值中包含子串"def"的所有元素。
用途举例：
```html
a[href*="w3school.com.cn"] {color: red;}
<h1>可以应用样式：</h1>
<a href="http://www.w3school.com.cn/">W3School</a>
<a href="http://www.w3school.com.cn/css/">CSS</a>
<a href="http://www.w3school.com.cn/html/">HTML</a>
```

**特定属性选择类型**
```html
*[lang|="en"] {color: red;}
<h1>可以应用样式：</h1>
<p lang="en">Hello!</p>
<p lang="en-us">Greetings!</p>
<p lang="en-au">G'day!</p>
<p lang="fr">Bonjour!</p>
<p lang="cy-en">Jrooana!</p>
```
通配符*可有可无，上面的规则会选择lang属性值为"en"或以"en-"开头的所有元素，该值必须是整个单词。所以前三个元素将会被渲染，后两个不会。

一般来说，`[att|="val"]`可用于任何属性及其值。这种属性选择器最常见的用途还是匹配语言值。

也可用于匹配图像样式：
```html
img[src|="figure"] {border: 1px solid gray;}
<h1>可以应用样式：</h1>
![](/i/figure-1.gif)
![](/i/figure-2.gif)
```

#### 后代选择器（包含选择器） ####
可以选择作为某元素后代的元素。
可以定义后代选择器来创建一些规则，使这些规则在某些文档结构中起作用，而在另外一些结构中不起作用。
```html
h1 em.1 {color:red;}
<h1>This is a <em class="1">会应用样式</em> hea<em>不会应用选择器内样式</em>ng</h1>
<p>This is a <em>不会应用选择器内样式</em> paragraph.</p>
```
上面这个规则会把作为h1元素后代的class
值为1的em元素的文本变为红色。其他em文本（如段落或块引用中的em）则不会被这个规则选中。

**语法：**规则左边的选择器一端包括两个或多个**用空格分隔**的选择器。在上面的例子中表现为“作为h1元素后代的任何em元素都会应用该样式”。

具体应用：
假设有一个文档，其中有一个边栏，还有一个主区。边栏的背景为蓝色，主区的背景为白色，这两个区都包含链接列表。不能把所有链接都设置为蓝色，因为这样一来边栏中的蓝色链接都无法看到。
解决方法如下：
```html
div.sidebar {background:blue;}
div.sidebar a{color:white;}
div.maincontent {background:white;}
div.maincontent a{color:blue;}
<div class="sidebar">我是边栏<a href="">我是链接</a></div>
<div class="maincontent">我是主区<a href="">我是链接</a></div>
```
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-82785d2c1b296e84.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

后代选择器中两个元素之间的层次可以是无限的，如以下样式一样可以成功应用。
```html
ul em {color:red; font-weight:bold;}
<ul>
  <li>List item 1
    <ol>
  <li>List item 1-1</li>
        <ol>
          <li>List item <em>1-3-2</em></li>
        </ol>
    </ol>
  </li>
</ul>
```
"1-3-2"显示为红色粗斜体。

#### 子元素选择器 ####
例如，如果选择只作为 h1 元素子元素的strong元素，可以这样写：
```html
h1 > strong {color:red;}
<h1>This is <strong>very</strong> <strong>very</strong> important.</h1>
<h1>This is <em>really <strong>very</strong></em> important.</h1>
```
结果：第一个h1下面的两个strong元素变为红色，但是第二个h1中的strong不受影响。

**语法：**
子选择器使用了大于号（子结合符）。
子结合符两边可以有空白符，以下写法都没有问题：
`h1 > strong`
`h1> strong`
`h1 >strong`
`h1>strong`
从右向左读，选择器`h1 > strong`可以解释为“选中作为h1元素子元素的所有strong元素”。

**结合后代选择器与子选择器**
`table.company td > p`
上面的选择器会选择作为td元素子元素的所有 p元素，这个td元素本身从table元素继承，该 table元素有一个包含company的class属性。

3/5/2017 1:34:55
#### 相邻兄弟选择器 ####
**可选择紧接在另一元素后的元素，且二者有相同父元素。**

**语法：**
相邻兄弟选择器使用了加号（+），与子结合符一样，相邻兄弟结合符旁边可以有空白符。
例如：
要增加紧接在 h1 元素后出现的段落的上边距，可以这样写：
```html
<head>
<style type="text/css">
h1 + p {margin-top:50px;}
</style>
</head>
<body>
<h1>This is a heading.</h1>
<p>This is paragraph.</p>
```
这个选择器读作：“选择紧接在h1元素后出现的段落，h1和p元素拥有共同的父元素”。

在下列文档树中：
```html
<!DOCTYPE HTML>
<html>
<head>
<style type="text/css">
li + li {font-weight:bold;}
</style>
</head>

<body>
<div>
  <ul>
    <li>List item 1</li>
    <li>List item 2</li>
    <li>List item 3</li>
  </ul>
  <ol>
    <li>List item 1</li>
    <li>List item 2</li>
    <li>List item 3</li>
  </ol>
</div>
</body>
</html>
```
ul列表和ol列表是相邻兄弟；ul内的列表项是相邻兄弟；ol内的列表项也是相邻兄弟；但ol内的列表项和ul内的列表项不是相邻兄弟关系，因为这两组列表项不属于同一父元素。
**注意：**
一个结合符只能选择两个相邻兄弟中的第二个元素。
即上例中，`li + li {font-weight:bold;}`只会选择ul和ol中的第二个和第三个列表项。

**结合其他选择器**
`html > body table + ul {margin-top:20px;}`
这个选择器解释为：选择紧接在table 元素后出现的所有兄弟ul元素，该table 元素和ul元素都有同一父元素body，body元素本身是html元素的子元素。

#### css伪类 ####
CSS伪类用于向某些选择器添加特殊的效果。
**语法：**
`selector : pseudo-class {property: value}`
CSS类也可与伪类搭配使用。
`selector.class : pseudo-class {property: value}`

**例1：锚伪类-向文档中的超链接添加样式**
```html
<style type="text/css">
a:link {color: #FF0000}
a:visited {color: #00FF00}
a:hover {color: #FF00FF}
a:active {color: #0000FF}
</style>
```
link表示未被点击的链接，visited表示已经被点击的链接，hover表示鼠标移到链接上时，active表示正在被点击的链接，这四个只能按照以上顺序编写。

```html
<style type="text/css">
a.one:link {color: #ff0000}
a.one:visited {color: #0000ff}
a.one:hover {color: #ffcc00}

a.two:link {color: #ff0000}
a.two:visited {color: #0000ff}
a.two:hover {font-size: 150%}

a.three:link {color: #ff0000}
a.three:visited {color: #0000ff}
a.three:hover {background: #66ff66}

a.four:link {color: #ff0000}
a.four:visited {color: #0000ff}
a.four:hover {font-family: monospace}

a.five:link {color: #ff0000; text-decoration: none}
a.five:visited {color: #0000ff; text-decoration: none}
a.five:hover {text-decoration: underline}
</style>
```
上例依次是改变当鼠标移到链接上时的颜色,字体大小，背景色，字体，是都有下划线。

**例2：伪类与css配合使用**
```html
a.red : visited {color: #FF0000}
<a class="red" href="css_syntax.asp">CSS Syntax</a>
```
假如上面的例子中的链接被访问过，那么它将显示为红色。

**例3：（：first-child伪类）**
**！！！必须声明` <!DOCTYPE>`**
**语义：**对作为某元素第一个子元素的元素应用样式，例如`p:first-child {font-weight: bold;}`的意思是：对作为某元素的第一个子元素p应用样式，而不是对p的第一个子元素应用样式，这一点要牢记。
```html
<!DOCTYPE HTML> 
<html>
<head>
<style type="text/css">
p:first-child {font-weight: bold;}
li:first-child {text-transform:uppercase;}
strong:first-child {color:red;}
em:first-child {background:blue;}
</style>
</head>

<body style="background:green;">
<div>
<p>abc</p>
<ul>
<li>abc</li>
<li>abc<strong>abc</strong></li>
<li>abc</li>
</ul>
<p>abc<em>abc</em> abc</p>
</div>
</body>

</html>
```
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-badccbfb3bfb05cb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

下例才是匹配所有p元素的第一个子元素
```html
<!DOCTYPE HTML>
<html>
<head>
<style type="text/css">
p > i:first-child {
  font-weight:bold;
  } 
</style>
</head>

<body style="background-color:green;">
<p>some <i>text</i>. some <i>text</i>.</p>
<p>some <i>text</i>. some <i>text</i>.</p>
</body>
</html>
```
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-f558610f30356aae.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

匹配所有 作为第一个子元素的`<p>`元素中的所有`<i>`元素。
```html
<!DOCTYPE HTML>
<html>
<head>
<style type="text/css">
p:first-child i {
  color:blue;
  } 
</style>
</head>

<body style="background-color:green;">
<p>some <i>text</i>. some <i>text</i>.</p>
<p>some <i>text</i>. some <i>text</i>.</p>
</body>
</html>
```
![](http://upload-images.jianshu.io/upload_images/6851923-5764cbce93d24d33.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**例4：（：lang伪类）**
向带有指定lang属性的元素添加样式。
**注意：**:lang 伪类根据元素的语言编码匹配元素。这种语言信息必须包含在文档中，或者与文档关联，不能从CSS指定。:lang的处理与|=选择器相同。
```html
<!DOCTYPE HTML>
<html>
<head>
<style type="text/css">
q:lang(no)
{
quotes: "~" "~"
}
</style>
</head>

<body style="background-color:green;">

<p>一些文本 <q lang="no">段落中的引用</q> 一些文本。</p>
</body>

</html>
```
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-f7eaa1e299a2c611.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**例5：（：focus伪类）**
对超链接应用-向拥有键盘输入焦点的元素添加样式，如果已规定!DOCTYPE，那么IE8及以上版本支持 :focus伪类。
```html
<!DOCTYPE HTML>
<html>
<head>
<style type="text/css">
input:focus
{
background-color:yellow;
color:red;
}
</style>
</head>

<body>
<form action="form_action.asp" method="get">
First name: <input type="text" name="fname" /><br />
Last name: <input type="text" name="lname" /><br />
<input type="submit" value="Submit" />
</form>
</body>
</html>
```
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-3d06f3446516fbd4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### css伪元素 ####
CSS伪类用于向某些选择器设置特殊效果。
**语法：**
`selector : pseudo-element {property: value}`
CSS类也可与伪类搭配使用。
`selector.class : pseudo-element {property: value}`
**例1：（:first-line伪元素）**
**只能用于块级元素**，用于向文本的首行设置特殊样式。
属性包括：
font
color
background
word-spacing
letter-spacing
text-decoration
vertical-align
text-transform
line-height
clear
```html
<!DOCTYPE HTML>
<head>
<style type="text/css">
p:first-line 
{
color: #ff0000;
font-variant: small-caps
}
</style>
</head>

<body>
<p>
You can use the :first-line pseudo-element to add a special effect to the first line of a text!
</p>
</body>
</html>
```

**例2：（:first-letter伪元素）**
**只能用于块级元素**，用于向文本的首字母设置特殊样式。
属性包括：
font
color
background
margin
padding
border
text-decoration
vertical-align (仅当 float 为 none 时)
text-transform
line-height
float
clear
```html
p:first-letter 
{
color: #ff0000;
font-size:xx-large
}
```
伪元素与css类可配合使用。
```html
p.article:first-letter
  {
  color: #FF0000;
  }
<p class="article">This is a paragraph in an article。</p>
```
多个伪元素可结合使用,这里不存在覆盖的问题。
```html
p:first-letter
  {
  color:#ff0000;
  font-size:xx-large;
  }
p:first-line 
  {
  color:#0000ff;
  font-variant:small-caps;
  }
<p>You can combine the :first-letter and :first-line pseudo-elements to add a special effect to the first letter and the first line of a text!</p>
```
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-6c9574ac4d453680.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**例3：（:before伪元素）**
在元素的内容前面插入新内容。
**例4：（:after伪元素）**
在元素的内容后面插入新内容。
```html
<!DOCTYPE html>
<html>
<head>
<style type="text/css">
h1:after {content:url(/i/w3school_logo_white.gif)}
p:before {content:url(/i/w3school_logo_white.gif)}
</style>
</head>

<body>
<h1>111</h1>
<p>222</p>
</body>
</html>
```
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-e34a26747eed7a58.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
**注意：**
只有规定!DOCTYPE，IE8及以上才支持 content属性。

#### URL字符编码 ####
URL只能使用ASCII字符集来通过因特网进行发送。
但URL常常会包含ASCII集合之外的字符，所以URL必须转换为有效的ASCII格式。[URL编码表](http://www.w3school.com.cn/tags/html_ref_urlencode.html)
URL编码使用"%"其后跟随两位的十六进制数来替换非ASCII字符。
URL不能包含空格。URL编码通常使用+来替换空格。
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-721139476f12e233.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-b48cb01f9a1e4ec7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### web服务器 ####
选择了解的内容。[网站主机教程](http://www.w3school.com.cn/hosting/index.asp)

#### 颜色 ####
颜色由一个十六进制符号来定义，这个符号由红色、绿色和蓝色的值组成（RGB），如#000000，也可写成#000，但建议写六位的，因为这样颜色更多。

#### HTML <!DOCTYPE>文档类型 ####
`<!DOCTYPE>`不是HTML标签，而是为浏览器提供一项声明，即HTML是用什么版本编写的，`<!DOCTYPE>`声明对大小写不敏感，但必须是HTML文档的第一行，位于`<html>`标签之前。
**用处:**Web世界中存在许多不同的文档，浏览器要完全了解文档类型及版本才能完全正确地显示页面。
**提示：**始终HTML文档添加`<!DOCTYPE>`声明，这样浏览器才能获知文档类型。
[只需要大致了解的内容](http://www.w3school.com.cn/tags/tag_doctype.asp)

#### HTML4.01快速参考 ####
[html快速参考](http://www.w3school.com.cn/html/html_quick.asp)
