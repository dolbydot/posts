2/25/2017 10:26:17 PM 
#### css定位 ####
一切皆为框：
- div、h1 或 p 元素常常被称为块级元素，即“块框”。
- span，strong等称为行内元素，即“行内框”。
- 把文本添加到一个块级元素的开头（如`<div>
some text<p>Some more text.</p></div>`），即使没有把这些文本定义为段落，它也会被当作段落对待，这种情况下这个框称为无名框，不与专门定义的元素相关联。
- 块级元素的文本行也会发生类似的情况。假设有一个包含三行文本的段落。每行文本形成一个无名框。无法直接对无名块或行框应用样式，因为没有可以应用样式的地方（注意，行框和行内框是两个概念）。

CSS 有三种基本的定位机制：普通流、浮动和绝对定位。默认普通流。
块级框从上到下一个接一个地排列，框之间的垂直距离是由框的垂直margin计算出来（margin合并）。
行内框在一行中水平布置。可以**使用水平内边距（padding-left/right）、边框（border-left/right）和外边距（margin-left/right）调整它们的间距。**但是，**垂直内边距、边框和外边距不影响行内框的高度**。由一行形成的水平框称为行框（Line Box），行框的高度总是足以容纳它包含的所有行内框。
如下：
```html
<!DOCTYPE html>
<html>
<head>
	<title>空标签合并</title>
<style type="text/css">
	br{margin: 20px;background-color: #0f0;}
	br.NO1{margin: 20px;margin-bottom: 30px;background-color: #00f;}
	p{margin: 10px 15px;background-color: #f00;color: #00f;}
	body{background-color: #000;}
	div{background-color: #fff;color: #aaa;}
	p.inline span{background-color: #dad;margin: 60px;}
</style>
</head>
<body>
<br/>
<br class="NO1" />
<p>我没有边框</p>
<br/>
<div>
some text
<p class="inline">Some more text.Some more <span>Some more text.</span>Some more text.Some more text.Some more text.Some more text.Some more text.Some more text.Some more text.Some more text.</p>
<p>我们的天空我们的天空我们的天空我们的天空我们的天空我们的天空我们的天空我们的天空我们的天空我们的天空我们的天空我们的天空我们的天空我们的天空</p>
</div>
</body>
</html>
```
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-32bcb1dbdebf65e5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**position定位属性：**
值：static；relative；absolute；fixed
- **static默认没有定位**
top,bottom,left,right或者z-index声明
- **relative（相对定位）相对于自身：**定义元素框偏移某个距离，这个距离可以为负值。
格式如下：`p{position: relative;left: 70px;top：80px;}`，将这个属性加到上例代码中p选择器内。
此时会发生什么情况呢？我原本理解的是元素框向左偏移70px，向上偏移80px，但实际如下图：
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-a4343b51c5cc94c2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
relative描述为“生成相对定位的元素，相对于其正常位置（以元素框左上角为起点）进行定位。
注意：在使用相对定位时，无论是否进行移动，元素仍然占据原来的空间。因此，移动元素会导致它覆盖其它框。

**‘left:20’ 会向元素的left位置添加20 像素。**”
所以`position: relative;left: 70px;top：80px;`的意思是向元素框left添加70px，top添加80px，实际即所有的p元素向右下偏移指定的值。
`position:relative;left:-20px`的意思是从元素框左侧减去：“-20px”。
- **absolute（绝对定位）相对于static定位以外的第一个已定位的父元素：**如下：
```html
<head>
<style type="text/css">
h2.pos_abs
{
position:absolute;
left:100px;
top:150px
}
</style>
</head>
<body>
<h2 class="pos_abs">这是带有绝对定位的标题</h2>
<p>通过绝对定位，元素可以放置到页面上的任何位置。下面的标题距离页面左侧 100px，距离页面顶部 150px。</p>
</body>
```
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-d650585995ba6720.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
absolute绝对定位：绝对定位的元素的位置相对于最近的已定位祖先元素，如果元素没有已定位的祖先元素，那么它的位置相对于最初的包含块。
在本例中父元素为body，所以相对于整个页面进行定位。指的是h2的margin的角点距离整个页面左侧100px，距离页面顶部150px。因为margin也属于h2的一部分。
如果设置了absolute属性弹没有设置值，那么使用了absolute的元素在代码中在哪个位置在浏览器中就还是在那个位置，absolute属性定义的元素是脱离了文档流。
**设置为绝对定位的元素框从文档流完全删除，并相对于其包含块定位**，包含块可能是文档中的另一个元素或者是初始包含块。**元素原先在正常文档流中所占的空间会关闭，即完全脱离了正常的文档流，（可能覆盖在普通文本流上方），因此不占据空间，**就好像该元素原来不存在一样。**元素定位后生成一个块级框，而不论原来它在正常流中生成何种类型的框。**
提示：因为绝对定位的框与文档流无关，所以它们可以覆盖页面上的其它元素。可以通过设置 z-index 属性来控制这些框的堆放次序。

