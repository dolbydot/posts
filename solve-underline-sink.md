直接上代码：
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        .aa {
            /*  设置字号为浏览器默认字体大小的三倍  */
            font-size: 3em;
            /*  设置文本全大写  */
            text-transform: uppercase;
            /*  添加下划线  */
            text-decoration: underline; 
        }

        .aa:first-letter {
            /*  用伪元素来控制首字母大写，字号为当前元素字号的两倍  */
            font-size: 2em;
        }

        .bb {
            /*  设置字号为浏览器默认字体的三倍  */
            font-size: 3em;
            /*  设置以小型大写字母的字体显示文本，即字号小于3em  */
            font-variant: small-caps;
            /*  设置首个字母以大写字母开头，此时字号为浏览器默认字体大小的三倍  */
            text-transform: capitalize;
            /*  添加下划线  */
            text-decoration: underline;
        }
    </style>
</head>

<body>
    <p class="aa">abcdefg</p>
    <p class="bb">abcdefg</p>
</body>

</html>
```
效果如图所示：

![](http://upload-images.jianshu.io/upload_images/6851923-cbcdb5a435cc42a8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
