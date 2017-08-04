### em、rem、vm、vw 分别如何计算尺寸的？
em：相对于当前元素字体大小，如2em为当前元素字体大小的两倍；
rem：相对于默认根元素字体大小，一般浏览器默认字体大小为16px，2rem就是32px；
vh：相对于视窗高度，1vh为视窗高度的1%，如视窗高度200px，80vh即为200px*80%=160px；
vw：相对于视窗宽度，1vw为视窗宽度的1%，如视窗宽度100px，60vw即为100px*60%=60px；
注意：“视窗”叫视区更合适，指浏览器内部的可视区域（即window.innerWidth/window.innerHeight）大小，不包含任务栏标题栏以及底部工具栏的浏览器区域。
vm：相对于视口的宽度或高度，取决于哪一个更小。

 -----
### 颜色有几种写法?透明色如何表示?透明效果如何实现？currentColor如何来用?
颜色写法：4种，分别是颜色关键字-如blue；十六进制值-如#abcdef或#333；RGB值-rgb(0,255,255)或rgb(50%,50%,50%)；HSL值（三个字母分别表示色相、饱和度、亮度，基于rgb值得来）-如hsl(276,100%,50%)。
# 
透明色：表示为RGBA & HSLA -- 其中A为Alpha，表示不透明度，如rgba(200,150,255,.5)，hsla(200,100%,50%,0.5)，.5和0.5都代表0.5，即当前颜色半透明。
要实现完全透明把Alpha设置为0即可，也可使用transparent关键字实现透明效果。
# 
currentColor关键字：代表原始的color属性的计算值。
用法：让继承自属性或子元素的属性的颜色属性以默认值不再继承。
也能用于那些继承了元素的 color 属性计算值的属性，相当于在这些元素上使用 inherit 关键字，如果这些元素有该关键字的话。

-----
### css 中calc是什么？实现一个footer 固定底部的效果，附上预览链接
[效果](https://dolbydot.github.io/demos/test/homework10-1.html) 
calc()是一个函数，括号内为一个数学表达式，表达式可以与加减乘除这四个运算符组合，该表达式结果会作为最终的值，我们可以通过计算来决定一个css属性的值。

-----
### 如下代码中，饥人谷3个字的样式是，原因？
![](http://upload-images.jianshu.io/upload_images/6851923-5f35aafa2c62503e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

结果：粉色， 14px
权值计算：
1、#msg：0,1,0,0=100;
2、#content p: 0,1,0,0+0,0,0,1=101;
3、.container .box p: (0,0,1,0)*2+0,0,0,1=21;
4、p#msg: 0,0,0,1+0,1,0,0=101;
2和4权值相同，即取得{color: blue; font-size: 14px;}和{color: pink; }这两个属性，未冲突的样式都会生效，冲突的样式采取后来居上原则。
所以上例最终结果为{color:pink;font-size:14px;}

----- 
### 下图所示的代码和效果中，为什么 h1 的字体大小没变化? 为什么 a 的颜色没变化?

![](http://upload-images.jianshu.io/upload_images/6851923-20770b3f481dd487.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

h1字体大小变化了，只是没有变成12px而已。h1默认样式为2em，表现在浏览器中是32px，设置font-size是12px后，继承自div的12px被划掉，h1默认字体大小仍是2em，但字号变为24px。
继承没有特殊性，浏览器对a有默认样式（user agent stylesheet），color:-webkit-link;，由于css层叠，继承自div的red被划掉了，即继承的样式与浏览器默认样式冲突，被浏览器默认样式覆盖，直接定义a的颜色是可以生效的。

-----
### 盒模型有哪些属性？
内容区：width,height,min-width,max-width,min-height,max-height
边框：border,border-top,border-right,border-bottom,border-left
内边距：padding,padding-top,padding-right,padding-bottom,padding-left
外边距：margin,margin-top,margin-right,margin-bottom,margin-left

-----
### 什么是标签的默认样式？列举几个带默认样式的标签，并写出默认样式的属性-值
为了没有样式表也能活着，浏览器都有自己的一套默认样式，不同的浏览器和不同版本的浏览器的默认样式都不相同。
部分带默认样式的标签：
a{color:-webkit-link;text-decoration:underline;}
h1-h6：font-size依次为2em,1.5em,1.17em,1.12em,0.83em,0.75em，且默认font-weight为bolder。
p与h4默认字号相同。
:link,:visited,:focus{text-decoration:underline;}
body{ margin: 8px; }
html, address,blockquote,body, dd, div,dl, dt, fieldset, form,frame, frameset,h1, h2, h3, h4,
h5, h6, noframes,ol, p, ul, center,dir, hr, menu, pre { display: block; unicode-bidi: embed ;}
li{ display: list-item; }
pre:{ white-space: pre }

-----
### 元素class 为 box，宽度400px，高度500px，边框2px、实线、#ccc，背景色为红色，在浏览器居中展示，上外边距为40px。
[预览链接](https://dolbydot.github.io/demos/test/homework10.html)

-----
### 回答如下截图中的两个问题
![](http://upload-images.jianshu.io/upload_images/6851923-f91574802fe1fdad.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

body是父元素，浏览器默认body有8px的margin，所以蓝色区域外会有缝隙；默认的h1有上下margin，所以红色区域上下有缝隙。
清除：
设置:*{margin:0;}或body,h1{margin:0;}

-----
### 列举display 的几个值
inline-生成一个或多个行盒
block-块元素盒
list-item-容纳内容和单独的列表行盒的块状盒
inline-block-块状行盒
table-相当于<table>
table-cell-相当于<td>
table-row-相当于<tr>
flex-类似于块元素，并根据flexbox模型布局其内容
inline-flex-类似于行内元素，并根据flexbox模型布局其内容
grid-类似于块元素，并根据grid模型布局其内容
inline-grid-类似于行内元素，并根据grid模型布局其内容

-----
### 块级元素和行内元素分别有什么特点？分别列举二者对应的标签
[块级元素和行内元素](http://www.jianshu.com/p/3937727285db)

-----
### box-sizing: border-box； 是什么意思？
告诉浏览器去理解你设置的边框和内边距的值是包含在width内的。也就是说，如果你将一个元素的width设为100px,那么这100px会包含其它的border和padding，不包括margin，内容区的实际宽度会是width减去(border + padding)的计算值。这使得我们更容易的去设定一个元素的宽高。
维度计算：
width = 左右border + 左右padding + content width
height = 上下border + 上下padding + content height

-----
### inline-block有什么作用？inline-block的缝隙是怎么回事？如何解决
inline-block是一个块状行盒，表现为一个行内元素，它既拥有了块状元素可以设置width和height的特性，又保留了行内元素不换行的特点。比如之前做横向菜单栏时可以用li和float实现，现在也可以用display:inline-block;实现。
有缝隙的原因：inline-block水平呈现的元素间，标签段之间换行显示或空格分隔的情况下会有间距，这是符合规范的应有表现。
解决方法：
方法1、去掉HTML中标签段之间的空格或用注释代替空格
方法2、设置margin值为负
方法3、去掉inline-block元素的闭合标签
方法4、设置inline-block元素letter-space值为0，其父元素letter-space值为负值

-----
### 动手题
[预览链接](https://dolbydot.github.io/demos/task15-a%20simple%20page.html)
