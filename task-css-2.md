>  1. class和id的使用场景。
>  2. CSS常见选择器。
>  3. 选择器的优先级是怎样的?复杂场景如何计算优先级？
>  4. 列出你知道的伪类选择器。
 
## [以上](http://www.jianshu.com/p/1ffaf3532bea)

----------
 5. a:link, a:hover, a:active, a:visited的顺序是怎样的？ 为什么？
依次是：
> a:link-选择所有未被访问的链接。
  a:visited-选择所有已被访问的链接。
  a:hover-选择鼠标指针位于其上的链接。
  a:active-选择活动链接。

原因：
与CSS样式定义书写原则有关，因浏览器解释CSS采取就近原则，所以最一般的条件放在最上面（外层），最特殊的条件放在最下面（内层）。
鼠标经过“未访问链接”同时拥有a:link、a:hover两种属性，后面的属性会覆盖前面的属性定义，鼠标经过的“已访问链接”同时拥有a:visited、a:hover两种属性，后面的属性会覆盖前面的属性定义。所以如CSS定义中所言，:hover 必须位于 :link 和 :visited 之后才有效，而:active必须被置于:hover之后才是有效的，如果没有指定伪类则默认为 :link。
-----
 6. 以下选择器分别是什么意思?
`#header{}`: 匹配id="header"的元素
`.header{}`: 匹配class="header"的元素
`.header .logo{}`: 匹配class="logo"且为class="header"的元素后代元素的元素。
`.header.mobile{}`: 匹配class="mobile"且class="header"的元素。
`.header p, .header h3{}`: 匹配class="header"的子元素p和子元素h3。
`#header .nav>li{}`: 匹配class=nav元素的所有子元素li，且class="nav"元素为id="header"元素的子元素。
`#header a:hover{}`:匹配鼠标悬停其上的a元素，且a元素为id="header"的元素的子元素。
`#header .logo~p{}`:匹配class="logo"的元素之后的同级元素p，且lass="logo"的元素为id="header"的元素的子元素。
`#header input[type="text"]{}`:匹配id="header"的元素下的 type="text"的input子元素。
----- 
 7. div:first-child、div:first-of-type、div :first-child和div :first-of-type的作用和区别 （注意空格的作用）
`div:first-child`:选择属于其父元素的首个子元素的每个div元素。
`div:first-of-type`:选择属于其父元素的首个div元素的每个div元素，等同于`:nth-of-type(1)`。
`div :first-child`:选择所有div元素的第一个子元素。
`div :first-of-type`:选择所有div元素下同类第一个div子元素。

**区别**：因为一个空格都脱离了必须是div类型的控制。也可理解为不加空格是同级，加了空格是后代。
**样例**：
```
<!DOCTYPE html>
<html lang="en">

<head>
    <style>
        .item1 :first-child {
            color: white;
        }

        .item1 :first-of-type {
            background: yellow;
        }
    </style>
</head>

<body>
    <div class="item1">
        <ul class="item1">
            <li class="item1">dd</li>
            <li>ff</li>
            <li>gg</li>
            <li>hh</li>
        </ul>
        <ol class="item1">
            <li class="item1">ii</li>
            <li class="item1">jj</li>
            <li>kk</li>
            <li>ll</li>
        </ol>
        <ol class="item1">
            <li class="item1">ii</li>
            <li class="item1">jj</li>
            <li>kk</li>
            <li>ll</li>
        </ol>
    </div>
    </div>
</body>

</html>
```
输出结果如下：

![](http://upload-images.jianshu.io/upload_images/6851923-be962fca985e82c1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

-----
 8. 运行如下代码，解析下输出样式的原因。
```
<style>
.item1:first-child{
  color: red;
}
.item1:first-of-type{
  background: blue;
}
</style>
 <div class="ct">
   <p class="item1">aa</p>
   <h3 class="item1">bb</h3>
   <h3 class="item1">ccc</h3>
 </div>
```
样式输出如下：

![](http://upload-images.jianshu.io/upload_images/6851923-01e30e20cd9a5673.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

首先外层定义`.item1:first-child{color: red;}`，选择属于其父元素的首个子元素的每个class="item1"的元素。代码中有三个class="item1"的元素p，h3，h3，属于同级兄弟关系，所以只有第一个子元素p被选中，表现为文本aa字色为红色。
接着内层定义`.item1:first-of-type{background: blue;}`，选择属于其父元素的首个class="item1"的元素的每个class="item1"的元素。代码中有三个class="item1"的元素p，h3，h3，所以p和第一个h3元素被选中，表现为背景色为蓝色。
