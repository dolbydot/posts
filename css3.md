3/20/2017 2:17:41 PM 
#### CSS3边框 ####
**border-radius**
定义圆角的形状。上右下左原则。

**border-image**
使用图片创建边框。

**box-shadow**
向方框添加阴影。
**语法**：box-shadow: h-shadow（必需 水平阴影） v-shadow（必需 垂直阴影） blur（模糊距离） spread（阴影尺寸） color（阴影颜色） inset（将外部阴影改为内部阴影）;
**说明**：可实现类似照片叠加拼图的效果。

#### CSS3背景 ####
**background-size**
可以以像素或百分比规定尺寸。如果以**百分比**规定尺寸，那么尺寸**相对于父元素的宽度和高度**。
```html
<!DOCTYPE html>
<html>
<head>
<style> 
body
{
background:url(/i/bg_flower.gif) red;
background-size:63px 100px;
-moz-background-size:63px 100px; /* 老版本的 Firefox */
background-repeat:no-repeat;
padding-top:80px;
}
</style>
</head>

<body>
<p>上面是缩小的背景图片。</p>

<p>原始图片：![](/i/bg_flower.gif)</p>

</body>
</html>
```
上面代码效果如下：
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-3e461e5750240320.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
其中body{padding-top:80px;}指的是body元素相对于自身，有一个80px的上内边距，即第一行文本元素距离页面顶部有一个80px的距离，这个值与背景图片无关。

将padding-top值设置为40px，结果如下：
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-d1ca4b531926f33e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**background-origin**
规定背景图片的定位区域。背景图片可以放置于 content-box、padding-box 或 border-box 区域。
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-002dc268304a7950.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
```html
<!DOCTYPE html>
<html>
<head>
<style> 
body
{
background: url('C:/Users/dolby/Pictures/yh2.jpg') 100px 300px no-repeat,url('C:/Users/dolby/Pictures/yh1.jpg') 110px 400px no-repeat;
}
div
{
border:20px solid black;
padding:20px;
background:url('C:/Users/dolby/Pictures/zl.jpg') no-repeat yellow;
background-size: 80px 60px;
color: red;
}
#div1
{
background-origin:border-box;
background-position:left;
}
#div2
{
background-origin:padding-box;
background-position:right;
}
#div3
{
background-origin:content-box;
background-position:top right;
}
</style>
</head>
<body>

<p>background-origin:border-box:</p>
<div id="div1">
这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。
</div>

<p>background-origin:content-box:</p>
<div id="div2">
这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。
</div>

<p>background-origin:padding-box:</p>
<div id="div3">
这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。这是文本。
</div>
</body>
</html>
```
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-3838e52bf102e3a8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**background-clip**
规定背景的绘制区域。
和background-origin一样，值也为"border-box(默认)/content-box/padding-box"
```html
<!DOCTYPE html>
<html>
<head>
<style> 
div
{
width:100px;
height:100px;
padding:10px;
background-color:yellow;
background-clip:content-box;
border:2px solid #92b901;
}
</style>
</head>
<body>

<div>
这是文本。这是文本。这是文本。
</div>

</body>
</html>
```
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-c97d290e0ffd3c19.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
若没有规定background-clip:content-box;则黄色背景会从边框开始填满。

#### CSS3文本效果 ####
**text-shadow**
给文本添加阴影。
**语法**：text-shadow: h-shadow（必需 水平阴影） v-shadow（必需 垂直阴影） blur（模糊距离） color（阴影颜色）;

