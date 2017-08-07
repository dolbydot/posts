### 块级元素和行内元素分别有哪些？动手测试并列出4条以上的特性区别
**块级元素：**

    <div>文档分区
    <h1>~<h6>
    <p>段落
    <hr>水平线
    <pre>预格式化文本
    <hgroup>标题组-实验中的功能。
    <ul>无序列表
    <ol>有序列表
    <table>表格
    <tfoot>表脚注
    <form>表单
    <fieldset>表单元素分组
    <output>表单输出
    <header>页头
    <footer>页尾
    <section>分区或节
    <artical>文章内容
    <aside>侧边栏
    <address>联系方式信息
    <noscript>不支持或禁用脚本时显示的内容
    <audio>音频
    <video>视频
    <blockquote>块引用
    <canvas>绘制图形
    <dd>定义列表中定义条目描述
    <dl>定义列表
    <figure>图文信息组
    <figcaption>图文信息组标题

**行内元素：**

    <span>
    <a>定义锚
    <b>定义粗体
    <i>定义斜体
    <tt>
    <abbr>定义缩写
    <acronym>定义取得首字母缩写
    <cite>定义引用
    <big>定义大号文本
    <small>定义小号文本
    <br>定义折行
    <dfn>定义定义项目
    <em>定义
    <strong>
    <img>定义图片
    <map>定义图像映射
    <script>定义脚本
    <sub>定义下标文本
    <sup>定义上标文本
    <button>定义按钮
    <input>定义输入框
    <label>定义表格标题
    <select>定义选择下拉列表
    <textarea>定义文本域

