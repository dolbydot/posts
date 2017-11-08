## 三种引入方式：
1、内联样式：直接写在元素开始标签的style属性中，如
`<div style="background:red;height:100px;"></div>`
2、内部样式表：放在head元素内的style标签中，如
```html
<head>
<style type="text/css">
p {margin-left: 20px;}
body {background-image: url("images/back40.gif");}
</style>
</head>
```
3、外部样式表：扩展名为.css的文件,文件中不能包含任何html标签，外部样式表的引入又分为两种情况：

- 放置于head元素内的link标签中，如：
```
<head>
<link rel="stylesheet" type="text/css" href="mystyle.css" />
</head>
```
- 放置于head元素内的style标签中或直接写入样式表中，如：
```
<style>
  @import url("1.css");
  @import "2.css";
</style>
```

-----
## link和@import的三点区别：

 1. link是一个html标签，除了可以加载css文件外还可以做很多其他的事情，如定义rel链接属性等。而@import是css提供的一种方式，只能用来加载css文件。
 2. IE5之前的浏览器不支持@import，link没有这个问题。
 3. link支持使用js控制DOM改变样式，@import不行。

查阅很多资料，显示出二者还有第4种差别：

> 加载顺序的差别。link 和页面本体是会同时加载的，而 @import 得等到页面加载完成再加载。所以有时候浏览@import加载CSS的页面时开始会没有样式（就是闪烁）。

**亲测结果**：
无论是@import定义的还是link引入的外部样式表，浏览器（chrome）都会按照从上往下的规则解析。**`所以第四点区别是不正确的。`**
# 
测试代码如下：
# 
**demo1.css** 其中插入了一个本地图片**pikachu.png**
```
h2{
    color:red;
    background: green;
}
body{
    background-image: url('./pikachu.png');
}
```
**demo2.css**
```
h2{
    color:black;
}
```
**script.js**
```
for(var i=0;i<10000;i++){
    console.log(12);
}
```
**demo1.html**
```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        @charset "utf-8";
        @import './demo2.css';
    </style>
    <script src="./script.js"></script>
    <link rel="stylesheet" type="text/css" href="./demo1.css" />

</head>

<body>
    <h2>hello dolby</h2>
</body>

</html>
```
在浏览器打开网页，打开开发者工具，切换到Network状态，选择常规网速regular 2G，结果如下：

![](http://upload-images.jianshu.io/upload_images/6851923-1949dc2501491e6a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/6851923-b8fe3544ab981e54.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

可以看出浏览器依次加载了demo1.html、demo2.css、script.js、demo1.css、pikachu.png，即先加载html文件形成文档结构，再按从上往下的顺序依次加载外部文件。

降低网速再刷新一次：

![](http://upload-images.jianshu.io/upload_images/6851923-4e94d9c0fad77169.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

结果相同，说明@import和link引入外部样式表的第四点区别并不成立。

如果这些还不能说服你，那么查看一下事件日志：

![](http://upload-images.jianshu.io/upload_images/6851923-a5c3ac7ccb7092f0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/6851923-f87df3812c03ee72.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

很明显可以看出，发送请求的先后顺序为，demo2.css、demo1.css。

欢迎打脸！