**word-wrap**
允许文本在元素内强制换行。（即解决前面经常遇到的问题：写一行很长的sssssssss但不加空格，就会认为这是一整个单词而不进行拆分，表现出来的效果有问题）
```html
<!DOCTYPE html>
<html>
<head>
<style> 
p.test
{
width:11em; 
border:1px solid #000000;
word-wrap:break-word;
}
</style>
</head>
<body>

<p class="test">This paragraph contains a very long word: thisisaveryveryveryveryveryverylongword. The long word will break and wrap to the next line.</p>

</body>
</html>
```
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-8a5329a852c63cf4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
去掉`word-wrap:break-word;`表现如下：
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-2723abe2525d550b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### CSS3字体 ####
通过@font-face规则定义任意喜欢的字体。
```html
<!DOCTYPE html>
<html>
<head>
<style> 
@font-face
{
font-family: myFirstFont;
src: url('/example/css3/Sansation_Light.ttf')
    ,url('/example/css3/Sansation_Light.eot'); /* IE9+ */
}

@font-face
{
font-family: myFirstFont;
src: url('/example/css3/Sansation_Bold.ttf')
    ,url('/example/css3/Sansation_Bold.eot'); /* IE9+ */
font-weight:bold;
}

div
{
font-family:myFirstFont;
}
</style>
</head>
<body>

<div>
With CSS3, websites can <b>finally</b> use fonts other than the pre-selected "web-safe" fonts.
</div>

<p><b>注释：</b>Internet Explorer 9+ 支持新的 @font-face 规则。Internet Explorer 8 以及更早的版本不支持新的 @font-face 规则。</p>

</body>
</html>
```
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-2f385a59d33c6226.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
如上，在新的@font-face规则中，必须首先定义字体的名称（比如 myFirstFont），然后指向该字体文件，通过font-family属性来引用字体的名称(myFirstFont)。
而当font-family的文本需要显示为粗体，也就是当使用了b标签时，需要另外添加一个包含该字体粗体的字体文件，为相同的字体设置许多@font-face规则来达到我们的目的。
当去掉上述代码中的第二段@font-face后，显示效果如下：
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-927791c26421ceeb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
**语法规则示例：**
```html
<style>
@font-face
{
font-family:myFirstFont; 
src: url('Sansation_Light.ttf'),
url('Sansation_Light.eot'); /* IE9+ */
}
div
{
font-family:myFirstFont;
}
</style>
```

#### CSS 2D转换 ####
属性：transform
值：
- translate()定义偏移量left和top
```html
<!DOCTYPE html>
<html>
<head>
<style> 
body
{
background:red;
}
div
{
width:100px;
height:75px;
background-color:yellow;
border:1px solid black;
}
div#div2
{
transform:translate(50px,100px);
-ms-transform:translate(50px,100px); /* IE 9 */
-moz-transform:translate(50px,100px); /* Firefox */
-webkit-transform:translate(50px,100px); /* Safari and Chrome */
-o-transform:translate(50px,100px); /* Opera */
}
div#div3
{
transform:translate(-50%,-50%);
-ms-transform:translate(-50%,-50%); /* IE 9 */
-moz-transform:translate(-50%,-50%); /* Firefox */
-webkit-transform:translate(-50%,-50%); /* Safari and Chrome */
-o-transform:translate(-50%,-50%); /* Opera */
}
</style>
</head>
<body>
<div>你好。这是一个 div 元素。</div>
<div id="div2">你好。这是一个 div 元素。</div>
<div id="div3">你好。这是一个 div 元素。</div>
</body>
</html>
```
效果如下：
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-e5959034d2f852b4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
元素会**以自身中心点为原点**（即原本所在的位置的中心点）偏移一定的长度，`transform:translate(50px,100px);`表示在中心点左边添加50px，在中心点上方添加100px。
也可用比例来表示，`transform:translate(-50%,-50%);`表示以中心点为原点，向X轴左边添加自身宽度的-50%，向Y轴上方添加自身高度的-50%。

- rotate()定义旋转角度
```html
<!DOCTYPE html>
<html>
<head>
<style> 
div
{
margin:30px;
width:200px;
height:100px;
background-color:yellow;
/* Rotate div */
transform:rotate(9deg);
-ms-transform:rotate(9deg); /* Internet Explorer */
-moz-transform:rotate(9deg); /* Firefox */
-webkit-transform:rotate(9deg); /* Safari 和 Chrome */
-o-transform:rotate(9deg); /* Opera */
}
</style>
</head>
<body>
<div>Hello World</div>
</body>
</html>
```
元素会**以自身中心点为原点**旋转一定角度，角度值为正即顺时针旋转，负值为逆时针。

- scale()定义元素尺寸在X轴和Y轴上的**成比例缩放**。
```html
<!DOCTYPE html>
<html>
<head>
<style> 
div
{
width:100px;
height:75px;
background-color:yellow;
border:1px solid black;
}
div#div2
{
margin:100px;
transform:scale(2,4);
-ms-transform:scale(2,4); /* IE 9 */
-moz-transform:scale(2,4); /* Firefox */
-webkit-transform:scale(2,4); /* Safari and Chrome */
-o-transform:scale(2,4); /* Opera */
}
</style>
</head>
<body>
<div>你好。这是一个 div 元素。</div>
<div id="div2">你好。这是一个 div 元素。</div>
</body>
</html>
```
如果没有设定div#div2，那么两个div元素应该是上下紧凑排列的，但上面代码的效果是：
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-057bca048b68094c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
div2相对于它原本应该在的地方，添加了100px的margin，即位置移到了第一个div的右下角并不与之相交，然后以自身中心点为原点，宽度变为原来的2倍，高度变为原来的4倍。

