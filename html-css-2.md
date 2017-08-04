2/23/2017 10:27:57 PM 
#### CSS多重属性： ####
若一个属性同时被外部样式表和内部样式表中的同名选择器定义，如下：
外部样式表：
```html
h3 {
  color: red;
  text-align: left;
  font-size: 8pt;
  }
```
内部样式表
```html
h3 {
  text-align: right; 
  font-size: 20pt;
  }
```
那么最终h3得到的样式是：
```html
color: red; 
text-align: right; 
font-size: 20pt;
```
即：有冲突的部分优先选用内部样式表样式，无冲突部分直接取用。

----------
#### 设置背景图片示例： ####
1. 网页图片：直接插入网页图片链接。
```html
body
  { 
  background-image: url(http://img05.tooopen.com/images/20150830/tooopen_sy_140703593676.jpg);
  background-repeat: repeat-y;
  }
```
2. 本地图片：“./”表示图片位于正在被编辑的html文件所在的文件夹，如果图片位于正在被编辑的html文件所在的文件夹的上级文件夹，则变为“../”
```html
body
  { 
  background-image: url(./tooopen_sy_140703593676.jpg);
  background-repeat: repeat-y;
  }
```

----------
#### background-repeat背景重复 ####
如果需要在页面上对背景图像进行平铺，可以使用 background-repeat 属性。
属性值 repeat 导致图像在水平垂直方向上都平铺，就像以往背景图像的通常做法一样。repeat-x 和 repeat-y 分别导致图像只在水平或垂直方向上重复，no-repeat 则不允许图像在任何方向上平铺。
默认地，背景图像将从一个元素的左上角开始。请看下面的例子：
```html
body
  { 
  background-image: url(/i/eg_bg_03.gif);
  background-repeat: repeat-y;
  }
```

#### background-position背景定位 ####
下面的例子在 body 元素中将一个背景图像居中放置：
```html
body
  { 
    background-image:url('/i/eg_bg_03.gif');
    background-repeat:no-repeat;
    background-position:center;
  }
```
为 background-position 属性提供值有很多方法。
1. 可以使用一些关键字：top、bottom、left、right 和 center。
通常，这些关键字会成对出现，其作用如其名称所表明的。例如，top right 使图像放置在元素内边距区的右上角。
根据规范，位置关键字可以按任何顺序出现，只要保证不超过两个关键字 - 一个对应水平方向，另一个对应垂直方向。
如果只出现一个关键字，则认为另一个关键字是 center。
所以，如果希望每个段落的中部上方出现一个图像，只需声明如下：
```html
p
  { 
    background-image:url('bgimg.gif');
    background-repeat:no-repeat;
    background-position:top;
  }
```
这里要说明的是：
**单一关键字=等价的关键字**
center=center center
top=top center/ center top
bottom=bottom center/center bottom
right=right center/center right
left=left center/center left
2. 百分数值
百分数值的表现方式更为复杂。假设你希望用百分数值将图像在其元素中居中，这很容易：
```html
body
  { 
    background-image:url('/i/eg_bg_03.gif');
    background-repeat:no-repeat;
    background-position:50% 50%;
  }
```
这会导致图像适当放置，其中心与其元素的中心对齐。
换句话说，百分数值同时应用于元素和图像。也就是说，图像中描述为 50% 50% 的点（中心点）与元素中描述为 50% 50% 的点（中心点）对齐。
如果图像位于 0% 0%，其左上角将放在元素内边距区的左上角。如果图像位置是 100% 100%，会使图像的右下角放在右边距的右下角。
**注意！！！**
**用百分比指定背景图像填充的位置，可以为负值。其参考的尺寸为容器大小减去背景图片大小 **

```html
body
  { 
    background-image:url('/i/eg_bg_03.gif');
    background-repeat:no-repeat;
    background-position:66% 33%;
  }
```

如上例，偏移前图片左上角默认与页面左上角重合，图片左上角坐标为（0，0），水平偏移66%，垂直偏移33%，偏移后左上角坐标为【（页面长度-图片长度）*66%，（页面宽度-图片宽度）*33%】，最后得到的效果是，页面中没被平铺满的白色区域，左侧宽度：右侧宽度=2：1，上侧宽度：下侧宽度=1：2。
若`background-position:60% 20%;`，则页面中没被平铺满的白色区域中，左侧宽度：右侧宽度=3：2，上侧宽度：下侧宽度=1：4。**
如果只提供一个百分数值，所提供的这个值将用作水平值，垂直值将假设为 50%。这一点与关键字类似。
background-position 的默认值是 0% 0%，在功能上相当于 top left。这就解释了背景图像为什么总是从元素内边距区的左上角开始平铺，除非设置了不同的位置值。
3. 使用长度值，如 100px 或 5cm.
长度值解释的是元素内边距区左上角的偏移。偏移点是图像的左上角。
比如，如果设置值为 50px 100px，图像的左上角将在元素内边距区左上角向右 50 像素、向下 100 像素的位置上：
```html
body
  { 
    background-image:url('/i/eg_bg_03.gif');
    background-repeat:no-repeat;
    background-position:50px 100px;
```
偏移只是从一个左上角到另一个左上角。也就是说，图像的左上角与 background-position 声明中的指定的点对齐。(点到点，直接加减)
