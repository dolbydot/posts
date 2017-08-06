### 浮动元素有什么特征？对父容器、其他浮动元素、普通元素、文字分别有什么影响?
1. 特征：
- 脱离正常文档流，沿其容器的左侧或右侧放置，外边缘碰到包含框或另一浮动元素的边缘时会停下，文本和内联元素将环绕它。
- float的计算值不为none。
- float意味着使用块布局，所以某些情况下可以修改display的计算值，如给inline元素或inline-block设置float属性，其display属性就被隐性设置为block。
- 提升层次半级。

2. 影响：
- 对父容器：元素浮动后脱离正常文档流，导致无法撑开父元素，造成父元素高度塌陷，除非给父元素也设置浮动或overflow属性。
- 对其他浮动元素：浮动元素会紧贴同一方向上其他浮动元素排列，父元素宽度不够的情况下会换行；反方向的浮动元素位于同一水平线上分别浮动、互不影响，但空间不够时也会被挤下，被迫换行。
- 对普通元素：浮动元素虽和绝对定位元素有所差别，但同样是脱离了正常文档流，普通元素察觉不到其存在，会占用它原本的空间。
- 对文字：文字环绕浮动元素。

### 清除浮动指什么? 如何清除浮动? 两种以上方法
1. 清除浮动：元素浮动之前在标准流中纵向排列，浮动之后可以理解为横向排列，所以清除浮动可以理解为打破横向排列。

2. 如何清除：
- `clear:both|left|right`：分别表示元素被向下移动用于清除之前的所有／左／右浮动，适用于浮动和非浮动元素。
举个例子：
比如页面中只有两个元素div1和div2，都是左浮动，父元素宽度足够的情况下，div2会跟随在div1后面。

