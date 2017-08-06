### text-align: center的作用是什么，作用在什么元素上？能让什么元素水平居中？
作用：定义行内内容居中。
作用元素：行内元素的块级父元素。
生效元素：行内元素。

### IE 盒模型和W3C盒模型有什么区别?
box-sizing属性用于更改计算元素宽度和高度的盒子模型。
- **IE盒模型**即`box-sizing: border-box;`：
width = 左右border + 左右padding + 内容区 width；
height = 上下border + 上下padding + 内容区 height；
- **W3C盒模型（又叫标准盒模型）**即`box-sizing: content-box;`（默认值）：
width = 内容区 width；
height = 内容区 height；

**所以IE 盒模型和W3C盒模型区别在于宽高的计算方式**。
下图可以直观地看出二者计算结果的区别：

![](http://upload-images.jianshu.io/upload_images/6851923-ce65d9dc05af79ce.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### *{ box-sizing: border-box;}的作用是什么？
把标准盒模型转换为IE盒模型，告诉浏览器去理解你设置的边框和内边距的值是包含在width内的。

### line-height: 200%和line-height: 2有什么区别?
**line-height：200%**——值200%是一个百分比，与元素自身的字体大小有关，计算值是给定的百分比值乘以元素计算出的字体大小。
**line-height：2**——值2是一个数字值number，没有单位，并不是一个CSS尺寸，大多数情况下，使用number设置line-height是首选方法，在继承情况下不会有异常的值。
有没有感觉以上概念看不懂啊^ - ^，先上一段代码～
```
—————————————————————————————————————————————————————————————————————————— html代码
<div class="dad">
        我是爸爸
    <div class="son">
            我是儿子<br /> 喜欢篮球
    </div>
</div>
```
```
—————————————————————————————————————————————————————————————————————————— css代码1
<style>
        .dad {
            line-height: 200%;
            font-size: 16px;
            background: yellowgreen;
        }

        .son {
            font-size: 30px;
            background: pink;
        }
</style>
```
![1-1](http://upload-images.jianshu.io/upload_images/6851923-a555fb5927d5ed94.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![1-2](http://upload-images.jianshu.io/upload_images/6851923-932d292b2864e044.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
—————————————————————————————————————————————————————————————————————————— css代码2
<style>
        .dad {
            line-height: 2;
            font-size: 16px;
            background: yellowgreen;
        }

        .son {
            font-size: 30px;
            background: pink;
        }
</style>
```

![2-1](http://upload-images.jianshu.io/upload_images/6851923-581fb9c28577fa8f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![2-2](http://upload-images.jianshu.io/upload_images/6851923-07aa43bfb6228a9e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

所以结论是，200%是按照声明line-height:200%的元素的font-size计算的；2是按照元素继承或声明的font-size计算的，其中2叫缩放因子，子元素会继承父元素的缩放因子并乘以子元素自身的font-size值动态计算出最终的值。

### inline-block有什么特性？如何去除缝隙？高度不一样的inline-block元素如何顶端对齐?
1、特性和去除缝隙详见我的[博客](http://www.jianshu.com/p/99a63509bb4d)
2、顶端对齐`vertical-align: top;`

### CSS sprite 是什么?
CSS sprite直译过来就是**CSS精灵**。通常被解释为“**CSS图像拼合**”或“**CSS贴图定位**”。
**css sprites是什么通俗解释：**把网页中一些背景图片整合**拼合成一张图片中**，再利用CSS的背景定位技巧，如“background-image"，“background- repeat，“background-position”的组合进行背景定位，background-position可以用数字能精确的定位出背景图片在布局盒子对象位置。
 
### 让一个元素"看不见"有几种方式？有什么区别?
详见我的[博客](http://www.jianshu.com/p/dfc36d2ddb2e)

### 代码
1、[CSSsprite实现](https://dolbydot.github.io/task/task9/CSSsprite.html)
2、[字体图标实现](https://dolbydot.github.io/task/task9/iconfont.html)
