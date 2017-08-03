网页布局中，元素水平居中比垂直居中简单不少，同时实现水平垂直居中也不难，难的是想出多种实现水平垂直居中的方法并从中挑选最合适最容易理解的那一个完成我们的项目。
现在是响应式设计的时代，大多数情况下我们并不知道用户浏览器尺寸，也没有办法计算元素准确的宽高等，所以将宽高等属性值固定为某个具体的px不可行。
# 
以下是实现元素居中的几种实用方法：
### 1 . line-height大法好
 - **单行文本垂直居中**
如果一个标签没有定义height属性，那么其最终表现的告诉一定是由line-height起作用。网上大多说把line-height值设置为height一样的可实现单行文字的垂直居中。这句话确实是正确的，但这个height是多余的。
示例代码：为了方便大家看，我给body加了一个边框。
```
<style>
        body{
            border: 10px solid black;
        }
        p {
            line-height: 50px;
            background: red;
        }
</style>
<body>
    <p>单行文本垂直居中</p>
</body>
```
![效果图1-1](http://upload-images.jianshu.io/upload_images/6851923-b49a05f922273153.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

 - **多行文本垂直居中**
（1）对于高度不固定的文本，设置文本垂直居中直接使用padding就行。

![效果图1-2-1](http://upload-images.jianshu.io/upload_images/6851923-3f6e63c6052836ba.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

（2）对于高度固定的文本，里面的文字单行或多行显示，字体有大有小，要怎么实现垂直居中呢？
```
<style>
        p {
            line-height: 400px;
            border: 10px solid black;
        }

        span {
            background: red;
            display: inline-block;
            line-height: 1.4em;
            vertical-align: middle;
        }

         i{
            width: 0;
            display: inline-block;
            vertical-align: middle;
            font-size: 0;
        }    
</style>

<p>
      <span>多行文本垂直居中，多行文本垂直居中，多行文本垂直居中，<br />
        多行文本垂直居中，多行文本垂直居中，多行文本垂直居中，<br />多行文本垂直居中，多行文本垂直居中，多行文本垂直居中，
        多行文本垂直居中，多行文本垂直居中，多行文本垂直居中，多行文本垂直居中，多行文本垂直居中，多行文本垂直居中，</span><i>&nbsp</i> 
</p>
```
![效果图1-2-2](http://upload-images.jianshu.io/upload_images/6851923-db0f2746a26fe0c1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

去掉i元素，得到的效果也是相同的，所以这里有一点疑惑，先mark一下，待日后弄懂了回来补充。

 - **一张图片水平垂直居中**
```
<style>
        p {
            border: 10px solid black;
            line-height: 400px;
            text-align: center;
        }

        img {
            vertical-align: middle;
        } 
</style>
<p>
      ![](http://upload-images.jianshu.io/upload_images/6851923-1d0bad137381a9be.jpg!qt290?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
</p>
```
![效果图1-3-1](http://upload-images.jianshu.io/upload_images/6851923-37404b3b7d0c5757.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
    <style>
        a {
            border: 10px solid black;
            display: inline-block;
            text-align: center;
            vertical-align: middle;
        }

        img {
            vertical-align: middle;
            padding: 10px;
            margin: 10px;
        }
    </style>
    <a href="">![](http://upload-images.jianshu.io/upload_images/6851923-71abf5d916e8379c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
    </a>
```

![效果图3-1-2](http://upload-images.jianshu.io/upload_images/6851923-fee178ce4240ffbc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


 - **多图水平垂直居中（题外话，与line-height无关）**

```
html代码：
<p>
    ![](http://upload-images.jianshu.io/upload_images/6851923-71abf5d916e8379c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
</p>
<p>
    ![](http://upload-images.jianshu.io/upload_images/6851923-ffe49441b8fbdde9.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
</p>
<p>
    ![](http://upload-images.jianshu.io/upload_images/6851923-26782d6438e7bd4e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
</p>
<p>
    ![](http://upload-images.jianshu.io/upload_images/6851923-1d0bad137381a9be.jpg!qt290?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
</p>
<p>
    ![](http://upload-images.jianshu.io/upload_images/6851923-474e68348e2a0572.gif?imageMogr2/auto-orient/strip)
</p>
```
```
CSS代码：
p {
        background: yellow;
        width: 1em;
        height: 1em;
        padding: 0.1em;
        margin: 0.1em;
        font-size: 280px;
        float: left;
}

img {
        display: block;
        width: 100%;
        height: 100%;
        background-repeat: no-repeat;
        background-position: center;
}
```

![效果图](http://upload-images.jianshu.io/upload_images/6851923-309937e9f1d6d34c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


### 2 . text-align: center; ——给行内元素的父元素设置此样式使得行内元素水平垂直居中
```
<style>
        p {
            border: 10px solid black;
            text-align: center;
        }
</style>
<p>
        <span>这是一段文本</span>
</p>
```

![效果图2](http://upload-images.jianshu.io/upload_images/6851923-f4e0c0caea3107ce.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


### 3 . 块级元素水平居中margin: 0 auto;
```
    <style>
        p {
            border: 10px solid black;
        }
        img {
            display: block;
            width: 33%;
            margin: 0 auto;
        }
    </style>
    <p>
        ![](http://upload-images.jianshu.io/upload_images/6851923-1d0bad137381a9be.jpg!qt290?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
    </p>
```

![效果图3](http://upload-images.jianshu.io/upload_images/6851923-81ba6f9405547a6f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 4 . position & translate——绝对定位 & 偏移 实现水平垂直居中。
- 绝对定位元素的水平垂直居中
关键点：上下左右皆为0，margin为auto。
```
<style>
div{
            border: 10px solid black;
            width: 600px;
            height: 400px;
            position: absolute;
            top: 0;
            right: 0;
            bottom: 0;
            left: 0;
            margin: auto;
        }
</style>
<div></div>
```
![效果图4-1](http://upload-images.jianshu.io/upload_images/6851923-c487f3dd4c7f60b8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 绝对定位元素的水平垂直居中-偏移法：
关键点：left和top相对父元素，translate相对于自身。
```
<style>
p{
        position: absolute;          
        background: red;
        width: 200px;
        height: 200px;
        left: 50%;
        top: 50%;
        transform: translate(-50%,-50%);
} 
</style>
<p></p>
```

![效果图4-2](http://upload-images.jianshu.io/upload_images/6851923-f26b49c4c487c393.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 5 . display: table-cell;
关键点：需要添加额外元素作为外部容器,需要实现垂直居中的元素与其父元素都要设置vertical-align: middle;不然不能实现垂直居中。
```
    <style>
        * {
            padding: 0;
            margin: 0;
        }
        .center-aligned{
            display: table;
            background: #00a0ea;
            width: 100%;
            height: 300px;
        }
        .center-core{
            display: table-cell;
            text-align: center;
            vertical-align: middle;

        }
        .center-core img{
            width: 40%;
            vertical-align: middle;
            height: auto;
        }
    </style>
    <div class="center-aligned">
        <div class="center-core">
            ![](http://upload-images.jianshu.io/upload_images/6851923-1d0bad137381a9be.jpg!qt290?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
        </div>
    </div>
```

![效果图6](http://upload-images.jianshu.io/upload_images/6851923-8bef024ea1c229df.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


### 6 . display: flex;模型实现水平垂直居中
关键点：容器获得display:flex;属性，其他所有特性定义也都在容器元素內进行。
```
html代码如下：
<div id="item-container">
        <div class="circle"></div>
        <div class="square"></div>
        <div class="circle"></div>
</div>
```
```
设置基础样式：
        * {
            padding: 0;
            margin: 0;
        }

        #item-container {
            display: flex;
            background: yellow;
        }

        .circle {
            background: black;
            width: 100px;
            height: 100px;
            border-radius: 50%;
        }

        .square {
            background: #cdcdcd;
            width: 150px;
            height: 150px;
        }
```
![效果图6-1](http://upload-images.jianshu.io/upload_images/6851923-2db69aef56f4b76b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

水平居中：
```
        #item-container {
            justify-content: center;
        }
```
![效果图6-2](http://upload-images.jianshu.io/upload_images/6851923-85fd7e6752774f4f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

两端对齐：（玩一下）
```
        #item-container {
            justify-content: space-between;
        }
```
![效果图6-3](http://upload-images.jianshu.io/upload_images/6851923-afa0dfe019d46756.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

垂直居中：
```
        #item-container {
            align-items: center;
            heigh: 200px;
        }
```
![效果图6-4](http://upload-images.jianshu.io/upload_images/6851923-a57ce5c5dd232409.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



### 7 . calc()——适合内容宽高为固定尺寸的场景
关键点：top: 50%;left: 50%只是将p的左上角移到了div的中心点，要实现两个中心点重合，需要得到p自身宽高的一半。
```
    <style>
        * {
            padding: 0;
            margin: 0;
        }
        div {
            background: green;
            position: relative;
            min-height: 400px;
        }
        p {
            background: red;
            position: absolute;
            width: 200px;
            height: 200px;
            top: calc(50% - 200px/2);
            left: calc(50% - 200px/2);
        }
    </style>
    <div>
        <p>
        </p>
    </div>
```
![效果图7](http://upload-images.jianshu.io/upload_images/6851923-8d88190caebebb05.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



*参考资料*：
- [大小不固定的图片、多行文字的水平垂直居中 张鑫旭](http://www.zhangxinxu.com/wordpress/2009/08/%E5%A4%A7%E5%B0%8F%E4%B8%8D%E5%9B%BA%E5%AE%9A%E7%9A%84%E5%9B%BE%E7%89%87%E3%80%81%E5%A4%9A%E8%A1%8C%E6%96%87%E5%AD%97%E7%9A%84%E6%B0%B4%E5%B9%B3%E5%9E%82%E7%9B%B4%E5%B1%85%E4%B8%AD/#zhangxinxu_1)
- [Seven-Ways-of-Centering-With-CSS](http://thenewcode.com/723/Seven-Ways-of-Centering-With-CSS)
- [justify-content MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/justify-content)
- [A-Designers-Guide-To-Flexbox](http://thenewcode.com/780/A-Designers-Guide-To-Flexbox)
