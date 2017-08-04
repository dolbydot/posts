2/24/2017 10:28:45 PM 
#### 背景关联 ####
如果文档比较长，那么当文档向下滚动时，背景图像也会随之滚动。当文档滚动到超过图像的位置时，图像就会消失。
可通过 background-attachment 属性防止这种滚动。通过这个属性，可以声明图像相对于可视区是固定的（fixed），因此不会受到滚动的影响：
```html
body 
  {
  background-image:url(/i/eg_bg_02.gif);
  background-repeat:no-repeat;
  background-attachment:fixed
  }
```
background-attachment 属性的默认值是 scroll，也就是说，在默认的情况下，背景会随文档滚动。
**如何使用简写属性来将所有背景属性设置在一个声明之中？**
```html
<head>
<style type="text/css">
body
{ 
background: #ff0000 url(/i/eg_bg_03.gif) no-repeat fixed center; 
}
</style>
</head>
```
呈现的效果为红色，不重复，可视区固定的背景。
这些属性值都属于background，用空格分开。
#### text-indent属性用于首行缩进 ####
通过使用 text-indent 属性，所有元素的第一行都可以缩进一个给定的长度，甚至该长度可以是负值。
有继承性。
```html
p {text-indent: 5em;}
```
注意：一般来说，可以为所有块级元素应用 text-indent，但无法将该属性应用于行内元素(如果想把一个行内元素的第一行“缩进”，可以用左内边距或外边距创造这种效果）。图像之类的替换元素上也无法应用 text-indent 属性，但如果一个块级元素（比如段落）的首行中有一个图像，它会随该行的其余文本移动。
在为 text-indent 设置负值时要当心，如果对一个段落设置了负值，那么首行的某些文本可能会超出浏览器窗口的左边界。为了避免出现这种显示问题，建议针对负缩进再设置一个外边距或一些内边距：
```html
p {text-indent: -5em; padding-left: 5em;}
```
text-indent 可以使用所有长度单位，包括百分比值。
百分数要相对于缩进元素父元素的宽度。
如果将缩进值设置为 20%，所影响元素的第一行会缩进其父元素宽度的 20%.
如下
```html
div {width: 500px;}
p {text-indent: 20%;}

<div>
<p>this is a paragragh</p>
</div>
```
和背景定位属性使用像素便宜道理一样，最简单意义上的点对点偏移。
**text-indent 属性可以继承**
```html
<head>
<style type="text/css">
div#outer {width: 500px;}
div#inner {text-indent: 10%;}
p {width: 200px;}
</style>
</head>
<body>
<div id="outer">
<div id="inner">some text. some text. some text.some text.some text.some text.some text.some text.some text.some text.some text.
<p>this is a paragragh.this is a paragragh.this is a paragragh.</p>
</div>
</div>
</body>
```
以上标记中的段落也会缩进50像素，因为这个段落继承了id为inner的div元素的缩进值。
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-5bbf149874d1fdd8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
#### 水平对齐属性text-align ####
text-align属性有五个值：**left,right,center(一般只用这三个)**,justify,inherit.
**如果direction属性是ltr，则默认值是left；如果 direction是rtl，则为right。**
justify:使文本的两端都对齐。在两端对齐文本中，文本行的左右两端都放在父元素的内边界上。然后调整单词和字母间的间隔，使各行的长度恰好相等。两端对齐文本在打印领域很常见。但因为要由用户代理（而不是 CSS）来确定两端对齐文本如何拉伸，以填满父元素左右边界之间的空间，所以在 CSS 中，两端对齐文本看上去没有打印出来好看，特别是元素可能太窄，以至于每行只能放下几个单词。要不要用这个值还需要多考虑。
inherit:规定应该从父元素继承 text-align 属性的值。
#### 文本装饰属性text-decoration ####
胜出规则的值会**完全取代**另一个值:
```html
<head>
<style type="text/css">
p.outer {color:#ff0;text-decoration: line-through;}
p{color:#0f0;text-decoration: underline overline;background-color: #000;white-space: normal;}
</style>
</head>
<body>
<p>s ome te xt</p>
<p class="outer">s              om        e   s              om        es              om        es              om        es              om        es              om        e</p>
</body>
```
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-a83abea11f79cc79.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- 所有class="outer"的p元素字色为“#ff0”，有一个贯穿线装饰，背景色为“#000”，丢掉多余的空白符；
- 所有其他的p元素字色为“#0f0”，有下划线和上划线装饰，背景色为“#000，丢掉多余的空白符。

**总结：**
1. 相同属性的两个不同的值与同一元素匹配，胜出规则的值会完全取代另一个值，即“值会替换”。
2. 属性与元素匹配，属性无冲突的部分会全部应用到所有的该元素上，即“值会累计”。

#### 空白符属性white-space ####
**white-space值可以应用到所有元素中。**
值：normal,pre,now-rap,pre-wrap,pre-line.
- **normal**
- **丢掉多余的空格，回车转换为空格，会自动换行**。
上例提到了空白符属性white-space，可用以下声明设置这种默认行为：
p {white-space: normal;}，
- **pre**
**保留所有空格和回车，不会自动换行**（回车之后的内容才会显示换行，不然文本再长在浏览器中也只有一行，不管代码中的内容有没有显示完）。其行为等同于html中pre元素，仅在这个方面，包含“text-space：pre”属性的任何元素都可以相当于一个pre元素。
- **nowrap**
**丢掉多余的空格，回车转换为空格，不会自动换行，换行要使用`<br />`**
- **pre-wrap**
浏览器会**保留所有空格和回车，允许自动换行**。
- **pre-line**
浏览器会**保留回车，允许自动换行，丢掉多余的空格**。

#### 文本方向的差别 ####
```html
<head>
<style type="text/css">
p{direction: ltr;}
h2{direction: rtl;}
</style>
</head>
<body>
<p>这是第一段文字</p>
<h2>这是第二段文字</h2>
<bdo dir="ltr">这是第三段文字</bdo>
<br/>
<bdo dir="rtl">这是第四段文字</bdo>
</body>
```
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-3c315624eb0cf9f8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- direction作为p,h等元素的属性时，属性值ltr可理解为文本左对齐，rlt为文本右对齐。
- direction作为bdo元素的属性时，属性值ltr表明文字按从左到右的方向书写，rlt表明文字按从右到左的方向书写。默认左对齐。

----------
#### CSS 字体 ####
CSS 中定义了 5 种通用字体系列：
**font-family**
**有继承性。**
- Serif 字体
- Sans-serif 字体
- Monospace 字体
- Cursive 字体
- Fantasy 字体
格式：
```html
p {font-family: Times, TimesNR, 'New Century Schoolbook',
 Georgia, 'New York', serif;}
```
当字体名中有一个或多个空格或者如果字体名包括 # 或 $ 之类的符号，就需要在 font-family 声明中加引号。
单引号或双引号都可以。但是，如果把一个 font-family 属性放在 HTML 的 style 属性中，则需要加单引号。
```html
<p style="font-family: Times, TimesNR, 'New Century Schoolbook', Georgia,
 'New York', serif;">...</p>
```
**font-style字体风格**
三个值：normal（正常显示），italic（斜体），oblique（倾斜）
- italic：对每个字母的结构有一些小改动，来反映变化的外观。
- oblique：正常竖直文本的一个倾斜版本。
两者看上去完全一样。
**font-size字体大小**
font-size 值可以是绝对或相对值。
- 绝对值：
将文本设置为指定的大小（可用像素px或em，**推荐使用em**）。
不允许用户在所有浏览器中改变文本大小（不利于可用性），绝对大小在确定了输出的物理尺寸时很有用。

- 相对大小：
相对于周围的元素来设置大小，允许用户在浏览器改变文本大小
**浏览器中默认普通文本（比如段落）的大小是 16 像素 (16px=1em)。**
可以使用下面这个公式将像素转换为 em：
pixels/16=em
其中，16=父元素的默认字体大小，若父元素为font-size为20px，公式需改为pixels/20=em.

只用px或em在IE中调整文本大小都会有问题，在所有浏览器中均有效的方案是结合使用百分比与em，即为body元素（父元素）设置默认的font-size值=100%.
以父元素font-size是16px为例：
```html
<head>
<style type="text/css">
body {font-size:100%;} /* 16px/16=1em */
h1 {font-size:3.75em;} /* 60px/16=3.75em */
h2 {font-size:2.5em;}  /* 40px/16=2.5em */
p {font-size:0.875em;} /* 14px/16=0.875em */
</style>
</head>
<body>
<h1>This is heading 1</h1>
<h2>This is heading 2</h2>
<p>This is a paragraph.</p>
<p>This is a paragraph.</p>
<p>...</p>
</body>
```
还有另一种用法：
```html
<head>
<style type="text/css">
h1 {font-size: 300%}
h2 {font-size: 200%}
p {font-size: 100%}
</style>
</head>
<body>
<h1>This is header 1</h1>
<h2>This is header 2</h2>
<p>This is a paragraph</p>
</body>
```
把所有针对属性font的值都写到一起：
```html
<head>
<style type="text/css">
p.ex2
{
font:italic bold 12px/30px arial,sans-serif;
}
</style>
</head>
<body>
<p class="ex2">This is a paragraph.</p>
</body>
```
值用空格分开，其中arial,sans-serif都属于font-family，字体用逗号分隔。

----------
### padding,border,margin以及margin collapse（外边距合并） ###
#### 用百分比设置内外边距 ####
格式大致都是如此。
```html
<html>
<head>
<style type="text/css">
td
{
padding-right: 10%
}
</style>
</head>
<body>
<table border="1">
<tr>
<td>
这个表格单元拥有右内边距。
</td>
</tr>
</table>
</body>
</html>
```
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-a2892f969609f1ec.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
上例中右侧padding宽度为表格边框宽度的10%。

1. 内边距的值不能为负值，上下左右内边距百分数会相对于父元素宽度设置，而不是相对于高度。
2. 外边距的值可以为负值，上下左右外边距百分数会相对于父元素宽度设置，而不是相对于高度。
3. 边框有 3 个方面：宽度、样式，以及颜色，元素的背景会覆盖到内容、内边距和边框区的背景，border-style的默认值是none，如果没有声明样式，就相当于border-style: none，也就是说根本就没有边框，后面设置任何参数都是白搭，所以如果希望边框出现，就必须声明一个边框样式。
4. margin外边距合并实在垂直方向（上下）进行合并。
- 比如A元素在上，margin-bottom=20px，B元素在下，margin-top=10px，当AB元素相遇，两个外边距会合并成20px，即合并外边距margin之后得到的值为高度较大的那个margin。
- 当A元素包含在B元素中时（假设没有padding和border把margin分隔开），那么他们的margin相交或重合的部分也会合并为高度较大的那个margin。
- 假设【有一个空元素br-1，它有margin，但是没有padding和border，margin-top=20px，margin-bottom=20px，那么它自身的上下margin会发生合并变成一个margin-top=20px的空元素【，【此时有另一个空元素br-2，没有padding和border，margin-top=10px，margin-bottom=20px，那么它自身的上下margin会发生合并变成一个margin-bottom=20px的空元素】，**br-1与br-2相遇，1在上2在下，？？？2在上1在下？？？当这个空元素遇到其他非空元素？？？**
元素会继续按照规则发生合并。这就是一系列段落元素占用空间非常小的原因。
