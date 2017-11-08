###  jQuery 中， $(document).ready()是什么意思？
(jQuery的load事件对应JS的onload事件，jQuery的ready事件对应JS的DOMContentLoaded事件，分别表示页面所有资源加载完成和页面DOM结构解析完成)

当DOM准备就绪时会发生ready事件，并执行ready內的函数。
由于该事件在文档就绪后就发生，所以正确做法是将所有其他jQuery事件和函数置于该事件中。
ready() 函数规定当 ready 事件发生时执行的代码，ready() 函数仅能用于当前文档，因此无需选择器。
所以以下三种语法是等价的
```
$(document).ready(function)
$().ready(function)
$(function)
```
看一个例子
```
<body>
    <ul>
        <li>item1</li>
        <li>item2</li>
        <li>item3</li>
        <li>item4 ![](http://upload-images.jianshu.io/upload_images/6851923-b0bda9c05c051541.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)</li>
    </ul>
    <script>
        $('ul').ready(function () {
            console.log('ul ready', Date.now())
            console.log($('img').width())
        })

        $('ul').load(function () {
            //这个没有打印值，因为load事件适用于任何可使用URL关联的任何元素：images,scripts,frames,iframes,window对象
            console.log('ul loaded', Date.now())
        })

        $('img').load(function () {
            console.log('img loaded', Date.now())
            console.log($('img').width())
        })

        $('img').ready(function () {
            console.log('img ready', Date.now())
            console.log($('img').width())
        })
    </script>
</body>
```
控制台打印结果为