**区别**：

 - 一般行内元素只能包含数据和其他行内元素，块级元素可以包含行内元素和自身／其他块级元素。
 - 默认情况下块级元素占用一整行，而行内元素占据自身宽度空间。

 ![](http://upload-images.jianshu.io/upload_images/6851923-cfaa7a926c786ac8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 宽高只对块级元素设置生效，对行内元素无效。但如果给行内元素设定绝对定位（如a{position:absolute;}，脱离了正常文档流)，绝对定位会隐性的改变a的display为inline-block，此时就可以把a当成块状元素一样设置宽高了，除了给a显式的设置display值为none这种情况。

![](http://upload-images.jianshu.io/upload_images/6851923-4158a67605c13bd8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/6851923-61f23b2f4f200956.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/6851923-ec6998ec41e1f3c8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 块级元素可设置padding和margin，行内元素只能设置padding及左右margin，且设置padding时左右padding推开距离，上下padding会延伸出去，但不会增加上下两行间的距离。

![](http://upload-images.jianshu.io/upload_images/6851923-b83410752adbddd5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![](http://upload-images.jianshu.io/upload_images/6851923-76b17d5d7850e755.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![](http://upload-images.jianshu.io/upload_images/6851923-75b4f3cea896f9be.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

------ 
### 什么是 CSS 继承? 哪些属性能继承，哪些不能？
每个 [CSS 属性定义](https://developer.mozilla.org/en-US/docs/CSS/CSS_Reference) 的概述都指出了某个属性是默认继承的 ("Inherited: Yes") 还是默认不继承的 ("Inherited: no")。这决定了当你没有为元素的属性指定值时该如何计算值。
当元素的一个 **继承属性 （inherited property** **）**没有指定值时，则取父元素的同属性的 [计算值 computed value](https://developer.mozilla.org/en-US/docs/CSS/computed_value) 。只有文档根元素取该属性的概述中给定的[初始值](https://developer.mozilla.org/en-US/docs/CSS/initial_value)（[initial value](https://developer.mozilla.org/en-US/docs/CSS/initial_value)）（这里的意思应该是在该属性本身的定义中的默认值）。
# 
通过 CSS 继承，子元素将继承最高级元素所拥有的属性（这些子元素诸如 p, td, ul, ol, ul, li, dl, dt,和 dd）。如设置`body{font-family:Verdana;}`，不需要另外的规则，所有 body 的子元素都应该显示 Verdana 字体，子元素的子元素也一样。而比如p不想继承高级元素body的字体属性，只需要针对自身的特殊规则，如`p{font-family:Times}`，即可摆脱父元素的规则。
这就是CSS继承。
# 
**继承属性**：`color、font-size、font-family、font-style、letter-spacing、white-spacing、text-decoration、text-align、text-indent`等。
**非继承属性**：`display、height、width、padding、border、margin、min-width、max-width、min-height、max-height、background、overflow、position、float、clear、top、right、bottom、left、vertical-align`等。
# 
 **注意**：[inherit](https://developer.mozilla.org/zh-CN/docs/Web/CSS/inherit) 关键字 用于显式地指定继承性，可用于继承性/非继承性属性。


-----
### 如何让块级元素水平居中？如何让行内元素水平居中?
```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        h2 {
            width: 300px;
            background: pink;
            margin: 0 auto;
        }

        .class1 {
            position: relative;
            height: 400px;
            background: yellow;
        }

        p {
            width: 400px;
            background: green;
        }

        p {
            background: red;
            width: 200px;
            position: absolute;
            left: 50%;
            top: 50%;
            transform: translate(-50%, -50%);
        }

        .class2 {
            margin: 20px;
            padding: 10px;
            width: 400px;
            background: green;
            text-align: center;
        }
    </style>
</head>

<body>
    <h2>hello dolby!</h2>
    <div class="class1">
        <p>hello world!</p>
    </div> 
    <div class="class2"><a href="">hello main!</a></div>

</body>

</html>
```

![](http://upload-images.jianshu.io/upload_images/6851923-a5c61982b7765973.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

-----
### 用 CSS 实现一个三角形
```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        p {
            height: 0;
            width: 0;
            border-top: 0;
            border-right: 100px solid transparent;
            /* border-left: 100px solid transparent; */
            border-bottom: 100px solid red;
        }
    </style>
</head>

<body>
    <p></p>
</body>

</html>
```
-----
### 单行文本溢出加 ...如何实现?
以下样式可让文字过长时显示...，如果想提早出现...可给元素设置width或max-width属性。
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
       <style>  
        p{
            /*  设置文本不换行，直到遇到br标签为止  */
            white-space: nowrap;
            /*  设置溢出元素被蓉区的内容隐藏  */
            overflow: hidden;
            /*  设置文本溢出时显示省略号代表被隐藏的文本  */
            text-overflow: ellipsis;
        }
        
    </style> 
</head>

<body>
    <p>
        唐僧：你想要啊？你要是想要的话你就说话嘛，你不说我怎么知道你想要呢，虽然你很有诚意地看着我，可是你还是要跟我说你想要的。
  难道你真的想要吗？你想要的话我会给你的，你想要我怎么可能不给你呢？不可能你想我不给你，你不想要我却偏给你的。
  大家讲道理嘛！现在我数三下，你要说清楚你要不要……你真的想要吗？那你就拿去吧！你不是真的想要吧？
    </p>
</body>

</html>
```
![](http://upload-images.jianshu.io/upload_images/6851923-7cf97d58a3f1e754.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

-----
### 多行文本溢出加 ...如何实现?
以下样式可让段落过长时显示...，如果想提早出现...可给元素设置width或max-width属性。
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
       <style>  
        p{
            /*  设置文本框宽度及边框  */
            width: 300px;
            border: 1px solid black;
            /*  将对象作为弹性伸缩盒子模型显示  */
            display: -webkit-box;
            /*  设置或检索伸缩盒对象的子元素的排列方式  */
            -webkit-box-orient: vertical;
            /*  设置显示的文本行数  */
            -webkit-line-clamp: 3;
            /*  设置溢出元素内容区的内容隐藏  */
            overflow: hidden;
            /*  设置文本溢出时显示省略号代表被隐藏的文本  */
            text-overflow: ellipsis;
        }
        
    </style> 
</head>

<body>
    <p>
        唐僧：你想要啊？你要是想要的话你就说话嘛，你不说我怎么知道你想要呢，虽然你很有诚意地看着我，可是你还是要跟我说你想要的。
  难道你真的想要吗？你想要的话我会给你的，你想要我怎么可能不给你呢？不可能你想我不给你，你不想要我却偏给你的。
  大家讲道理嘛！现在我数三下，你要说清楚你要不要……你真的想要吗？那你就拿去吧！你不是真的想要吧？
    </p>
</body>

</html>
```

![](http://upload-images.jianshu.io/upload_images/6851923-790d9b9a4f29a638.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


-----
### px, em, rem 有什么区别
px: 绝对/固定单位，通常情况下浏览器默认文字大小为16px
em: 相对单位，表示当前字体大小是父容器字体大小的多少倍
rem:相对单位，表示当前字体大小是根元素(html)字体大小的多少倍，IE8及之前版本不支持。

-----
### 解释下面代码的作用?为什么要加引号? 字体里\5b8b\4f53代表什么?
```
body{
  font: 12px/1.5 tahoma,arial,'Hiragino Sans GB','\5b8b\4f53',sans-serif;
}
```
设置body字体大小为12px，行高为字体大小的1.5倍，字体取值依次是tahoma，arial，Hiragino Sans GB，宋体，sans-serif，浏览器会使用它可识别的第一个值。加引号是因为字体族名包含空格，不加会被浏览器误认为是多个族名。'\5b8b\4f53'：是“宋体”的Unicode编码表示。

-----
### 代码动手
 1. [各种背景及边框](https://dolbydot.github.io/task/task8/)
 2. [按钮及阴影](https://dolbydot.github.io/task/task8/index2.html)
 3. [表格](https://dolbydot.github.io/task/task8/index3.html)
 4. [三角形](https://dolbydot.github.io/task/task8/index4.html)
 5. [card](https://dolbydot.github.io/task/task8/index5.html)