- **fixed（固定定位）相对于浏览器窗口**
元素的margin角点相对于整个窗口的定位。可以把fixed看作是absolute的特殊情况。

**注意：**
- 定位之后的元素A在显示页面上可能会覆盖原本在此位置上的普通刘元素B，A有多大就覆盖多达面积。
- 可用像素和百分比设置定位值。

**子元素在父元素中居中定位**
当子元素定位属性为absolute/fixed，这个时候子元素脱离了文本流，父元素定位属性为relative，在没有设置偏移量的情况下，子元素永远在父元素里面，设置了偏移量之后可能会离开父元素的界面。
在不知道父元素尺寸的情况下，将一个元素在父元素中居中放置，最简单的方式是，给父元素设定一个relative属性，子元素设定一个absolute/fixed属性，如下所示：
```html
<head>
<style type="text/css">
p {
	position: relative;
	padding: 50px;
	background-color: #f00;
}
span{position: absolute;
left: 50%;
top: 50%;
background-color: green;
transform: translate(-50%,-50%);}
</style>
</head>
<body>
	<p>aswwwwwwwwwwd <span>artfgyhjk</span></p>
</body>
```
span元素在p元素内，设定`span{left: 50%;top: 50%;}`，即span以p元素长宽为基数，以自身左上角为基点，向右偏移50%，向下偏移50%，此时span元素左上角与p元素中心点对齐。我们要实现的是中心点与中心点对齐，此时再额外设定一个`transform: translate(-50%,-50%)`,使span以自身的长宽为基数，以自身左上角为基点，向左偏移50%，向上偏移50%，成功啦~
**注意：以下这两段代码实现的效果相同**
```html
span{position: absolute;
left: 50%;
top: 50%;
background-color: green;
transform: translate(-50%,-50%);}
```

```html
span{position: absolute;
right: 50%;
bottom: 50%;
background-color: green;
transform: translate(50%,50%);}
```

**设置元素的形状**
检索或设置对象的可视区域。区域外的部分是透明的。
clip属性剪裁绝对定位元素，只有**当position的值设定为“absolute”或“fixed”时，clip属性才可以用。**
**clip值为auto（默认）和shape。**
- auto：默认不剪裁。
- shape：设置元素的形状，唯一合法的形状值是：rect (top, right, bottom, left)

rect(<number>|auto <number>|auto <number>|auto <number>|auto)： 依据上-右-下-左的顺序提供自对象左上角为(0,0)坐标计算的四个偏移数值，其中任一数值都可用auto替换，即此边不剪切。  
- 示例1：clip:rect(auto 50px 20px auto)

说明：上边不剪切，从右往左剪切到图片宽度为50px，从下往上剪切到图片高度为20px，左边不剪切。
- 示例2：clip:rect(10px 70px 40px 10px)

说明：图片从上往下剪切10px，从右往左剪切到图片宽度为（70-10）px，从下往上剪切到图片高度为（40-10）px，从左往右剪切10px
**即：盒子的实际高度为|bottom-top|，实际宽度为|right-left|。
（和截图时调整宽度和高度是一样的道理）**