- skew()定义水平X及垂直Y翻转拉伸。
```html
<!DOCTYPE html>
<html>
<head>
<style> 
div
{
width:100px;
height:75px;
background-color:yellow;
border:1px solid black;
}
div#div2
{
transform:skew(30deg,20deg);
-ms-transform:skew(30deg,20deg); /* IE 9 */
-moz-transform:skew(30deg,20deg); /* Firefox */
-webkit-transform:skew(30deg,20deg); /* Safari and Chrome */
-o-transform:skew(30deg,20deg); /* Opera */
}
</style>
</head>
<body>
<div>你好。这是一个 div 元素。</div>
<div id="div2">你好。这是一个 div 元素。</div>
</body>
</html>
```
值skew(30deg,20deg)**围绕**X轴把元素翻转30度，围绕Y 轴翻转20度。

- matrix()将所有的2D转换方法组合，需要6个参数，矩阵为3*3，包括函数，允许旋转、缩放、移动及倾斜元素，注意：translate, rotate等方法都是需要单位的，而matrix方法e,f参数的单位可以省略。

[transform:matrix详细介绍](http://www.zhangxinxu.com/wordpress/2012/06/css3-transform-matrix-%E7%9F%A9%E9%98%B5/)
以下线性代数知识：
![线性代数](http://upload-images.jianshu.io/upload_images/6851923-4e36b57499fe1da9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


**设原始基点H坐标为(x,y)，transform:matrix(a,b,c,d,e,f)**

1. 用于偏移translate时，变换后基点H'(x'=ax+cy+e,y'=bx+dy+f)，在不设置transform-origin属性时默认矩阵基点为(0,0),这时候得到的变换后基点坐标为H'(e,f)；
2. 用于缩放scale时，参数a和d分别表示X轴和Y轴缩放比例，那么对于matrix(a,0,0,d,0,0)即缩放后H'(x'=ax+cy+e=ax,y'=bx+dy+f=dy)
3. 当matrix应用于旋转rotate时，假设角度为θ，那么`matrix(cosθ,sinθ,-sinθ,cosθ,0,0)`，结合矩阵公式，变化后的坐标为x'=x*cosθ-y*sinθ+0=x*cosθ-y*sinθ
y'=x*sinθ+y*cosθ+0=x*sinθ+y*cosθ
例子：
```html
transform:matrix(0.866,0.5,-0.5,0.866,0,0);
```
上面代码表示将元素旋转30°
4. 用于拉伸skew()时，只与b,c相关，对于matrix(1,tan(θy),tan(θx),1,0,0)，套用公式得到x'=x+y*tan(θx)+0=x+y*tan(θx)y'=x*tan(θy)+y+0=x*tan(θy)+y，即2D动作之后得到的基点坐标为H'[x+y*tan(θx),y+x*tan(θy)]
那么，举个例子，设matrix(2,3,4,5,6,7):
当基点坐标为(x,y)时，矩阵之后得到的基点坐标为H'(2x+4y+6,3x+5y+7),元素宽度为原来的2倍，高度为原来的5倍，还存在拉伸和旋转角度。当然，一般不会存在这么奇怪的6个参数。
5. **用matrix实现镜像效果：**
镜像对称轴永远经过原点(0,0),那么对称轴可以用y=kx表示，已知点(x,y),求其对称点(x',y')坐标。

![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-59851df345312d5c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
计算步骤如下：
(y-y') / (x - x') = -1/ k
(x + x') / 2 * k = (y + y')/2
得到：
ky-ky' = -x+x'
kx+kx' = y+y'
提出x' y':
x' = (1-k*k)/(k*k+1) *x + 2k/(k*k+1) *y;
y' = 2k/(k*k+1) *x + (k*k-1)/(k*k+1) *y;
结合矩阵公式：
x' = ax+cy+e;
y' = bx+dy+f;
可以得到：
a = (1-k*k)/(k*k+1);
b = 2k/(k*k+1);
c = 2k/(k*k+1);
d = (k*k-1)/(k*k+1);

3/21/2017 2:36:16 PM 
**transform-origin属性**
允许您改变被转换元素的基点位置。
2D转换元素能够改变元素x和y轴。3D 转换元素还能改变其Z轴。