![](http://upload-images.jianshu.io/upload_images/6851923-f5ef323dd14918a8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

但我们希望div2能够排列在div1下面，就像div1没有浮动而div2左浮动一样，这时就要用到清除浮动，我们应在div2中设置"clear: left;"来指定div2左边不允许出现浮动元素，这样div2就被迫下移一行。

![](http://upload-images.jianshu.io/upload_images/6851923-569e0bb85db15c72.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**结论：clear规则只影响使用清除的元素本身，不能影响其他元素**。

- `overflow: hidden/auto;`：不存在结构化和语义化问题，代码量少，但内容增多时可能会导致内容隐藏，无法显示需要溢出的内容。

- 浮动元素的父元素也设置浮动：下面的BFC一题中有举例。

- 浮动元素的父元素设置`display:table;`：改变了盒模型属性所以可能会造成一系列问题。

- 使用::after伪元素：结构和语义化完全正确、代码量居中，但复用方式造成代码量增加。

### 有几种定位方式，分别是如何实现定位的，参考点是什么，使用场景是什么？
三种定位方式：普通流、position定位、浮动。默认普通流。
- 普通流定位：
块级框从上到下一个接一个地排列，框之间的垂直距离是由框的垂直margin计算出来（margin合并）。
由一行形成的水平框称为行框（Line Box），行框的高度总是足以容纳它包含的所有行内框。
行内框在一行中水平布置。可以使用水平padding、border和margin调整它们的间距。但是，垂直内边距、边框和外边距不影响行内框的高度。
- position定位：值：static|relative|absolute|fixed；
`static`默认没有定位；
`relative`相对于自身正常位置左上角定位，定义元素框偏移某个距离，这个距离可以为负值。在使用相对定位时，无论是否进行移动，元素仍然占据原来的空间，因此移动元素会导致它覆盖其它框。相对定位一般用于需要绝对定位的子元素的父元素中。
`absolute`绝对定位，相对于static定位以外最近的已定位的祖先元素，如果没有已定位的祖先元素，那么它的位置相对于最初的包含块。如果设置了absolute但没有设置值，那么使用了absolute的元素在页面中的位置不会改变，但已经脱离了文档流，与普通流已不在一个index-z层面上，因此不占据空间，其他元素表现得就好像该元素不存在一样，元素定位后生成一个块级框，而不论原来它在正常流中是何种类型的框。比如需要一个元素水平垂直居中就会用到absolute。
`fixed`相对于浏览器窗口固定定位，元素的margin角点相对于整个窗口定位，可以把fixed看作是absolute的特殊情况。定位之后的元素A在显示页面上可能会覆盖原本在此位置上的普通流元素B，A有多大就覆盖多达面积。比如有些块框需要固定在页面上方就可以用fixed。
- float浮动定位：值：none|left|right；
值不为none的情况下，浮动定位与绝对定位一样会脱离正常文档流，沿其容器的左侧或右侧放置，外边缘碰到包含框或另一浮动元素的边缘时会停下，普通元素察觉不到浮动元素存在会占用它原本的空间，文本和内联元素将环绕它。比如需要做一个有按钮的导航栏就可以用到浮动。

### z-index 有什么作用? 如何使用?
1. 作用：
z-index属性设置元素的堆叠顺序。该属性设置一个定位元素沿z轴的位置，z轴定义为垂直延伸到显示区的轴。
2. 使用：
z-index的值默认为auto，即堆叠顺序继承自父元素，也可设置值为number，number值可以为负数。如果为正数，则离用户更近，为负数则表示离用户更远，拥有更高堆叠顺序（number值越大）的元素总是会处于堆叠顺序较低的元素的上面。
**注意**：z-index只能在定位元素上奏效（例如 position:absolute;）

### position:relative和负margin都可以使元素位置发生偏移，二者有什么区别？
- relative是相对定位，还在正常文档流中，无论元素是否进行移动它都仍占据原来的空间，也就是说其他的元素的位置不会发生改变。移动元素可能会覆盖其他的框，因为它的z-index层级发生了改变，可理解为只会重绘，不会回流。
- 负margin会影响文档中其他元素的位置，造成页面的回流与重绘。

### BFC 是什么？如何生成 BFC？BFC 有什么作用？举例说明。
1. BFC——block formatting context：块格式化上下文，是Web页面的可视化CSS渲染的一部分，是块盒子的布局发生、浮动、互相交互的区域。通俗理解，首先BFC是一个独立的布局环境，我们可以理解为一个箱子（实际上是看不见摸不着的），箱子里面物品的摆放是不受外界的影响的，反之也如此。

2. 如何生成：一个**块格式化上下文**由以下之一创建：
- 根元素或其它包含它的元素
- 浮动(元素的 float不是 none)
- 绝对定位的元素(元素的position为 absolute或 fixed)
- 内联块 inline-blocks (元素具有display: inline-block)
- 表格单元格 (元素具有display: table-cell，HTML表格单元格默认属性)
- 表格标题 (元素具有 [display: table-caption, HTML表格标题默认属性)
- 块元素具有overflow ，且值不是 visible
- display:flow-root

3. 作用：
- 自适应两栏布局：
设置浮动使元素脱离正常文档里，生成BFC，与normal状态下的元素互不影响，由此形成自适应两栏布局。

![](http://upload-images.jianshu.io/upload_images/6851923-4d6a76ecc8cf2813.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 防止垂直方向上的margin合并：
设置了绝对定位的p生成了一个BFC，与其他两个p不属于同一个BFC，不会发生margin合并。

![](http://upload-images.jianshu.io/upload_images/6851923-b4f8db60ef8a2412.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 清除浮动，防止内部塌陷
子元素设置了浮动脱离了正常文档流，那么其父元素也要设置浮动或者overflow属性来生成BFC去包裹子元素，才不会造成高度塌陷。

![](http://upload-images.jianshu.io/upload_images/6851923-c2c078e3b1d6e96c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 在什么场景下会出现外边距合并？如何合并？如何不让相邻元素外边距合并？给个父子外边距合并的范例。
1. **概念**：
块的顶部外边距和底部外边距有时被组合(折叠)为单个外边距，其大小是组合到其中的最大外边距，这种行为称为外边距塌陷(margin collapsing)，有的地方翻译为外边距合并。

2. **合并场景及如何合并**——垂直方向上合并。
- 相邻的兄弟元素（除非后一个兄弟元素的出现是为了清除浮动）：兄元素的下外边距和弟元素的上外边距挨到了一起就会发生外边距合并，合并之后的外边距不是兄-下外边距与弟-上外边距之和，而是两者间较大的那个，可以理解为取并集。

- 块级父元素与其第一／最后一个子元素：当块级父元素中不存在上边框、上内边距、內联元素、清除浮动这四条属性时，此块级父元素会与其第一个子元素发生上外边距合并，此时父元素对外展现出来的上外边距将直接变成这个父元素和其第一个子元素的margin-top较大者；类似的，若块级父元素的 margin-bottom 与它的最后一个子元素的margin-bottom之间没有父元素的 border、padding、inline content、height、min-height、max-height分隔时，就会发生下外边距合并现象。

- 空块元素：如果存在一个空的块级元素，其 border、padding、inline content、height、min-height 都不存在。那么此时它的上下边距中间将没有任何阻隔，此时它的上下外边距将会合并，即自身合并。

元素按照以上规则发生合并，即使外边距为0，这些规则也仍旧生效。因此，无论父元素的外边距是否为0，第一个或者最后一个子元素的外边距会被父元素的外边距"截断"，在负外边距的情况下，合并后的外边距为最大正外边距与最小负外边距之和。这就是一系列段落元素占用空间非常小的原因。

3. 阻止相邻元素外边距合并：[BFC](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Block_formatting_context)-块格式化上下文——会阻止元素外边距合并，如把元素设置为浮动和绝对定位那么它的外边距不会发生合并。

4. 父子外边距合并示例：
```
<style>
        .dad {
            background: red;
            width: 200px;
            height: 200px;
            margin: 20px;
        }
        .son {
            background: yellow;
            width: 100px;
            height: 100px;
            margin: 30px;
        }
</style>
<div class="dad">
    <div class="son"></div>
</div>
```
![](http://upload-images.jianshu.io/upload_images/6851923-6aaac46cdc77bb77.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 代码
[代码1](https://dolbydot.github.io/task/task10/code1.html)
[代码2](https://dolbydot.github.io/task/task10/code2.html)
[代码3](https://dolbydot.github.io/task/task10/code3.html)
[代码4](https://dolbydot.github.io/task/task10/code4.html)

**参考资料**：
- [*mdn float*](https://developer.mozilla.org/zh-CN/docs/CSS/float)
- [*CSS浮动与清除浮动*](http://www.cnblogs.com/zhongxinWang/archive/2013/03/27/2984764.html)
- [*CSS浮动、定位*](http://www.cnblogs.com/wlf1112/p/6245502.html)
- [*清除浮动*](http://www.iyunlu.com/view/css-xhtml/55.html)