![](http://upload-images.jianshu.io/upload_images/6851923-cc74f3af3a72a69f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

上例说明了两点：
- load事件适用于任何可使用URL关联的任何元素：images,scripts,frames,iframes,window对象等
- ready事件会在load事件前触发

### $node.html()和$node.text()的区别?
还是举个例子
```
<body>
    <ul>
        <li>item1 </li>
        <li>item2 </li>
        <li>item3 </li>

    </ul>
    <script>
        console.log($('li').html())//item1
        console.log($('li').text())//item1 item2 item3

        //无论如何外层的<li></li>不会发生改变
        console.log($('li').html('<span>insert span</span>'))//
        console.log($('li').text('insert text'))//
    </script>
</body>
```

![](http://upload-images.jianshu.io/upload_images/6851923-6026f7065cb3aab5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 相同点
html()和text()都是读写两用方法。
- 区别
    - html()对jQuery对象的html进行操作，相当于原生js的innerHTML；text()对jQuery对象的text进行操作，相当于原生js的innerText
    - 没有传递参数时，html()获取的是第一个匹配元素的innerHTML；text()获取的是所有匹配元素的innerText
    - 传递了string参数时，html()修改所有匹配元素的innerHTML为参数值，text()修改所有匹配元素的innerText为参数值

### $.extend 的作用和用法? 
`jQuery.extend([deep,] target [, object1 ] [, objectN ] )`
- 作用：将两个及以上的对象内容合并到目标对象，相同属性后面对象的值覆盖前面对象的值，target将被修改并通过$.extend()返回。参数 deep 为布尔值true/false，用来设置合并操作是否递归（深拷贝）。
如果只有一个参数提供给`$.extend()`，jQuery对象本身被默认为目标对象，这样，我们可以在jQuery的命名空间下添加新的功能，这对于插件开发者向 jQuery 中添加新函数时很有用。
- 用法：
如果我们想保留原对象，可通过传递一个空对象作为目标对象：
`var object = $.extend({}, object1, object2); //将object1, object2合并到{}中`
默认`$.extend()`合并操作是浅复制，如果第一个对象的属性本身是一个对象或数组，那么它将完全用第二个对象相同的key重写一个属性。这些值不会被合并。如果将 true作为该函数的第一个参数，那么会在对象上进行递归的合并。
```
<script>
    var object1 = {
        apple: 0,
        banana: {
            price: 200, user: {
                age: 20
            }
        },
        cherry: 97
    }
    var object2 = {
        durian: 100,
        banana: {
            weight: 52, name: ['dot', 'dolby', 'bob'], user: {
                age: 18
            }
        }
    }
    console.log($.extend(object1, object2))//浅复制，将object2合并到object1中
    console.log(object1)//object1为返回的最终结果
    console.log(object2)//object2值不变
    console.log($.extend(true, object1, object2))//深复制，将object2合并到object1中
</script>
```

### jQuery 的链式调用是什么？
链式调用适用于异步编程，可避免线程阻塞，实现原理是在当前函数执行完后return this，即返回该函数的执行环境，下一个函数就可以继续在这个函数下运行了，结果就是多种方法在一个jQuery对象上一个接一个地调用
示例
```
<body>
    <p>hello world</p>
    <h2>hello dolby</h2>
    <script>
        $('p').on('mouseenter', function () {
            $(this).css('background-color', 'red')
        }).on('mouseleave', function () {
            $(this).css('background-color', 'blue')
        }).parents('body').find('h2').toggle()
    </script>
</body>
```
本例中，mouseenter和mouseleave是事件监听，只有事件触发后才会执行相应函数中的代码，属于异步执行，与以上所说的在同一jQuery上一个接一个地调用方法并不冲突。
结果就是无论如何js引擎都会先执行`$('p').parents('body').find('h2').toggle()`切换h2的显示状态为隐藏，再根据用户是否触发鼠标事件来计算结果。

### jQuery 中 data 函数的作用
- 在匹配元素上存储任意的数据：
```
.data( key, [value] )
.data( obj )
```
- 返回匹配的元素集合中第一个元素给定名称的 数据上存储的数据：
```
.data()
.data( key )
```
作用：允许我们在DOM元素上绑定任意类型的数据，避免了循环引用可能产生的内存泄漏。
```
$('body').data('name', 'dot')
$('body').data('hobby', { fav: 'eat', love: 'food' })
$('body').data({ arr: [1, 2, 3, 4, 5] })

$('body').data('name')//dot
$('body').data()//{ name: "dot",hooby: { fav: "eat", love: "food" },arr: [1,2,3,4,5] }
```

### 写出以下功能对应的 jQuery 方法
- 给元素 $node 添加 class active，给元素 $node 删除 class active
```
$node.addClass('active')
$node.removeClass('active')
```
- 展示元素$node, 隐藏元素$node
```
$node.show()
$node.hide()
```
- 获取元素$node 的 属性: id、src、title， 修改以上属性
```
//获取属性
$node.attr('id')
$node.attr('src')
$node.attr('title')
//修改属性
$node.attr('id','newId')
$node.attr('src','newSrc')
$node.attr('title','newTitle')
```
- 给$node 添加自定义属性data-src
```
$node.prop('data-src')
```
- 在$ct 内部最开头添加元素$node
```
$ct.prepend($node)
$node.prependTo($ct)
```
- 在$ct 内部最末尾添加元素$node
```
$ct.append($node)
$node.appendTo($ct)
```
- 删除$node
```
$node.remove()
$ct.detach($node)
```
- 把$ct里内容清空
```
$ct.empty()
$ct.text('')
```
- 在$ct 里设置 html `<div class="btn"></div>`
```
$ct.html('<div class="btn"></div>')
```
- 获取、设置$node 的宽度、高度(分别不包括内边距、包括内边距、包括边框、包括外边距)

获取宽高
```
//不包括内边距
$node.width()
$node.height()
$node.css('width')
$node.css('height')

//包括内边距
$node.innerWidth()
$node.innerHeight()

//包括内边距，包括边框
$node.outerWidth()//不传参数或参数为false
$node.outerHeight()//不传参数或参数为false

//包括内边距，包括边框，包括外边距
$node.outerWidth(true)
$node.outerHeight(true)
```
设置宽高
```
//不包括内边距
$node.width(100)
$node.height('100px')
$node.css({width:'200px',height:'300px'})//设置元素的宽度和高度，也可以不要引号和单位

//包括内边距
$node.innerWidth(30)
$node.innerHeight('30px')

//包括内边距，包括边框
$node.outerWidth(60)
$node.outerHeight('60px')

//包括内边距，包括边框，包括外边距
$node.outerWidth(70,true)
$node.outerHeight('70px',true)
```
- 获取窗口滚动条垂直滚动距离
```
$(window).scrollTop()
```
- 获取$node 到根节点水平、垂直偏移距离
```
$node.offset().left
$node.offset().top
```
- 修改$node 的样式，字体颜色设置红色，字体大小设置14px
```
$node.css({
    'color': 'red',
    'font-size': '14px'
})
```
- 遍历节点，把每个节点里面的文本内容重复一遍
```
$node.each(function () {
    $(this).text($(this).text() + $(this).text())
})
```
- 从$ct 里查找 class 为 .item的子元素
```
$ct.find('.item')
$ct.children('.item')
```
- 获取$ct 里面的所有孩子
```
$ct.children()
```
- 对于$node，向上找到 class 为'.ct'的父亲，在从该父亲找到'.panel'的孩子
```
$node.parents('.ct').find('.panel')
```
- 获取选择元素的数量
```
$node.length
```
- 获取当前元素在兄弟中的排行
```
$node.index()
```

### 用jQuery实现以下操作
- 当点击$btn 时，让 $btn 的背景色变为红色再变为蓝色
```
var $btn = $('.btn')
$btn.on('click', function () {
    $(this).css('background-color', 'red')
    setTimeout(function () {
        $btn.css('background-color', 'blue')
    }, 500)
})
```
- 当窗口滚动时，获取垂直滚动距离
```
$(window).scroll(function () {
    $node.text($(this).scrollTop())//用html替换text也可
})
```
- 当鼠标放置到$div 上，把$div 背景色改为红色，移出鼠标背景色变为白色
```
var $div = $('div')
$div.on('mouseenter', function () {
    $(this).css('background', 'red')
}).on('mouseleave', function () {
    $(this).css('background', 'white')
})
```
- 当鼠标激活 input 输入框时让输入框边框变为蓝色，当输入框内容改变时把输入框里的文字小写变为大写，当输入框失去焦点时去掉边框蓝色，控制台展示输入框里的文字
```
var $input = $('input')
$input.focus(function () {
    $(this).css('border-color', 'blue')
        .on('keyup', function () {
            $(this).val($(this).val().toUpperCase())
        })
})

$input.blur(function () {
    $(this).css('border-color', 'black')
    console.log($(this).val())
})
```
- 当选择 select 后，获取用户选择的内容
```
//html
<select>
    <option value="1">item 1</option>
    <option value="2">item 2</option>
    <option value="3">item 3</option>
    <option value="4">item 4</option>
    <option value="5">item 5</option>
</select>
<p>用户选取的内容是：<span></span></p>

//js
$('select').on('change', function () {
    $('span').text($('select>option:selected').text())
})
```

### 用 jQuery ajax 实现如下效果。
当点击加载更多会加载数据展示到页面[效果预览393](http://jrgzuoye.applinzi.com/%E4%BD%9C%E4%B8%9A%E5%AE%89%E6%8E%92/jscode/JS9-jqueryajax/1.html)
[*我的代码*](https://github.com/dolbydot/task/blob/master/advance-task15/index.html)

### （可选）实现一个天气预报页面，UI 如下图所示(仅供参考，可自由发挥)。
- 数据接口:
    - 获取天气接口：http(s)://weixin.jirengu.com/weather
    - 服务端支持 CORS 跨域调用，前端可直接使用 ajax 获取数据，返回数据以及使用方式参考 [http://api.jirengu.com16](http://api.jirengu.com/)

- 更多接口参考 [http://api.jirengu.com16](http://api.jirengu.com/)

![](http://upload-images.jianshu.io/upload_images/6851923-dbf7be3362738e09.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**参考资料**：
- [*jQuery获取和设置元素宽高*](https://github.com/yoowinsu/blog/issues/6)
- [*jquery如何获取元素的滚动条高度*](https://www.ctolib.com/topics-75962.html)

PS：关于jQuery获取和设置元素innerWidth和outerHeight等、网上有很多文章代码或者方法总结得有问题，一定要以自己试过的结论为准。