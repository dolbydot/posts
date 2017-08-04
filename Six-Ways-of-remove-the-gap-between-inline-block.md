inline-block是一个块状行盒，表现为一个行内元素，它既拥有了块状元素可以设置width和height的特性，又保留了行内元素不换行的特点。
应用了`display:line-block`属性的元素会生成一个块状盒，该块状盒随着周围内容流动，如同它是一个单独的行内盒子，其表现更像是一个被替换的元素。
# 
真正意义上inline-block水平呈现的元素间，换行显示或空格分隔的情况下会有间距，上代码：
```
    <input />
    <input type="submit" />
```
![](http://upload-images.jianshu.io/upload_images/6851923-3565e3a38a30bcf0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

使用CSS更改非inline-block水平元素为inline-block水平也会有该问题：
```html
<style>
        a {
            background: pink;
            display: inline-block;
            padding: .5em 1em;
        }
</style>
<div>
        <a href="">链接1</a>
        <a href="">链接2</a>
        <a href="">链接3</a>
        <a href="">链接4</a>
</div>
```
![](http://upload-images.jianshu.io/upload_images/6851923-a0aa509729ed5610.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
以上情况是符合规范的应有表现，但这类间距有时会对我们的布局或兼容性产生影响，所以要想办法去掉它，以下示例几种方法～

### 1. 移除空格
元素间留白间距的出现原因即标签段间的空格，去掉空格间距自然没有了。
以下是几种写法：
```
    <div>
        <a href="">
        链接1</a><a href="">
        链接2</a><a href="">
        链接3</a><a href="">
        链接4</a>
    </div>
```
```
    <div>
        <a href="">链接1</a
        ><a href="">链接2</a
        ><a href="">链接3</a
        ><a href="">链接4</a>
    </div>
```
```
    <div>
        <a href="">链接1</a><!--
        --><a href="">链接2</a><!--
        --><a href="">链接3</a><!--
        --><a href="">链接4</a>
    </div>
```
三种写法都能达到去除缝隙的效果：

![](http://upload-images.jianshu.io/upload_images/6851923-ce0e864aefa43c87.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 2. 使用margin负值
margin负值的大小与上下文字体和文字大小有关，由于外部环境的不确定性及最后一个元素多出的父margin值等问题，此方法不适合大规模使用。
```
<style>
        a {
            background: pink;
            display: inline-block; 
            padding: .5em 1em;
            margin: -3px;
        }
</style>
<body>
    <div>
        <a href="">链接1</a>
        <a href="">链接2</a>
        <a href="">链接3</a>
        <a href="">链接4</a>
    </div>
</body>
```
![](http://upload-images.jianshu.io/upload_images/6851923-8a4036124944ee63.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 3. 删掉闭合标签
HTML5中可以很任性：虽然这样很怪但确实有效。
```
    <div>
        <a href="">链接1
        <a href="">链接2
        <a href="">链接3
        <a href="">链接4      
    </div>
```
![](http://upload-images.jianshu.io/upload_images/6851923-88209161399463c8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 4. 使用font-size:0
```
<style>
        div{
            font-size: 0;
        }
        a{
            font-size: 16px;
            background: pink;
        }
</style>
<div>
        <a href="">链接1</a>
        <a href="">链接2</a>
        <a href="">链接3</a>
        <a href="">链接4</a>
</div>
```
![](http://upload-images.jianshu.io/upload_images/6851923-54b9ba41efbdfb8e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 5. 使用letter-spacing
```
<style>
        div{
            letter-spacing: -6px;
        }
        a{
            letter-spacing: 0;
            background: pink;
        }
</style>
<div>
        <a href="">链接1</a>
        <a href="">链接2</a>
        <a href="">链接3</a>
        <a href="">链接4</a>
</div>
```
![](http://upload-images.jianshu.io/upload_images/6851923-61906bb90c673380.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 6. 使用word-spacing
```
<style>
        div{
            word-spacing: -6px;
        }
        a{
            word-spacing: 0;
            background: pink;
        }
</style>
<div>
        <a href="">链接1</a>
        <a href="">链接2</a>
        <a href="">链接3</a>
        <a href="">链接4</a>
</div>
```
![](http://upload-images.jianshu.io/upload_images/6851923-61906bb90c673380.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

*参考资料*：
[去除inline-block元素间间距的N种方法](http://www.zhangxinxu.com/wordpress/2012/04/inline-block-space-remove-%E5%8E%BB%E9%99%A4%E9%97%B4%E8%B7%9D/)
